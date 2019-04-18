# Usecase 746395_PierCTD

For metadata for this dataset see: https://www.bco-dmo.org/dataset/746395

# Original data
The originally submitted file is [orig/SantaMonicaPier_April_2018_CTD_data.csv](orig/SantaMonicaPier_April_2018_CTD_data.csv)

# Data processing

Changes made to create  [v1/CTD.csv](v1/CTD.csv):
* used find and replace to correct inconsistant time format h changed to hh.
* Added ISO timestamp in UTC in addition to local Date and Time columns, maintaining original format.
* Added lat/lon from other metadata.  One location for deployment at the pier (34.00765,-118.50015).

