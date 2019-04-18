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

### Error on load because missingValues not set yet when using (force_strings=False)

Attempted using dataflow but abandonded that due to load errors and unsupported date formats when trying to load the data in formats we need.  Can't infer when we haven't added missing data identifiers yet.  I was wondering if it is possible to supply a schema or even just the missingValues to the load processor.

> load(orig_path, name=row.obj_name, validate=False, force_strings=True,sheet=row.sheet_name, strip=True),

    dataflows.base.schema_validator.ValidationError: 
    ROW: {'Date': datetime.datetime(2015, 11, 13, 0, 0), 'Treatment days': -4, 'Treatment': 870, 'Flume': 4, 'Temperature (24h)': 'NA', 'Temperature (day)': 'NA', 'Temperature (night)': 'NA', 'Irrandiance': 'NA'}

### Set types on column name with () causes error

```
    INFO :RESULTS:

    INFO :FAILURE: ./40f79ec8-5575-11e9-ae8b-0242ac110002/missing-data-identifiers-excel

    ERROR log from processor set_types:

    +--------

    | Traceback (most recent call last):

    | File "/usr/local/lib/python3.6/site-packages/datapackage_pipelines/specs/../lib/set_types.py", line 26, in <module>

    | spew_flow(flow(ctx.parameters), ctx)

    | File "/usr/local/lib/python3.6/site-packages/datapackage_pipelines/utilities/flow_utils.py", line 46, in spew_flow

    | datastream = flow.datastream()

    | File "/usr/local/lib/python3.6/site-packages/dataflows/base/flow.py", line 18, in datastream

    | return self._chain(ds)._process()

    | File "/usr/local/lib/python3.6/site-packages/dataflows/base/datastream_processor.py", line 42, in _process

    | datastream = self.source._process()

    | File "/usr/local/lib/python3.6/site-packages/dataflows/base/datastream_processor.py", line 42, in _process

    | datastream = self.source._process()

    | File "/usr/local/lib/python3.6/site-packages/dataflows/base/datastream_processor.py", line 42, in _process

    | datastream = self.source._process()

    | File "/usr/local/lib/python3.6/site-packages/dataflows/base/datastream_processor.py", line 46, in _process

    | self.datapackage = self.process_datapackage(self.datapackage)

    | File "/usr/local/lib/python3.6/site-packages/dataflows/processors/set_type.py", line 37, in process_datapackage

    | assert added, 'Failed to find field {} in schema'.format(self.name)

    | AssertionError: Failed to find field re.compile('^Temperature (24h)$') in schema

```
