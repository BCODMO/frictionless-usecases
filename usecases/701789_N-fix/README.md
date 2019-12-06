# Usecase 701789_N-fix

For metadata for this dataset see: https://www.bco-dmo.org/dataset/701789

# Original data

The [orig](orig) folder contains the original excel file submitted to BCO-DMO.

# Data processing needs:

* convert lat/lon to decimal degrees
* add timestamp (UTC) in ISO format
* data with value "surface" in collection depth column should be changed to 0
* remove parenthesis and units from column names (field descriptions and units captured in metadata).
* remove spaces from column names

# data version 1

folder "v1" contains the frictionless datapackage pipeline file 'pipeline-spec.yaml' along with processed file "nfix.csv" and the "datapackage.json" file which describes nfix.csv


The folder "screenshots" shows various images of the Laminar processing tool and the data before and after processing.
