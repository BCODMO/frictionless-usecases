## Usecase water_column_particle_profiles

These datasets are in the process of being served at bco-dmo.org.  Full documentation of originally submitted format, and processing steps pending on these pages.

## originally submitted file

[orig/Elementa Aggregate Data.xlsx](Elementa Aggregate Data.xlsx)


## preprocessed data

[preprocessed/profile_info.xlsx](preprocessed/profile_info.xlsx)
[preprocessed/elementa.xlsx](preprocessed/elementa.xlsx)
* sheet: particles per liter
* sheet: ghost colonies

General processing description:
* Sheets in Elementa Aggregate Data.xlsx extracted as individual tabular resources in elementa.xlsx.  Some sheets actually had two separate tables in one sheet, one for marine snow particles and one for Phaeocystis ghost colonies together in one sheet.  Two independant tabular datasets created, one for ghost colonies, one for marine snow.
* profile_info.xlsx - date/time/location formatting cleaned, missing values filled in from correspondence with PI.
* There was no way to join the data sources so added "Profile_ID" columns so marine snow and ghost colony data could be joined to profile_info.

## data version 1 

v1 data are clean and will be posted on pages:
* https://www.bco-dmo.org/dataset/719478
* https://www.bco-dmo.org/dataset/768570

[v1/ghost_colonies.csv](v1/ghost_colonies.csv)
[v1/marine_snow.csv](v1/marine_snow.csv)

General processing summary: 
* Online pipeline tool used to join particle data to profile_info.  
* Added ISO_DateTime_UTC.
* lat|lon formatting fixed and converted to decimal degrees.

## data version 2

Processing need:
* Combine v1/ghost_colonies.csv and v1/marine_snow.csv. Do equivalent of a full outer join on with these two tabular datasets so that each row corresponds to the depth in a profile and has both the marine snow and ghost colony data. v1 data are clean and described on landing pages, they just need to be combined.
    * Join on Canister,depth
    * The results should have null values in "ghost colony" columns where there there were no matching Canister,depth in ghost_colonies.csv.  There should be null values in "marine snow" columns where there were no matching Canister,depth columns in marine_snow.csv

