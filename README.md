# frictionless-usecases

These are use-cases using datasets submitted to the Biological and Chemical Oceanography Data Managment Office (BCO-DMO) https://www.bco-dmo.org

## Usecase structure

Folder strucutre:

	usecases/
		<usecase_name>/
			README.md - use case documentation
			orig/  - original files submitted to BCO-DMO
			<v#>/ - data version number
			  README.md - notes specific to processing of this data version
			  staging/ - if preprocessing was needed before fricitonless tools, files go here.
			  processing/ - any scripts or pipeline-specs used for data processing
			  output/ - data files returned after processsing.  This is considered to be the data version.

## Terms of Use

All data sets are licensed under a Creative Commons Attribution 4.0 International License (CC BY 4). If you wish to use a data set, it is highly recommended that you contact the original principal investigator(s) (PI) listed on the associated BCO-DMO dataset landing page. Should the relevant PI be unavailable, please contact BCO-DMO (info@bco-dmo.org) for additional guidance. For general guidance please see the [BCO-DMO Terms of Use](https://www.bco-dmo.org/terms-use) document. 

Code is licensed under MIT license.  See [LICENSE](LICENSE).

# Data Processing: Frictionlessdata #

## Project Goals ##

1. To make it easier for BCO-DMO Data Managers to assess and perform the necessary data management on data submissions
2. To record provenance of all data processing steps from original submission to archived version.

## Strategic Actions ##

### Process Efficiency for BCO-DMO Data Managers ###

Current data management activities at BCO-DMO are tedious and time consuming to perform. Part of this problem is not being able to see immediate results for a specific action. To quickly correct any mistakes or change a course of action. A lot of the tasks that are required are often re-used on other datasets,  but it's difficult to save a pattern of processing for reuse. In using Frictionlessdata, we propose to: 

1. Create a UI to build a pipleline of processing steps,
   - to assess a data file before starting a pipeline,
   - for constructing a pipeline to help visualize the transforms of each processing step,
   - to abstract common patterns, or groups of processing steps, that commonly occur but require a sequence of multiple steps (e.g. renaming a column),
    
2. Create a UI to manage dataset-specific metadata for inclusion in the datapackage.json
   - could this be a re-purpose of [create.frictionlessdata.io](https://create.frictionlessdata.io)?
   - includes summary statistics of certain dataset columns (e.g. species name),
   - manage metadata about file's columns (parameters) (e.g. controlled-vocabulary term, units, finer detail about data type, etc.)
   - add metadata about instruments used in collection
   - manage authorship and other person roles
   - selecting from lists of related awards and projects
   - creating/selecting associated deployments (e.g. cruises, etc)
   - adding/selecting related publications
   - adding/selecting supplemental documentation (as reources to the datapackage?)

### Recording Provenance ###

Declarative workflows provide a capability to interpret processing steps as provenance records of data transforms. THis valudable information will help BCO-DMO bridge original data file submissions to the archived versions in the repository and national archive. This provenance communicates to the data authors what was done to a dataset in a reproducible way, but also helps BCO-DMO track what processing steps were performed per dataset in case of bugs, errors that would require further action. in using Frictionlessdata, we propose to:

1. convert the `pipeline-spec.yaml` into a provenance record, using the PROV data model, encoded as RDF via PROV-O.
   - see [Towards capturing data curation provenance using Frictionless Data Package Pipelines [poster]](https://darchive.mblwhoilibrary.org/handle/1912/10631)

