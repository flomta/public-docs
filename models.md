# Flomta entities

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
consumption. A Meter always belongs to an [Apartment](models.md#apartment). Some meters can refer to specific 
[Building](models.md#building) main input meters (_is_main_) measuring the whole building. Also in such case an 
Apartment is needed (eg "main") to be related to. A meter always belongs to a [device](models.md#device).

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

One physical Meter can contain readings data for multiple physical [Mediums](models.md#medium). Eg cold AND hot water. Daily AND nightly 
electricity. And or combinations of multiple Mediums, eg 2 waters + heat etc. In such case each Medium is #mapped# as 
separate "logical" Meter. Logical meters share the same serial identification number, the logical distinction is done
via _position_ and _position_name_. Typically, there could be up to 4 positions in a data record. 

In general Meter's serial number is not globally unique. It is only unique in one building context.  

The identification of how to decode relevant data from a raw device data is done based on:
- [device type](models.md#device-type): specifying the general data format (bin/CSV/xml). Determining how to read raw data records from a file.
- CURRENTLY: parsed based on the record profile
- FUTURE (needs implementing): based on pre-defined [Record Type](models.md#record-type)

### Meter Model

Meter model describes an instance of one [Medium](models.md#medium) measuring for one [Account](models.md#account). An 
account could also have multiple instances of Meter Models for _one_ Medium. Eg "cold water kitchen", "cold water 
bathroom" etc. The Meter Models are defined on Account level. 

### Period

Flomta deals with time-series data for [readings](models.md#reading). Each [reading](models.md#reading) has a Period.
Currently, a Period means a monthly time-frame. Readings of _one_ period and _one_ [Device](models.md#device)
are aggregated into a [Report](models.md#report). 

Readings of a Period are typically done by [Devices](models.md#device) on the last or first days of a period (month). 
Flomta will regard the data stamped before 20th day of month as "previous month's data" and data stamped after 
20th dat of month as "current/latest months data". 

### Readings File

Readings File entity describes the actual physical file delivered by the [Device](models.md#device) containing the
[meter's](models.md#meter) initial raw data of [readings](models.md#reading). Readings file is always linked to a
[Device](models.md#device) and a [period](models.md#period). 

Flomta will store the status of the file, the initial processing timestamp as well as a reference of the path of the 
actual file in the FileStorage where the files are stored for archiving purposes. 

Typically, one [Device](models.md#device) will deliver _multiple_ Readings Files for one [period](models.md#period) for 
processing. It is common for the first files to miss some data for a selection of [meters](models.md#meter) and the 
later files have additional data frames on the [meters](models.md#meter) missed in first files. 

### Readings File Import

Readings File Import refers to _one_ attempted rea/import of one [Readings File](models.md#readings-file). Any
[Readings File](models.md#readings-file) might be tried for processing multiple times. 

Readings File Import wil store the timestamp and the number of various records included in the reading process eg: 
- total records in the file
- valid records
- calculated records
- duplicate records
- failed records

### Reading

A Reading refers to the data from _one_ (logical) [Meter](models.md#meter) for _one_ [period](models.md#period). Reading 
stores the reported _value_ of the [Meter](models.md#meter) and _consumption_ which is the difference of two sequential
[period](models.md#period) reading values. 

Reading can be also calculated (if missing) or adjusted manually, see [Reading Type](models.md#reading-type). 

Reading stores the initial raw data data record as hexData or json (csv, xml), as well as the 
[Record Type](models.md#record-type) at the time of reading (since it might change over time).

A reading might need human attention (_needs_attention_) if some #logical checks# fail. 

### Reading Type

Reading can be a) actual b) calculated or c) manual. 

Most of the readings typically are "actual" which are tha actual values delivered by the [Device](models.md#device) and the
[Readings File](models.md#readings-file). In some cases the actual data for a [Meter](models.md#meter) is missing. A missing 
data could be a result of a failure in the physical meter or the radio signals delivering the data between a meter and a
[Device](models.md#device) or various other reasons. 

In many cases if the missing reading is temporary, the missing value of the meter at that point of time could be 
calculated using the context information (eg previous readings from the same meter, data from similar meters etc.).

In such distinct cases the reading value will be calculated and the reading is flagged with a "calculated" type flag. 

In some rare cases the actual or calculated reading needs to be adjusted manually. After the manual calculation, the 
reading type will be referred as "manual". 

### Report

A Report is a main reportable entity to the end users. A report aggregates _one_ [Building](models.md#building) reportable 
data [Device](models.md#device)

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


