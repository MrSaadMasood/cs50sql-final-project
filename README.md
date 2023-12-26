erDiagram
    
    PRODUCT }|--o{ SUPPLIER : has
    PRODUCT {
        id int PK
        tradeName string
        activeIngredient string
        composition string
        packingSize string
        packingType string
        manufacturer string
        SKU int
        unitPrice int
    }
    
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
    
    SUPPLIED{
        supplierID int FK
        productID int FK
    }
    
    ORDER }o--|{ PRODUCT : has
    ORDER{
        id int PK
        orderDate date
        expectedDelivery date
        orderCost real
    }
    CUSTOMERS }|--|{ PRODUCT : has
    CUSTOMERS{
        id int PK
        name string
        conact int
    }
    SALES }o--|{ PRODUCT : has
    SALES{
        productID int FK
        productQuantity real
        productBoxPrice real
        totalSale real
        saleDate date
    }
    CATAGORY }|--|{PRODUCT : has
    CATAGORY{
        id  int PK
        productID int FK
        type string
    }
    
    EXPLOYEES{
        id int PK
        firstName string
        secondName string
        contact int
        role string
    }
    
