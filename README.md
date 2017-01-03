# DN! Video API

This video API allows your HTPC to query for Democracy Now! videos to be played back without having to wait for some script to parse the videos.


## Archetecture

The service will run on AWS Lambda and have two end points.

##### GET `/videos`

This end point will return the videos queried for.

Parameters:

```
  n_months    - number of Months since the current month.
  n_years     - eg 1
  start_year  - eg 2017
  start_month - eg 12
  end_year    - [optional]
  end_month   - [optional]
  show_extras - true if you want to see non-official vids
```



##### POST `/scrape`

This will read from democracynow.org and determine if any new videos have been added.  This script only needs to be run once a day.  It will write to a DB.

Parameters:

```
  n_weeks     - Number of weeks to 'dig up' since the current date
  n_months    - Number of months to 'dig up' since the current date
```


## Deploy

##### Setup Database

```
  mysql -h RDSEndPointAddress -P 3306 -u username -p databasename < PathTORDSdatabaseSchema.sql
```

##### Conduct Initial Scrape


##### Setup a cron job

A cronjob should run the scrape script once a day.

