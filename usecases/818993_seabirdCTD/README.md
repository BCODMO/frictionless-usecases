Files in orig/head are truncated seabird ctd data files.  The .csv file is the same data as the .cnv file but converted to tabular csv data with the first line being a header line.  

The .cnv file is a Seabird fixed-width formatted file (see seasave v7 software manual https://www.seabird.com/asset-get.download.jsa?code=251445)

The original submission to BCO-DMO contained the data in both formats.

We need to perform a validation check for field names on these (see  https://github.com/BCODMO/laminar_web/issues/801).