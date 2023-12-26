```mermaid
erDiagram
PRODUCT {
    id int PK
    tradeName string
    activeIngredient string
    composition string
    packingSize string
    packingType string
    manufacturer string
    SKU int
}
PRODUCT }o--o{ STOCK : in
STOCK ||--o{ SUPPLIER : has
    STOCK {
        id int PK
        productID int FK
        supplierID int FK
        stockPacks real
        ProfitPerPackSold real
        unitPrice real
        expirationDate date
        arrivalDate date

    }

SUPPLIER{
    id string PK
    name string
    contact int

}
SUPPLIER ||--o{ SUPPLIED : has
PRODUCT }o--|{ SUPPLIED : is
SUPPLIED{
    supplierID int FK
    productID int FK
}

ORDER }|--o{ PRODUCT : has
ORDER{
    id int PK
    orderDate date
    expectedDelivery date
    orderCost real
}
PRODUCT }|--|{ CUSTOMERS : has
CUSTOMERS{
    id int PK
    name string
    contact int
}
PRODUCT }o--|{ SALES : has
SALES{
    productID int FK
    productQuantity real
    productBoxPrice real
    totalSale real
    saleDate date
}
PRODUCT }|--|{CATEGORY : has
CATEGORY{
    id  int PK
    productID int FK
    type string
}
EMPLOYEES }o--o{ PRODUCT : handles
EMPLOYEES{
    id int PK
    role string
    firstName string
    secondName string
    contact int
}
EMPLOYEES }|-- o{ AUDIT_TRAIL : induce
AUDIT_TRAIL {
    dateTime date
    userID int FK
    changeType string
    changedTableID int FK
    columnChanged string
    oldValue string
    newValue string
}
