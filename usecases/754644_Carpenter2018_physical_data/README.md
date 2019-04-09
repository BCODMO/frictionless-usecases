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

### Can't get format from Excel, just values

Excerpt from internal notes: https://github.com/BCODMO/pipeline-web/issues/52

We need to use the same formatting that is in the Excel file.  The behaviour if you use "Save as" csv in Excel is to output the values with formats as they are displayed in the Excel program.  We want the same formatting shown below. **minus the extra blank columns

![image](https://user-images.githubusercontent.com/9537357/55420656-87258c00-5545-11e9-966d-9adea6d61e4e.png)

Excel "Save as"->csv gives you this:

```
Date,Treatment days,Treatment,Flume,Temperature (24h),Temperature (day),Temperature (night),Irrandiance,,,,
13-Nov,-4,344,3,27.78,28.48,27.28,NA,,,,
14-Nov,-3,344,3,27.59,27.99,27.19,34.74,,,,
15-Nov,-2,344,3,27.37,27.42,27.31,25.14,,,,
16-Nov,-1,344,3,27.47,27.76,27.18,25.03,,,,
17-Nov,1,344,3,27.67,28.10,27.24,33.26,,,,
18-Nov,2,344,3,27.61,27.88,27.33,25.23,,,,
19-Nov,3,344,3,27.68,28.10,27.26,31.65,,,,
```

This was the closest I could get when using pipelines:

```
Date,Treatment days,Treatment,Flume,Temperature (24h),Temperature (day),Temperature (night),Irrandiance
2015-11-13T00:00:00,-4,344,3,27.7810833333333,28.4814,27.2808571428571,NA
2015-11-14T00:00:00,-3,344,3,27.5885833333333,27.9920833333333,27.1850833333333,34.74306
2015-11-15T00:00:00,-2,344,3,27.3660416666667,27.4173333333333,27.31475,25.14186
2015-11-16T00:00:00,-1,344,3,27.4698333333333,27.7567916666667,27.182875,25.03278
2015-11-17T00:00:00,1,344,3,27.6653958333333,28.0955833333333,27.2352083333333,33.25788
```
* From this we would have to figure out what format was used in Excel manually and add steps in the pipeline to format/round the values back to that.
* At this point, "Date" is still a string, but it stuck in the format for DateTime not Date upon load.

using pipeline load with parameters:

```
    parameters:
      force_strings: true
      format: xlsx
      from: https://github.com/BCODMO/frictionless-usecases/blob/master/usecases/754644_Carpenter2018_physical_data/orig/Carpenter%20et%20al.%202018_data.xlsx?raw=true
      headers: 1
      name: physical
      sheet: physical data
      skip_rows: []
      validate: true
```

It would be great if the user could have an option to load with the specified formats in the excel file.  That way:

* load_with_format=True would give like "27.78"  "13-Nov"
* load_with_format=False would give the value "27.7810833333333"  and a default date format like 2015-11-13.  You can't get around that you have to have a default format in the case of date since I assume whatever encoding of dates in excel doesn't make sense outside of Excel.

This challenge does not seem unique to frictionless.  I have also incountered similar setbacks with formatting on import when using read_excel in pandas. The formatting set in Excel is not imported with the data values.  I try playing around with settings to achieve the equivalent of Excel csv export with dtypes=objects (to do something similar to force_strings=True) and parse_dates=False.  But it still requires the user to go back to the original excel file, figure out what the formatting is, and then apply it to the colums in your data frame.


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
