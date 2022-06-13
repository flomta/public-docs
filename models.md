# Flomta entities

## Business entities

### Account

[Account](/models.md#Account) is a primary level business entity. An account is a dividing entity separating logical 
access between different accounts. All [business entities](/models.md#business-entities) down the tree _belong_ to _one_ 
[Account](/models.md#Account). An [User](models.md#user) can be part of multiple Accounts via being an [AccountManager](/models.md#AccountManager). 

### AccountManager
....

AccountManager is an [User] (###user) who has been granted the account-administrative permissions on one [Account] (/##account)
### Company

### Building

### Apartment

### Meter

### Period

### Reading

### Report

### Notification

### User
