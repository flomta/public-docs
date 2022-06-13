# Flomta entities

## Business entities

### Account

[Account](/models.md#Account) is a primary level business entity. An account is a dividing entity separating logical 
access between different accounts. All [business entities](/models.md#business-entities) down the tree _belong_ to _one_ 
[Account](/models.md#Account). An [User](models.md#user) can be part of multiple Accounts via being an 
[AccountManager](/models.md#AccountManager). Account typically is the main business partner for Flomta OÜ. Account will 
combine multiple [Companies](models.md#company) which are the main business partners for that Account. 

### AccountManager
AccountManager is an [User](models.md#user) who has been granted the account-administrative permissions on one 
[Account](/models.md#Aaccount)

### Company

Company is the secondary business unit following the [Account](models.md#Account). A company typically means one 
apartment association managing one or multiple [Buildings](models.md#building). A company is the primary business unit 
for one [Account](/models.md#Account). Company has [Company admins](models.md#UserHasCompany), who can receive the 
[Notifications](models.md#notification) for the [reports](models.md#report) containing the [period](models.md#period) 
[readings](models.md#reading). 

### Building

### Apartment

### Meter

### Period

### Reading

### Report

### Notification

### User

### UserHasCompany
