# Aircraft Data

Collection of data files that can be used by applications that need detailed configuration and datum information about gliders. 

## Installation

```sh
npm install @cael-aero/aircraft-data --save
yarn add @cael-aero/aircraft-data
bower install @cael-aero/aircraft-data --save
```                                      

## Format

Files are in either standard CSV format or JSON files for complex structured data. Dates are ISO6801, without timestamps. No 
timezone is defined, because it is irrelevant to the data being described. The dates are to confirm which doc was read
from the items in the aircraft logbook, or when this was last updated.

### Type Certificate Name Handling

Each line has a primary key (first column) based on the type certificate name. These have been standardised somewhat to make them
easily reproducible. Note that there may be multiple entries for an aircraft type, with each matching the TCDS name. For example,
there's a DG300 and DG300 ELAN as separate rows, since these are types that will separately appear on the TCDS and also any local
registry certificate of airworthiness or Type Acceptance Certificate. Often the original importers are not very careful in what is
written into those fields, but we don't intend to handle all the variations. To generate the ID the following rules are applied 
to the raw name that is often found in data files from CASA or the GFA. 

1. Convert all characters to upper case
2. Remove the following punctuation characters: ' ', '-', '_', '.', '/', '\\', '"', '''

## Data Available 

| Type of data | Source File | Description of file format |
|----|----|----|
| Weight and Balance Datum | [weight-and-balance-datum.csv](data/weight-and-balance-datum.csv) | [Definition](docs/datum.md)|
| Aircraft Configuration | [aircraft-configuration.csv](data/aircraft-configuration.csv)| [Definition](docs/aircraft-config.md)|
| Aircraft Limits | | [Definition](docs/aircraft-limits.md)|
| References | [reference-data.json](data/reference-data.json) | [Definition](docs/reference-data.md) |

## Data Validity

This data has been collected and verified to the best of our ability. Where possible we will list the source of the datum information
so that you can double check. There core data is typically found in the Type Certifcate Data Sheet. However, the more esoteric data,
such as tail ballast arms are usually found from less trustworthy sources - such as individual club/NAA sheets. The British Gliding
Association has a pretty extensive collection, as well as some from Gliding Australia. Were we can verify these, it will be labelled
as such. Some you may need to re-validate yourself. 

## Updating Data

If you have data that you'd like to submit to the repository, or corrections to data, please use the Ticket creation button here
and provide as much relevant information as possible. Please cite the source of your data as part of the ticket. If you're more
technically savvy, happy to take a PR with the ticket. 
 
## License

This source code is licensed under the BSD-style license found in the
LICENSE file in the root directory of this source tree. 

## Related Projects

Weight and Balance Calculation Library: https://github.com/CAELAero/weight-and-balance This also contains
loaders, exporters and Javascript/Typescript objects that represent the data files contained in this
repository.
