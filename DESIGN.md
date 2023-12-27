
The catagorized table takes both the column as `FOREIGN KEYS`.

#### Employees

The `employees` table includes:

* `id`, which specifies the unique ID for the employee as an `INTEGER`. This column thus has the `PRIMARY KEY` constraint applied.
* `first_name`, which specifies the employee's first name as `TEXT`.
* `last_name`, which specifies the employee's last name as `TEXT`.
* `contact`, which specifies the employee's contact number as `INTEGER`.
* `role`, which specifies the employee's role as `TEXT`. The purpose of role was to give specific access to the employees. But SQLite users can access the whole database.

#### Audit Trial

The `audit_trial` table includes:

* `employee_id`, which specifies the unique ID of the employee associated with the audit trail as an `INTEGER`.
* `date_of_change`, which specifies the date and time of the change in the audit trail as `DATETIME`. This column has the `NOT NULL` constraint and defaults to the current timestamp when a new row is inserted.
* `change_type`, which specifies the type of change made, represented as `TEXT`. The change type can be `INSET`, `UPDATE`, `DELETE` etc.
* `changed_table_name`, which specifies the name of the table where the change occurred as `TEXT`.
* `changed_column_name`, which specifies the name of the column that was changed as `TEXT`.
* `old_value`, which represents the previous value before the change as `NUMERIC(10,2)`.
* `new_value`, which represents the new value after the change as `NUMERIC(10,2)`.



### Relationships

The below entity relationship diagram describes the relationships among the entities in the database.

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
SUPPLIER ||--o{ SUPPLIED_PRODUCT : has
PRODUCT }o--|{ SUPPLIED_PRODUCT : is
SUPPLIED_PRODUCT{
    supplierID int FK
    productID int FK
}

ORDERS }|--o{ PRODUCT : includes
ORDERS{
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
PRODUCT }o--|{ SALE : has
SALE{
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
EMPLOYEES }o--o{ PRODUCT : manages
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
    changedTableName string
    columnChanged string
    oldValue string
    newValue string
}
```
As detailed by the diagram:

* One student is capable of making 0 to many submissions. 0, if they have yet to submit any work, and many if they submit to more than one problem (or make more than one submission to any one problem). A submission is made by one and only one student. It is assumed that students will submit individual work (not group work).
* A submission is associated with one and only one problem. At the same time, a problem can have 0 to many submissions: 0 if no students have yet submitted work to that problem, and many if more than one student has submitted work for that problem.
* A comment is associated with one and only one submission, whereas a submission can have 0 to many comments: 0 if an instructor has yet to comment on the submission, and many if an instructor leaves more than one comment on a submission.
* A comment is written by one and only one instructor. At the same time, an instructor can write 0 to many comments: 0 if they have yet to comment on any students' work, and many if they have written more than 1 comment.
