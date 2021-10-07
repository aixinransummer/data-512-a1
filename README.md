# data-512-a1 Data Curation

## Goal
The goal of this project is to aqcuire, clean and visualize a dataset of monthly traffic data on English Wikipedia and make sure the work done during this process is fully reproducible by others. 

## Description
This project collects and analyzes monthly pageviews data of English Wikipedia from two API endpoints from January 1st 2008 to September 30th 2021. 

## API Endpoints
The two API endpoints used for this project are the Legacy Pagecounts API and the Pageviews API. 

- The Legacy Pagecounts API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts), [endpoint](https://wikimedia.org/api/rest_v1/#/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end)) provides access to desktop and mobile traffic data from December 2007 through July 2016.

- The Pageviews API ([documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews), [endpoint](https://wikimedia.org/api/rest_v1/#/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.

Notice that there are two types of devices provided by the Legacy Pagecounts whreas there three provided by the Pageviews API. However, during analysis, data from the two mobile-type devices in the Pageviews API was combined together. In addition, the Pageviews allow us to select only the user traffic (not spiders/crawlers) by setting agent to 'user' but the Legacy Pagecounts does not. Thus, data from the Pageviews API endpoint contains only user traffic data but data from the Legacy Pagecounts does not. 

## Final Data
The final dataset contains eight fields: year, month, pagecount_all_views, pagecount_mobile_views, pagecount_desktop_views, pageview_all_views, pageview_mobile_views, pageview_desktop_view

## License & Copyright
Licensed under the [MIT License](LICENSE)

By using the REST API, I agree to Wikimedia's general [Terms of Use](https://foundation.wikimedia.org/wiki/Terms_of_Use/en) and [Privacy Policy](https://foundation.wikimedia.org/wiki/Privacy_policy).

