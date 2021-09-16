# Prueba técnica frontend

## Se solicita realizar

- Una aplicación React Native
- Un Api (backend / server) en NodeJs que se comunique con https://services.odata.org/V3/Northwind/Northwind.svc

## Funcionalidades esperadas

- Listado de ordenes realizadas donde se pueda visualizar CustomerID, ShippedDate (con formato dia/mes/año -> 01/01/2001), ShipCity y ShipCountry
- Al seleccionar una orden visualizar el listado de productos que fueron vendidos en la orden seleccionada, permitiendo visualizar ProductName y calcular el precio total de cada producto usando los valores de la orden (UnitPrice \* Quantity). Además mostrar en pantalla la suma total de los subtotales de todos los productos (Subtotal), el total de todos los descuentos (Discount) y el total de la orden (SUBTOTAL - DISCOUNT).
  Por ejemplo para la orden:

```json
{
  "odata.metadata": "https://services.odata.org/V3/Northwind/Northwind.svc/$metadata#Order_Details",
  "value": [
    {
      "Product": {
        "ProductID": 14,
        "ProductName": "Tofu",
        "SupplierID": 6,
        "CategoryID": 7,
        "QuantityPerUnit": "40 - 100 g pkgs.",
        "UnitPrice": "23.2500",
        "UnitsInStock": 35,
        "UnitsOnOrder": 0,
        "ReorderLevel": 0,
        "Discontinued": false
      },
      "OrderID": 1,
      "ProductID": 14,
      "UnitPrice": "18.6000",
      "Quantity": 9,
      "Discount": 0
    },
    {
      "Product": {
        "ProductID": 51,
        "ProductName": "Manjimup Dried Apples",
        "SupplierID": 24,
        "CategoryID": 7,
        "QuantityPerUnit": "50 - 300 g pkgs.",
        "UnitPrice": "53.0000",
        "UnitsInStock": 20,
        "UnitsOnOrder": 0,
        "ReorderLevel": 10,
        "Discontinued": false
      },
      "OrderID": 1,
      "ProductID": 51,
      "UnitPrice": "42.4000",
      "Quantity": 40,
      "Discount": 10
    }
  ]
}
```

Los valores esperados son:

```
Tofu                         167,40
Manjimup Dried Apples       1696,00
___________________________________
Subtotal                    1863,40
Discounts                     10,00
___________________________________
Total                       1853,40
```

## Que se debe entregar

- Código fuente de la aplicación RN y del BFF (pueden ser repositorios diferentes o usar un monorepo). El nombre del o de los repositorios deberá ser según el tipo de repositorio

  - `<CODIGO_PROVISTO>`-rn si el repositorio solo contiene la app React Native (ej: north-0001-rn)

  - `<CODIGO_PROVISTO>`-ms si el repositorio solo contiene el codigo del MS
    (ej: north-0001-ms)

  - `<CODIGO_PROVISTO>`-mono si el repositorio contiene la app RN y el MS
    (ej: north-0001-mono)

  siendo `<CODIGO_PROVISTO>` un identificador único por candidato

- Entregar un Readme con los pasos para ejecutar la aplicación (suponiendo que ya el ambiente está preparado para compilar RN y NodeJs)
- Agregar también en un archivo Markdown indicando como fue realizado la separación de tareas para cumplir con las 2 funcionalidades.

## Que se evaluará

- **Calidad del código**: nomenclatura, estilo, extensibilidad, flexibilidad
- **Manejo de errores**: como se procede cuando ocurren errores inesperados
- **Componentización**: como se diseñaron los componentes para permitir reutilización
- **Interfaz de usuario presentada**: diseño y estilos utilizados
- **Manejo de Git**: commits claros que permitan seguir la historia de como se realizo el desarrollo, utilización de Pull Requests

## Notas útiles

- Para acceder al MS en formato json se puede hacer agregando un query param `$format=json` en el request. Por ej: https://services.odata.org/V3/Northwind/Northwind.svc/Order_Details_Extendeds?$format=json
- Al acceder a https://services.odata.org/V3/Northwind/Northwind.svc/$metadata se puede ver un XML donde se presentan todos los endpoints disponibles
- https://philcalcado.com/2015/09/18/the_back_end_for_front_end_pattern_bff.html
- https://nestjs.com
- https://expressjs.com/es/

## Endpoints útiles:

- Listado de ordenes: https://services.odata.org/V3/Northwind/Northwind.svc/Orders?$format=json
- Detalle de una orden en particular: https://services.odata.org/V3/Northwind/Northwind.svc/Orders(1234)?$format=json
- Detalle de los productos de una orden en particular: https://services.odata.org/V3/Northwind/Northwind.svc/Orders(1234)/Order_Details?$format=json&$expand=Product
