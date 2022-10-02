# UBC PAIR Grade Data

This repo contains CSV data of grade distribution data from UBC PAIR for each campus, each year session, and each course code.

Data Source | Last Updated
--- | ---
[PAIR Reports](https://webprd01.pair.ubc.ca/reports/welcome.action) | June 2019
[Tableau Dashboard](https://reports.im.it.ubc.ca/#/site/Learner/views/GradeDistributionReport/GradeDistributionReport?:iid=1) | September 2022
[Tableau Dashboard v2](http://reports.im.it.ubc.ca/t/PAIR/views/GradesDistribution/GradesDistribution) | September 2022

## Description
### PAIR Reports (? - 2022)

The data from PAIR Reports should only be relevant for grade data of around 2016W or earlier. This is because grade data from 2017W was found to be modified in the timeframe between June 2019 and Dec 2019. Only data for UBC Vancouver was taken.

The PAIR Reports represent **raw** data taken from the dashboard contained these distinctions:
  - Number of students that audited the course
  - Number of students that completed the course outside any of the above three categories
  - Precision of grade averages and standard deviations of two decimal places
  - A grade category representing the number of fails as `<50`
  - `OVERALL` sections for courses with a populated `DETAIL` field do not have that field populated.

Other considerations for this data include:
  - Certain rows are duplicated by everything except for the `Professor` column. Most of the time there one field will be empty and the other will be populated. In a few cases, all Professor columns will be non-empty and contain different entries. My solution to this was manually looking up the section info from PAIR and adjusting the section as necessary. See the `extras` folder.
    - An exception to this is `UBC-2007W-DENT-420-PSI` whose row is simply duplicated with no changes.
  - `OVERALL` sections are generated based on the course code for the year. As such there will be numerous `OVERALL` rows if a course has a populated detail field.

### Tableau Dashboard (2019 - 2022)

The new Tableau dashboard has these distinctions:
  - Additional privacy for the data, resulting in null entries for any class sections or grade letters that had fewer than 6 entries.
    - For this reason if fewer than 6 people failed a course it is not possible to get the failure/passing rate for a section.
    - Additionally, for some sections only `OVERALL` sections are available where there is no data given for each grade category.
    - Where possible, missing grade entries are filled.
      - Using `High` and `Low`, zeroes are filled where it's not possible for a student to be earn a grade in that category.
      - If the number of grade entries matches the `Enrolled`, zeros are filled for all other grade categories.
      - If only one entry is missing among all the grade categories for one section, the missing value can be computed by subtracting the populated grade entries from the total enrolment. This is also applied across sections, if only one section and one grade entry is missing across multiple sections. The missing grade entry is computed by subtracting the populated grade entry for a particular grade category from the grade entry of the `OVERALL` section. This assumes that the `Enrolled` field is the sum of the students that received a grade in each grade category.
    - This change does not appear for all yearsessions as sometime in 2020, grade letters that had fewer than 6 entries were visible.
  - Higher precision of grade averages and standard deviations to nine decimal places.
  - The campus code `UBC` has been changed to `UBCV`.
  - The course title fields are populated with its full title rather than a capitalized shorthand, as one might see on the SSC.
  - The `Professor` field includes names of Teaching Assistants where available.
  - The `Enrolled` field excludes students that withdrew or audited the course.

### Tableau Dashboard v2 (2022 - ?)

These are new observed changes compared to the previous Tableau Dashboard:
  - Removal of `OVERALL` sections.
  - Removal of the standard deviation statistic
  - Addition of 25th and 75th percentile, and median statistic
  - Re-enforcement of grade entry removals for letter grades with fewer than 6 entries
  - The `Professor` field no longer includes names of Teaching Assistants
  - The field `Enrolled` has been renamed/changed to `Reported` for more clarity.
  - Lower precision of grade averages and statistics to just one decimal place.

Similar to before, missing grade entries are filled where possible.