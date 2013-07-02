# St. Paul Councilmatic

An instance of [Councilmatic](https://github.com/codeforamerica/councilmatic), a subscription service for city council legislative information, started in Philadelphia, for St. Paul.  Based on code for the [Philly instance](https://github.com/mjumbewu/philly-councilmatic).

## Issues

This is not currently working as the [scraper](https://github.com/fgregg/legistar-scrape) is not working for the [St. Paul Legistar site](http://stpaul.legistar.com/Legislation.aspx) (advanced search).


## Install

1. (optional) Create a Virtualenv
1. `pip install -r requirements.txt`
1. Create a PostGIS database called 'councilmatic'. Refer to the [GeoDjango documentation](https://docs.djangoproject.com/en/dev/ref/contrib/gis/install/postgis/) or other PostGIS documentation for instructions.
1. Create log directory: `mkdir website/logs`

### Configure

1. `cp website/local_settings.py.template website/local_settings.py`
1. Configure `local_settings.py` with your database.  The LEGISLATION configuration for St. Paul should be included.

### Setup

	python website/manage.py syncdb
	python website/manage.py migrate

If you chose to create a superuser during the `syncdb` command, you should now create a subscriber for that superuser. A subscriber could not be created until the subscriptions app's database tables were set up, and that didn't happen until the `migrate` command. Now that the subscription app is ready, sync the subscriber objects:

	python website/manage.py syncsubscribers

Now you should be able to run the site:

	python website/manage.py runserver
	
### Load data

1. `python website/manage.py loadlegfiles` (maybe)
1. `python website/manage.py updatelegfiles`
1. `python website/manage.py update_index`