# UBC PAIR Grade Data

This repo contains CSV data of grade distrubution data from UBC PAIR for each campus, each year session, and each course code.

Data Source | Last Updated
--- | ---
PAIR Reports | June 2019
Tableau Dashboard | Dec 2019

There are two main sources for the data. The first (now deprecated) source was from the old PAIR Reports dashboard located [here](https://webprd01.pair.ubc.ca/reports/welcome.action). This tool was removed in the summer of 2019 in favor of a Tabluea dashboard found [here](http://pair.ubc.ca/student-performance/grades-distribution/) (the UBC VPN is needed to access), serving as the second source.

## Differences
The PAIR Reports represent RAW data taken from the dashboard contained these distinctions:
  - Number of students that audited the course
  - Number of students that completed the course outside any of the above three categories
  - Precision of grade averages and standard deviations of two decimal places
  - A grade category representing the number of fails as `<50`
  - `OVERALL` sections for courses with a populated `DETAIL` field do not have that field populated.
  
The new Tableau dashboard has these distinctions:
  - Additional privacy for the data, resulting in null entries for any class sections or grade letters that had fewer than 6 entires.
    - For this reason if fewer than 6 people failed a course it is not possible to get the failure/passing rate for a section.
    - Where possible, missing grade entries are filled. For example, if only one entry is missing among all the grade categories for one section, the missing value can be computed by subtracting the populated grade entries from the total enrolment. This is also applied across sections, if only one section and one grade entry is missing across mutiple sections. The missing grade entry is computed by subtracting the populated grade entry for a particular grade category from the grade entry of the `OVERALL` section.
  - Higher precision of grade averages and standard deviations to nine decimal places.
  - The campus code `UBC` has been changed to `UBCV`.
  - The course title fields are populated with its full title rather than an capitalized shorthand, as one might see on the SSC.
  - The `Professor` field includes names of Teaching Assistants where available.
 
These differences are reflected in the data.

## PAIR Reports Data

The data from PAIR Reports should only be relevant for grade data of around 2016W or earlier. This is because grade data from 2017W was found to be modified in the timeframe between June 2019 and Dec 2019. Only data for UBC Vancouver was taken.

Other considerations for this data include: 

  - Certain rows are duplicated by everything except for the `Professor` column. Most of the time there one field will be empty and the other will be populated. In a few cases, all Professor columns will be non-empty and contain different entries. My solution to this was manually looking up the section info from PAIR and adjusting the section as necessary.
    - An exeption to this is `UBC-2007W-DENT-420-PSI` whose row is simply duplicated with no changes.
  - `OVERALL` sections are generated on the basis of the course code for the year. As such there will be numerous `OVERALL` rows if a course has a populated detail field.
