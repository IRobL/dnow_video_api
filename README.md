# DN! Video API

This video API allows your HTPC to query for Democracy Now! videos to be played back without having to wait for some script to parse the videos.


## Archetecture

The service will run on AWS Lambda and have two end points.

##### GET `/videos`

This end point will return the videos queried for.

Parameters:

```
  n_shows     - number of shows since specified date
  start_show - eg show id/ show title, if you say n_show=1&start_show=boy%20and%20blob, youll get the show after "boy and blob"

  start_year  - eg 2017
  start_month - eg 12
  n_months    - number of Months since the current month.
  n_years     - eg 1
  end_year    - [optional]
  end_month   - [optional]
  show_extras - true if you want to see non-official vids
  act         - Your account token, which enables tracking what you've seen (see tracker)
```



##### POST `/scrape`

This will read from democracynow.org and determine if any new videos have been added.  This script only needs to be run once a day.  It will write to a DB.

Parameters:

```
  n_weeks     - Number of weeks to 'dig up' since the current date
  n_months    - Number of months to 'dig up' since the current date
```


##### GET `/account`



##### GET `/account/subscriptions`

Returns all the shows you're subscribing to, and the date of the last show, it's id, and it's title, and also the show that probably succeeds that show.


##### POST `/account/subscriptions`

Parameters:
```
  media_access_api      - link to /videos that follows the convention of the core API for DN! I'm building.
                          The app will be able to use the parser to
```


##### GET `/account/subscriptions/:id`


##### DELETE `/account/subscriptions/:id`



## Deploy

##### Setup Database

```
  mysql -h RDSEndPointAddress -P 3306 -u username -p databasename < PathTORDSdatabaseSchema.sql
```

##### Conduct Initial Scrape


##### Setup a cron job

A cronjob should run the scrape script once a day.

