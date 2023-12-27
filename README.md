```mermaid
erDiagram
PHARMACY }o--|{PRODUCT : has
PHARMACY{
    id int PK
    name string
    accountNumber int
    accountBalance int
}
PRODUCT {
    id int PK
    tradeName string
    activeIngredient string
    composition string
    packingSize int
    packingType string
    manufacturer string
    SKU int
}
PRODUCT }o--o{ STOCK : in
STOCK ||--o{ SUPPLIER : has
    STOCK {
        productID int FK
        supplierID int FK
        stockPacks real
        ProfitPerPackSold real
        unitPrice real
        arrivalDate date
        expirationDate date

    }

SUPPLIER{
    id string PK
    name string
    contact int
    accountNumber int
    accountBalance int

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
    status string
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
    productBoxQuantity real
    productBoxPrice real
    totalSale real
    profitOnSale real
    saleDate date
}
PRODUCT}|--|{AVAILABLE_CATAGORIES : in
AVAILABLE_CATAGORIES{
    id int PK
    name string
}
AVAILABLE_CATAGORIES }|--|{CATEGORIZED : by
CATEGORIZED{
    CatagoryID  int FK
    productID int FK
}
EMPLOYEES }o--o{ PRODUCT : handles
EMPLOYEES{
    id int PK
    firstName string
    secondName string
    contact int
    role string

}
EMPLOYEES }|-- o{ AUDIT_TRAIL : induce
AUDIT_TRAIL {
    dateOfChange date
    employeeID int FK
    changeType string
    changedTableName int FK
    columnChanged string
    oldValue string
    newValue string
}
