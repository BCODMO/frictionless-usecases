# Usecase 786028_abund

Metadata for dataset available on the BCO-DMO dataset landing page: https://www.bco-dmo.org/dataset/786028

## Original file(s)

[orig/Pvent_P&S_135_supptable1_submit.xlsx](orig/Pvent_P&S_135_supptable1_submit.xlsx)

![image](https://user-images.githubusercontent.com/9537357/71844991-602c5580-3095-11ea-899f-ebed7a1eb410.png)

## data version 1

The folder [v1/unpivoted](v1/unpivoted) contains the output from a pipeline corresponding to data version 1 of this dataset.
* pipeline-spec.yaml
* datapackage.json
* epr.csv

Unpivots the dataset to transform it from having multiple header rows containing data into having all data in columns with one set of field names.

epr.csv displayed in Laminar

![image](https://user-images.githubusercontent.com/9537357/71844157-8bae4080-3093-11ea-80e6-810f0f615f1c.png)


## data version 2

TBD. Needs all processing steps from data version 1 in addition to joining with another data source to get specied identifiers into the dataset.  

This pipeline uses custom pipeline processors found in the github repo https://github.com/BCODMO/bcodmo_processors.
