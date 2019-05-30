## Usecase water_column_particle_profiles

These datasets are in the process of being served at bco-dmo.org.  Full documentation of originally submitted format, and processing steps pending.

## originally submitted file

orig/"Elementa Aggregate Data.xlsx"

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

General processing summary: 
* Online pipeline tool used to join particle data to profile_info.  Note: there is a lot of find and replace to deal with date|time issues.  These pipelines were originally developed before the new preserve_format option was available in datapackage-pipelines and so the pipelines could be streamlined now that that is available.
* Added ISO_DateTime_UTC.
* lat|lon formatting fixed and converted to decimal degrees.

Pipelines & results:
* Be advised, this uses custom processors.
* [v1/marine_snow](v1/marine_snow) contains the pipeline-spec.yaml datapackage.json and output csvs from the marine snow pipeline.
* [v1/ghost_colonies](v1/ghost_colonies) same as above

CSVs:
* [v1/ghost_colonies/ghost_colonies.csv](v1/ghost_colonies/ghost_colonies.csv)
* [v1/marine_snow/particles_per_liter.csv](v1/marine_snow/particles_per_liter.csv)

v1 data are considered clean and will be posted on pages:
* https://www.bco-dmo.org/dataset/719478
* https://www.bco-dmo.org/dataset/768570

## data version 2

Source files: 
* [v1/ghost_colonies/ghost_colonies.csv](v1/ghost_colonies/ghost_colonies.csv)
* [v1/marine_snow/particles_per_liter.csv](v1/marine_snow/particles_per_liter.csv)


Processing need:
* Combine v1/ghost_colonies.csv and v1/particles_per_liter.csv. Do equivalent of a full outer join on with these two tabular datasets so that each row corresponds to the depth in a profile and has both the marine snow and ghost colony data. v1 data are clean and described on landing pages, they just need to be combined.
    * Join on Profile_ID,depth
    * The results should have null values in "ghost colony" columns where there there were no matching Profile_ID,depth in ghost_colonies.csv.  There should be null values in "marine snow" columns where there were no matching Profile_ID,depth columns in particles_per_liter.csv

Folder [v2/pipeline-spec.yaml](v2/pipeline-spec.yaml) has a pipeline that does a join with datapackage-pipelines optoin Full:True, but it isn't what I would consider a full outer join since it dropped the rows from the ghost colony data (source) where there was no marine snow "particles_per_liter" data (target).
* results of join are in data file [v2/particles_per_liter.csv](v2/particles_per_liter.csv)
* Be advised, this uses custom processors.
