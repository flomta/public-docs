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

Building typically represents one physical building containing a [central collecting device](models.md#device) and multiple 
[Apartments](models.md#apartment). 

### Device

Device refers to a central data collection unit for one [Building](models.md#building) that collects the 
[Readings](models.md#reading) data for individual remote [Meters](models.md#meter) and transfers the data into Flomta
application via a [Collector](models.md#collector). Devices can be of multiple [types](models.md#device-type). The 
[device type](models.md#device-type) is configured to an individual Device via [device models](models.md#device-model). 

### Device Type

Device type separates various physical input data types. mainly the type indicates the primary file format difference
the data is provided by a [device](models.md#device) for external processing. The main types are:

- Sontex INI - containing raw binary data frames with hex data bytes
- CSV
- XML

### Device Model

Device Model describes the [Account](models.md#account) specific instances of [device types](models.md#device-type). Not 
all Accounts make use of all device Types. A device Model configures one Device Type for usage in one Account. 

### Apartment



### Meter

### Period

### Reading

### Report

### Collector

### Notification

### User

### UserHasCompany
