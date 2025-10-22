---
title: Mostrar precios gravados con la API Mesh
description: Use [!DNL API Mesh] para Adobe Commerce y el servicio de catálogo para mostrar los precios, incluidos los impuestos.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: ca62c653-29b9-45cf-b2d4-8cb693b08aac
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Mostrar precios gravados con API Mesh para Adobe Developer App Builder

[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permite a los desarrolladores integrar API privadas o de terceros y otras interfaces con productos de Adobe mediante Adobe I/O Runtime.

En este tema, API Mesh se utiliza para mostrar los precios de los productos en una página de detalles del producto con los impuestos incluidos en.

## Configurar tipos impositivos

Debe tener los impuestos configurados para que se muestren en la página Detalles del producto.

1. [Configurar tasas de impuestos](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/taxes/tax-rules.html).
1. Habilite que los impuestos se [muestren en el catálogo](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/taxes/display-settings.html#step-1%3A-configure-catalog-prices-display-settings) y configúrelo en `Including and Excluding Tax` o `Including Tax`.

Compruebe que el servicio de catálogo funciona en la página de detalles del producto.

![Impuestos mostrados en la página de detalles del producto](assets/display-tax.png)

## Configuración de API Mesh

Si aún no lo ha hecho, conecte la API Mesh con el servicio de catálogo a su instancia. Consulte las instrucciones detalladas en el tema [Introducción](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/) de la guía para desarrolladores de API Mesh.

En el archivo `mesh.json`, reemplace los valores `name`, `endpoint` y `x-api-key`.

```json
{
    "meshConfig": {
      "sources": [
        {
          "name": "<NAME OF MESH>",
          "handler": {
            "graphql": {
              "endpoint": "<COMMERCE INSTANCE GQL ENDPOINT URL>"
            }
          },
          "transforms": [
              {
                  "prefix": {
                      "includeRootOperations": true,
                        "value": "Core_"
                  }
              }
          ]
        },
        {
          "name": "CommerceCatalogServiceGraph",
          "handler": {
            "graphql": {
              "endpoint": "https://catalog-service-sandbox.adobe.io/graphql/",
              "operationHeaders": {
                "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
                "Magento-Website-Code": "{context.headers['magento-website-code']}",
                "Magento-Store-Code": "{context.headers['magento-store-code']}",
                "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
                "x-api-key": "API_KEY",
                "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
              },
              "schemaHeaders": {
                "x-api-key": "<YOUR API_KEY>"
              }
            }
          }
        }
      ],
      "additionalTypeDefs": "extend type ComplexProductView {\n  priceWithTaxes: Core_PriceRange\n}\n extend type SimpleProductView {\n  priceWithTaxes: Core_PriceRange\n}\n",
      "additionalResolvers": [
            {  
              "targetTypeName": "ComplexProductView",
              "targetFieldName": "priceWithTaxes",
              "sourceName": "MagentoQACore",
              "sourceTypeName": "Query",
              "sourceFieldName": "Core_products",
              "requiredSelectionSet": "{\n items {\n sku, \n price_range {\n minimum_price {\n final_price {\n value\n currency\n }\n }\n }\n }\n }",
                "sourceArgs": {
                    "filter.sku.eq": "{root.sku}"
                },
                "result": "items[0].price_range"
            },
            {  
              "targetTypeName": "SimpleProductView",
              "targetFieldName": "priceWithTaxes",
              "sourceName": "MagentoQACore",
              "sourceTypeName": "Query",
              "sourceFieldName": "Core_products",
              "requiredSelectionSet": "{\n items {\n sku, \n price_range {\n minimum_price {\n final_price {\n value\n currency\n }\n }\n }\n }\n }",
                "sourceArgs": {
                    "filter.sku.eq": "{root.sku}"
                },
                "result": "items[0].price_range"
            }
        ]
     }
  }
```

Este archivo de configuración de `mesh.json`:

* Transforma la aplicación principal de Commerce para que requiera &quot;Core_&quot; delante de cualquiera de sus consultas o tipos. Esto evita posibles conflictos de nomenclatura con el servicio de catálogo.
* Amplía los tipos `ComplexProductView` y `SimpleProductView` con un nuevo campo denominado `priceWithTaxes`.
* Agrega una resolución personalizada para el nuevo campo.

Cree la malla con el [comando create](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1) con el archivo `mesh.json`.

### GraphQL query

Puede recuperar los nuevos datos de `priceWithTaxes` mediante GraphQL.

Ejemplo de consulta:

```graphql
query {
    products(skus:[MH07]) {
        __typename
        id
        sku
        name
        description
        shortDescription
        addToCartAllowed
        url
        ... on ComplexProductView {
            priceWithTaxes {
              minimum_price {
                final_price {
                  value
                }
              }
              maximum_price {
                final_price {
                  value
                }
              }
            }
            priceRange {
                maximum {
                    final {
                        amount {
                            value
                            currency
                        }
                    }
                    regular {
                        amount {
                            value
                            currency
                        }
                    }
                    roles
                }
                minimum {
                    final {
                        amount {
                            value
                            currency
                        }
                    }
                    regular {
                        amount {
                            value
                            currency
                        }
                    }
                    roles
                }
            }
        }
    }
}
```

Respuesta de consulta:

```json
{
  "data": {
    "products": [
      {
        "__typename": "ComplexProductView",
        "id": "VFVnd053AFpHVm1ZWFZzZEEAWkRWa09Ua3hNVFl0WTJJd015MDBaRGMwTFRnME16a3RNak01TVRVNE9ESTBOemd4AGJXRnBibDkzWldKemFYUmxYM04wYjNKbABZbUZ6WlEAVFVGSE1EQTFPRFEyTVRjeA",
        "sku": "MH07",
        "name": "Hero Hoodie13",
        "description": "<p>Gray and black color blocking sets you apart as the Hero Hoodie keeps you warm on the bus, campus or cold mean streets. Slanted outsize front pockets keep your style real . . . convenient.</p>\r\n<p>* Full-zip gray and black hoodie.<br />* Ribbed hem.<br />* Standard fit.<br />* Drawcord hood cinch.<br />* Water-resistant coating.</p>",
        "shortDescription": "",
        "addToCartAllowed": true,
        "url": "http://commerce_url/hero-hoodie.html",
        "priceWithTaxes": {
          "minimum_price": {
            "final_price": {
              "value": 8.330001
            }
          },
          "maximum_price": {
            "final_price": {
              "value": 13355.524701
            }
          }
        },
        "priceRange": {
          "maximum": {
            "final": {
              "amount": {
                "value": 39.02,
                "currency": "USD"
              }
            },
            "regular": {
              "amount": {
                "value": 54,
                "currency": "USD"
              }
            },
            "roles": [
              "visible"
            ]
          },
          "minimum": {
            "final": {
              "amount": {
                "value": 39.02,
                "currency": "USD"
              }
            },
            "regular": {
              "amount": {
                "value": 54,
                "currency": "USD"
              }
            },
            "roles": [
              "visible"
            ]
          }
        }
      }
    ]
  },
  "extensions": {}
}
```
