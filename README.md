# Middleware Engineering "Distributed Architecture and Document Formats"

*Autor:* **Benjamin Princ**<br>
*Datum:* **19.09.2023**

## Aufgabenstellung
Die detaillierte [Aufgabenstellung](TASK.md) beschreibt die notwendigen Schritte zur Realisierung.

## Arbeitsschritte
1. Zusätzliche Attribute zum Warehouse hinzugefügt.
2. Produkt Implementierung begonnen:<br>
2.1. Package "product" mit Klasse "[ProductData](src/main/java/tradearea/product/ProductData.java)" erstellt.<br>
2.2. Objektklasse (Attribute, Konstruktor) gecodet. Anfangs statisch, später dynamisch mit zufälligen Produkten.

## Implementierung

### Umwandlung in verschiedene Dateiformate
*Klasse [WarehouseController](src/main/java/tradearea/warehouse/WarehouseController.java)*
```java
@RequestMapping(value="/warehouse/{inID}/data", produces = MediaType.APPLICATION_JSON_VALUE)
(...)
```
```java
@RequestMapping(value="/warehouse/{inID}/xml", produces = MediaType.APPLICATION_XML_VALUE)
(...)
```
Mit dem RequestMapping wird angegeben bei welchem Pfad(1. Parameter) der Code darunter ausgeführt wird.
Zusätzlich wird angegeben im welchen Format(2. Parameter) der Client die Daten erhalten wird.

### Warenhausdaten
*Klasse [WarehouseData](src/main/java/tradearea/model/WarehouseData.java)*
```java
private String warehouseAddress;
private int warehousePostalCode;
private String warehouseCity;
private String warehouseCountry;
```
Diese vier Parameter zu den Warenhausdaten hinzugefügt.

### Produkte generieren
*Klasse [ProductData](src/main/java/tradearea/product/ProductData.java)*
```java
private final String[][] randomProduct = {
            {"Apfel", "Obst", "Kiste 1kg"}, (...)
    };

    public String getTempProductName(int index) {
        return randomProduct[index][0];
    }

    public String getTempProductCategory(int index) {
        return randomProduct[index][1];
    }

    public String getTempProductUnit(int index) {
        return randomProduct[index][2];
    }
```
Mit Hilfe einer generierten index Nummer kann ein Beispiel Produkt ausgewählt werden und die dazugehörigen Attribute abgefragt werden.
### Produkte zum Warenhaus hinzufügen
*Klasse [WarehouseSimulation](src/main/java/tradearea/warehouse/WarehouseSimulation.java)*
```java
public WarehouseData getData( String inID ) {
		(...)
        
		ProductData p1 = new ProductData();
		(...)
		ProductData p5 = new ProductData();
		data.setProductData(new ProductData[]{p1, p2, p3, p4, p5});
		return data;
		
	}
```
Es können beliebig viele Produkt Objekte erstellt werden, welche anschließend in Form eines ProductData-Arrays als Warehouse Attribut gesetzt werden.
## Quellen
[1], **ID generieren**, https://stackoverflow.com/questions/1389736/how-do-i-create-a-unique-id-in-java