# Data Reference

File used to describe where each of the data items in there other files here can be found.

## File Format

JSON file where the top level field names are the type certificate ID that is referenced in
the other files as their primary key. The value of each key is an object with multiple fields
as described below.

| Field name | Field Type | Description |
|----|----|----|
| References | Array of strings | Refers to another typecertificate ID that has the description of the data for this type certification. Often used where multiple subvariants all have exactly the same details, or primarily the same details. This can co-exist with the existance of the other fields. |
| TCDS | Object | Details about the Type Certificate Data Sheet for this type certificate |
| FlightMannual | Object | Details about the flight manual |
| AMM | Object | Details about the Aircraft Maintenance Manual |
| RepairManual | Object | Details about the repair manual | 
| OtherData | Object | Details about other supplementary data documentation - typically the BGA data sheet that has data no found elsewhere |
| Unverified | Array of strings | List of the datum fields that we have values for but cannot be verified from other sources |
| Measured | Array of objects | List of datum fields that are populated by directly measured values off specific aircraft | 

### TCDS Object 

| Field name | Field Type | Description |
|----|----|----|
| Authority | enum | Name of the NAA that hold the type certificate, typically EASA or LBA |
| URL | URL string | Location on the internet of the TCDS file |
| Provides | Array of strings | Names of each of the datum data fields that can be found in this doc |

### Flight Manual Object 

| Field name | Field Type | Description |
|----|----|----|
| URL | URL string | Location on the internet of the flight manual file |
| Provides | Array of strings | Names of each of the datum data fields that can be found in this doc |

### AMM Object 

| Field name | Field Type | Description |
|----|----|----|
| URL | URL string | Location on the internet of the maintenance/service manual file |
| Provides | Array of strings | Names of each of the datum data fields that can be found in this doc |

### Repair Manual Object 

| Field name | Field Type | Description |
|----|----|----|
| URL | URL string | Location on the internet of the repair manual file |

### Other Data Object 

| Field name | Field Type | Description |
|----|----|----|
| URL | URL string | Location on the internet of the file containing other reference data |
| Provides | Array of strings | Names of each of the datum data fields that can be found in this doc |

### Measured Data Object

| Field name | Field Type | Description |
|----|----|----|
| arms | Array of strings | Names of each of the datum arm length fields that were measured |
| source | string | Registration of the aircraft this data was sourced from |
| date | ISO date string | Date of the manual entry for the aircraft that the data was sourced from | 

