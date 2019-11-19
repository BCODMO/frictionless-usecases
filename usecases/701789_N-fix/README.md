# Usecase 701789_N-fix

For metadata for this dataset see: https://www.bco-dmo.org/dataset/701789

# Original data

The [orig](orig) folder contains the original excel file submitted to BCO-DMO.

# Data processing needs:

* convert lat/lon to decimal degrees
* add timestamp (UTC) in ISO format
* data with value "surface" in collection depth column should be changed to 0
