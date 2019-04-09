# Usecase 752613_Temperature

Metadata for dataset available on the BCO-DMO dataset landing page: https://www.bco-dmo.org/dataset/752613

## Original file(s)

Processing needs:

* unpivot (temperature columns)
* join (with sites.csv to get lat/lons)
* date time in ISO (UTC) needed to be added in addition to format provided
* degrees decimal minutes needed to be converted to decimal degrees
* Rename columns

## Data Souces

orig/Field_Temperature_Data_set1.txt

## v1/

Souce data files used for pipeline:

staging/
* sites.csv (was constructed from text in the DATASET metdata form. Column names renamed by hand)
* temp.csv - edited version of  orig/Field_Temperature_Data_set1.txt

pipeline rand with dpp:
	v1/processing/pipeline-spec.yaml

output file(s): 

output/

* temp.csv  (this will be BCO-DMO dataset 752613)
* sites.csv
* datapackage.json
