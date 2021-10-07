# data-512-a1 Data Curation

## Description and Goal
This project collects and analyzes monthly pageviews data of English Wikipedia from two API endpoints from January 1st 2008 to September 30th 2021. The goal of this project is to aqcuire, clean and visualize Wikipedia pageviews data and make sure the work done during this process is fully reproducible by others. 

## API Endpoints
The two API endpoints used for this project are the Legacy Pagecounts API and the Pageviews API. 

- The Legacy Pagecounts API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts), [endpoint](https://wikimedia.org/api/rest_v1/#/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end)) provides access to desktop and mobile traffic data from December 2007 through July 2016.

- The Pageviews API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews), [endpoint](https://wikimedia.org/api/rest_v1/#/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.

Notice that there are two types of devices provided by the Legacy Pagecounts whreas there three provided by the Pageviews API. However, data from the two mobile-type devices in the Pageviews API is combined together during data processing. In addition, the Pageviews API allows us to select only the user traffic (not spiders/crawlers) by setting the agent filter to 'user' but the Legacy Pagecounts API does not. Thus, data from the Pageviews API endpoint contains only user traffic data but data from the Legacy Pagecounts does not. 

## Project Details
There are 3 stages in this project: data acquisition, data processing and data analysis. The code for each section can be found in the [jupyter notebook](hcds-a1-data-curation.ipynb).
### Data Acquisition
The data for the project is retrieved from the two API endpoints mentioned above. The raw result for each set of the data per API per device type is saved as json files. Because the Legacy Pagecounts API provides data with two types of devices and the other provides three, there are five json files in total, each with a name convention of 'apiname_devicetype_firstmonth-lastmonth.json'. There is about one year of overlapping between the data provided by the two API endpoints, so data for this year is collected from both sources. 

### Data Processing
Json files collected from the previous step are transformed into a dataframe in this section to better prepare for the analysis. There are two major processing steps. First, data from the two mobile-type devices in the Pageviews API is combined together and labled as mobile. Each API endpoint now associates with two types of devices: desktop and mobile. Second, year and month are extracted from the 'timestamp' information provided in the original json files, which means the exact days and hours are neglected. 

All data is then combined into a single csv, with all NA values being replaced with 0. To better understand the total pageviews, the pageviews of mobile and desktop are added together for each API endpoints. Column names for pageviews information follows the name convention 'apiname_devicetype_views'.

#### Final Data
The final dataset is named as [en-wikipedia_traffic_200712-202109.csv](en-wikipedia_traffic_200712-202109.csv). It contains eight fields: year, month, pagecount_all_views, pagecount_mobile_views, pagecount_desktop_views, pageview_all_views, pageview_mobile_views, pageview_desktop_view.

### Data Anlysis
Data is visualized as a time-series graph in this step to show the trend of Wikipedia pageviews over years. There are six columns of pageviews data and each of them is shown with a different color on the graph. Due to the size of the data, the number of pageviews is shown in 10 billions and only the first month of each year is labled on the x ticks. A .png file of the [graph](time_series.png) is stored in the repository. 

## License & Copyright
Licensed under the [MIT License](LICENSE)

By using the REST API, I agree to Wikimedia's general [Terms of Use](https://foundation.wikimedia.org/wiki/Terms_of_Use/en) and [Privacy Policy](https://foundation.wikimedia.org/wiki/Privacy_policy).

