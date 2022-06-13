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

A Company can be deactivated (_status_id_). Deactivated Company will not be processed for new data or notifications etc.

### Building

Building typically represents one physical building containing a [central collecting device](models.md#device) and 
multiple [Apartments](models.md#apartment). 

Building belongs to one [Company](models.md#company).

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

Apartment belongs to one [Building](models.md#building). Apartment has [Meters](models.md#meter). 

### Meter

Meter refers to the main remote devices that actually do the physical data measurement of [Medium](models.md#medium) 
consumption. A Meter always belongs to an [Apartment](models.md#apartment). Some meters can refer to specific building
main input meters (_is_main_) measuring the whole building. Also in such case an Apartment is needed (eg "main") to be 
related to. A meter always belongs to a [device](models.md#device).

A main meter can be used for further analysis (eg comparison to individual meter's consumption aggregated sum). 

A meter (eg main) can be connected to an external API for communicating with a [Medium](models.md#medium)
[Provider](models.md#provider) ([API](models.md#provider-api) or e-mail) delivering provider 
[Notification](models.md#notification) data to external systems. 

A Meter can sometimes be installed (by accident) backwards (_is_flipped_). 

A meter can be deactivated (_active_).

The raw medium Readings data will be processed and stored in Flomta as [readings](models.md#reading).

A meter reads one value stream ([readings](models.md#reading)) and has an _initial_value_ defined as calculations
starting point.

Meter's Medium is defined by a [Meter model](models.md#meter-model).

One physical Meter can contain readings data for multiple physical mediums. Eg cold AND hot water. Daily AND nightly 
electricity. And or combinations of multiple Mediums, eg 2 waters + heat etc. In such case each Medium is #mapped# as 
separate "logical" Meter. Logical meters share the same serial identification number, the logical distinction is done
via _position_ and _position_name_. 

In general Meter's serial number is not globally unique. It is only unique in one building context.  

The identification of how to decode relevant data from raw device data is done based on:
- [device type](models.md#device-type): specifying the general data format (bin/CSV/xml)
- CURRENTLY: parsed based on the record profile
- FUTURE (needs implementing): based on pre-defined [Record Type](models.md#record-type)

### Meter Model

Meter model describes an instance of one [Medium](models.md#medium) measuring for one [Account](models.md#account). An 
account could also have multiple instances of Meter Models for _one_ Medium. Eg "cold water kitchen", "cold water 
bathroom" etc. The Meter Models are defined on Account level. 

### Period

### Reading

### Report

### Collector

### Notification

### User

### UserHasCompany

### Medium

Mediums refer to M-bus standard medium typology 8.4.1

https://m-bus.com/documentation-wired/08-appendix

### Provider

### Provider API

### Record Type


