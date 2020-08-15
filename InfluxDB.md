# InfluxDB

## Time-series data
- Time Series data is a sequence of data points , a succesive measurements of data from same source over a time interval.
- Typically one of the axis of data would representation would be time.
- Regular timeseries data and Irregular timeseries data
  - Regular - usually metrics
  - Irregular - usually event driven data
## Time-series database
- Optimised for collecting ,storing ,retrieving and processing timeseries data.
- efficiently handle time-series data
- support time based queries
- Things that make time-series unique
  - Time-series workload
  - lifecyle management
  - summarization
  - large range scans of many records
> Example of tsdb- kx-kdb , openTSDB, graphite, riak, prometheus

### Primary usecases
- IoT
- DevOps
- Real-Time Analytics

### Why InfluxDB
- Easy to get started
- familiar query syntax
- No external dependencies
- allows for regular and irregular timeseries 
- horizontally and vertically scalable
- aims to solve the entire time-series platform
- Member of a cohesive timeseries platform
### Influxdb datamodel
- Label - measurement
- metadata - tags - indexed values in infludb
- y axis values - fields
- x axis - time data

> Note: - Should take care of data being segreated to tags and fields 
> in a way that the tags have less cardinality.
### InfludDB insite
- Data representation in timeseries - data is stored in Line protocol format 
> measurement,tagset fieldset timestamp
> ex:- stock_price,ticker=A,market=NASQAQ price=12,maxprice=15 14452999000
### Writing data into InfluxDB
- fieldset and tagset are sperated by space
  ex:-  stock_price,ticker=A,market=NASQAQ are tagset and what comes after are filedset ex: price=12,maxprice=15
### Schema Consideration
- Tags are indexed. Fields are not
- Field types are immutable
- store data in tags if you are gone use group by()
- store data in fields if you are gone use influxQL function(aggregation,math function)
- prefer data in fields to be integers/float
- be aware of series cardinality
#### Series cardinality
- Number of unique databse,measurement, and tagset combination in Influxdb
- Make sure you have less series more datapoints than vice verse
#### Retention Policies
#### Shard and shard groups
#### Continuous queries and Down sampling
- 2 ways to perform downsampling 
  - continous queries in influxdb
  - Using kapacitor as a continous query engine
- When to use kapaciotoer?
  - While performing a significant no of CQ's and want to isolate workload
  - When you need more data processing beyond just query
- Use CQ only when performing Downsampling for retention polies via query only ore when you have a only few CQ's
#### Influx SQL
- SQL like queries
- always consider scope while performing analysis. like dont use select * blah blah blah
- use time range on your queries to make them more efficient
#### InfluxQL Primer
- Find more on [InfluxQL spec](https://docs.influxdata.com/influxdb/v1.7/query_language/spec/) and [InfluxQL functons](https://docs.influxdata.com/influxdb/v1.7/query_language/functions/)
- InfluxQL supports regular expression


> Note:- Find more on query commands [Influxdb Doc](https://docs.influxdata.com/influxdb/v1.7/query_language/data_exploration/)

# TICK stack - Telegraf, InfluxDb, Chronograf, Kapacitor

## Telegraf
- Its an Opensource ,plugin driven server agent for collecting and reporting metrics.
- large collection of plugins
  - inputs
  - outputs
  - aggregators
  - processors
- Can act as an
  - agent
  - collector
  - Ingest pipeline
- Metrics ingestion from host system(cpu,i/o,network)
  - common programs (Hadoop,Postgres,Redis etc)
  - third party API's(cloudwatch,Google analyctics)
- Output Plugins to send metrics to other datastores
  - InfluxDB,Graphite,Kafka,MQTT,Prometheus..etc
### Telegraf Benefits
- Minimal memory footprint
- Tagging if metrics
- Easy contribution of functionality
- Strong COmmunity contributions and support
  