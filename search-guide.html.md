---
title: Data Dictionary and Search Guide for Pivotal Cloud Foundry&reg; Log Search
owner: London Services
---

<a id="data-dictionary"></a>
## Data Dictionary

In the Available Fields pane of the Discover tab, elevated fields are denoted by a prefixing **@**, and show information
that Log Search has extrapolated from the raw data and are considered useful in interpreting the data.
These will always be displayed at the top of the Available Fields pane for ease of access.

| Field      				| Description                                                                                                                                      | Example                                                                                                                                           |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| @timestamp 				| Parsed timestamp of log message, in UTC.  Defaults to parse time.  Overridden by syslog_timestamp, or timestamp pulled from specific log message | 2015-11-18T15:00:04.896Z                                                                                                                          |
| @timestamp_ns 		| Nano-seconds since Unix Epoch (optional) 																																																	| For a timestamp of 1463503340.250173807, @timestamp_ns would be 173,807                                                                           |
| @level     				| Indicates the severity level of the message                                                                                                  		| Can be one of: DEBUG, INFO, WARN, ERROR or FATAL																																																	|
| @message  				| Unparsed / human readable text of log.  May be empty if all data has been parsed into separate fields                                                                                                            | Switchboard.Error routing to backend                                                                                                                                            			|
| @raw   		 				| The raw unparsed message                                                                                                                         | <139>2016-01-28T21:17:52.856995+00:00 10.0.16.88 switchboard [job=proxy-partition-e3353cc4ddedf43fa7a6 index=0]  {"timestamp":"1454015872.856954575","source":"Switchboard","message":"Switchboard.Error routing to backend","log_level":2,"data":{"error":"No active Backend"}} |
| @source.deployment| Name of deployment cluster log is from (eg, bosh deployment or Tile name)                                                               |	'CF' if from a cloud foundry job, or 'logsearch' if from a logsearch job														 	 																						|
| @source.host			| Guid of the container which is running an app. Defaults to @source.ip if this does not apply                                                  |	'4138q23c-1v2c-4a21-9szbc-4b37c11fda0b' if from a container, or '10.0.1.6' if from a vm														 	 															|
| @source.ip				| IP address of the origin vm                                                  																																		|	10.0.1.6														 	 																																																						|
| @source.job				| Name of source component                                                 																										|	In a logsearch deployment: 'elasticsearch\_data', 'elasticsearch_master', 'kibana' etc.														 	 															|
| @source.index			| Instance of source component job                                               									|	0														 	 																																																										|
| @source.vm				| Combination of @source.job and @source.index                                                   																									|	'elasticseach_data/0'														 	 																																													      |
| @source.program		| Program emitting the logs   |	cloud\_controller\_ng													 	 																																													      		|
| tags							| Arbitrary set of tags    |	syslog_standard, NATS									 	 																																													      		|


<a id="search-examples"></a>
## Search examples

Making search queries against these fields is relatively straightforward.

The following examples are search queries that can be made from the discover tab.

####Timestamps

The kibana UI comes with an easy way to filter logs by time. Absolute time periods, and time periods relative to now
are available.

* Relative query: To see logs from the last 4 hours, click on the "Last 15 minutes" button in the top right corner
of the discover tab, and select "last 4 hours" from the options. To make a more specific relative query, click on the
"Relative" button on the left hand side navigation bar.

* Absolute query: To see logs during a specific time period in the past, use the "Absolute" option in the left hand side
navigation bar, and select the time period you wish to view.


####Other fields

To search against any of the other fields, type in the search bar a query with the following format: `field:value`

For example: `@source.ip:10.0.16.21`
