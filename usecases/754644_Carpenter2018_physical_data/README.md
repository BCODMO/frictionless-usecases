# Usecase 754644_Carpenter2018_physical_data

Metadata for dataset available on the BCO-DMO dataset landing page: https://www.bco-dmo.org/dataset/754644

## Original file(s)

Processing needs:

* load sheet from excel file
* add missing data identifier "NA"
* make character replacements in column names
* have decimal places & date the same as formatted in the Excel file
* Add Date column in ISO 8601 format yyyy-MM-dd in addition to original date column.
* set types

## Data Souces

[orig/Carpenter et al. 2018_data.xlsx](orig/Carpenter%20et%20al.%202018_data.xlsx)
* sheet "physical data"

There are other sheets in this file, each correspond to a different dataset at BCO-DMO.

## Issues encountered when using dataflows and pipelines

### Can't import field formats with the values from Excel

https://github.com/BCODMO/frictionless-usecases/issues/5

### Error on load because missingValues not set yet when using (force_strings=False)

https://github.com/BCODMO/frictionless-usecases/issues/6

### Set types on column name with () causes error

https://github.com/BCODMO/frictionless-usecases/issues/9
