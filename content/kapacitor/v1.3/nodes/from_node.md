---
title: FromNode
note: Auto generated by tickdoc

menu:
  kapacitor_1_3:
    name: From
    identifier: from_node
    weight: 90
    parent: nodes
---

A [FromNode](/kapacitor/v1.3/nodes/from_node/) selects a subset of the data flowing through a [StreamNode.](/kapacitor/v1.3/nodes/stream_node/) 
The stream node allows you to select which portion of the stream you want to process. 

Example: 


```javascript
    stream
        |from()
           .database('mydb')
           .retentionPolicy('myrp')
           .measurement('mymeasurement')
           .where(lambda: "host" =~ /logger\d+/)
        |window()
        ...
```

The above example selects only data points from the database `mydb` 
and retention policy `myrp` and measurement `mymeasurement` where 
the tag `host` matches the regex `logger\d+` 


Index
-----

### Properties

-	[Database](/kapacitor/v1.3/nodes/from_node/#database)
-	[GroupBy](/kapacitor/v1.3/nodes/from_node/#groupby)
-	[GroupByMeasurement](/kapacitor/v1.3/nodes/from_node/#groupbymeasurement)
-	[Measurement](/kapacitor/v1.3/nodes/from_node/#measurement)
-	[RetentionPolicy](/kapacitor/v1.3/nodes/from_node/#retentionpolicy)
-	[Round](/kapacitor/v1.3/nodes/from_node/#round)
-	[Truncate](/kapacitor/v1.3/nodes/from_node/#truncate)
-	[Where](/kapacitor/v1.3/nodes/from_node/#where)

### Chaining Methods

-	[Alert](/kapacitor/v1.3/nodes/from_node/#alert)
-	[Bottom](/kapacitor/v1.3/nodes/from_node/#bottom)
-	[Combine](/kapacitor/v1.3/nodes/from_node/#combine)
-	[Count](/kapacitor/v1.3/nodes/from_node/#count)
-	[CumulativeSum](/kapacitor/v1.3/nodes/from_node/#cumulativesum)
-	[Deadman](/kapacitor/v1.3/nodes/from_node/#deadman)
-	[Default](/kapacitor/v1.3/nodes/from_node/#default)
-	[Delete](/kapacitor/v1.3/nodes/from_node/#delete)
-	[Derivative](/kapacitor/v1.3/nodes/from_node/#derivative)
-	[Difference](/kapacitor/v1.3/nodes/from_node/#difference)
-	[Distinct](/kapacitor/v1.3/nodes/from_node/#distinct)
-	[Elapsed](/kapacitor/v1.3/nodes/from_node/#elapsed)
-	[Eval](/kapacitor/v1.3/nodes/from_node/#eval)
-	[First](/kapacitor/v1.3/nodes/from_node/#first)
-	[Flatten](/kapacitor/v1.3/nodes/from_node/#flatten)
-	[From](/kapacitor/v1.3/nodes/from_node/#from)
-	[HoltWinters](/kapacitor/v1.3/nodes/from_node/#holtwinters)
-	[HoltWintersWithFit](/kapacitor/v1.3/nodes/from_node/#holtwinterswithfit)
-	[HttpOut](/kapacitor/v1.3/nodes/from_node/#httpout)
-	[HttpPost](/kapacitor/v1.3/nodes/from_node/#httppost)
-	[InfluxDBOut](/kapacitor/v1.3/nodes/from_node/#influxdbout)
-	[Join](/kapacitor/v1.3/nodes/from_node/#join)
-	[K8sAutoscale](/kapacitor/v1.3/nodes/from_node/#k8sautoscale)
-	[KapacitorLoopback](/kapacitor/v1.3/nodes/from_node/#kapacitorloopback)
-	[Last](/kapacitor/v1.3/nodes/from_node/#last)
-	[Log](/kapacitor/v1.3/nodes/from_node/#log)
-	[Max](/kapacitor/v1.3/nodes/from_node/#max)
-	[Mean](/kapacitor/v1.3/nodes/from_node/#mean)
-	[Median](/kapacitor/v1.3/nodes/from_node/#median)
-	[Min](/kapacitor/v1.3/nodes/from_node/#min)
-	[Mode](/kapacitor/v1.3/nodes/from_node/#mode)
-	[MovingAverage](/kapacitor/v1.3/nodes/from_node/#movingaverage)
-	[Percentile](/kapacitor/v1.3/nodes/from_node/#percentile)
-	[Sample](/kapacitor/v1.3/nodes/from_node/#sample)
-	[Shift](/kapacitor/v1.3/nodes/from_node/#shift)
-	[Spread](/kapacitor/v1.3/nodes/from_node/#spread)
-	[StateCount](/kapacitor/v1.3/nodes/from_node/#statecount)
-	[StateDuration](/kapacitor/v1.3/nodes/from_node/#stateduration)
-	[Stats](/kapacitor/v1.3/nodes/from_node/#stats)
-	[Stddev](/kapacitor/v1.3/nodes/from_node/#stddev)
-	[Sum](/kapacitor/v1.3/nodes/from_node/#sum)
-	[Top](/kapacitor/v1.3/nodes/from_node/#top)
-	[Union](/kapacitor/v1.3/nodes/from_node/#union)
-	[Window](/kapacitor/v1.3/nodes/from_node/#window)

Properties
----------

Property methods modify state on the calling node.
They do not add another node to the pipeline, and always return a reference to the calling node.
Property methods are marked using the `.` operator.


### Database

The database name. 
If empty any database will be used. 


```javascript
node.database(value string)
```


### GroupBy

Group the data by a set of tags. 

Can pass literal * to group by all dimensions. 
Example: 


```javascript
  stream
      |from()
          .groupBy(*)
```



```javascript
node.groupBy(tag ...interface{})
```


### GroupByMeasurement

If set will include the measurement name in the group ID. 
Along with any other group by dimensions. 

Example: 


```javascript
 stream
      |from()
          .database('mydb')
          .groupByMeasurement()
          .groupBy('host')
```

The above example selects all measurements from the database &#39;mydb&#39; and 
then each point is grouped by the host tag and measurement name. 
Thus keeping measurements in their own groups. 


```javascript
node.groupByMeasurement()
```


### Measurement

The measurement name 
If empty any measurement will be used. 


```javascript
node.measurement(value string)
```


### RetentionPolicy

The retention policy name 
If empty any retention policy will be used. 


```javascript
node.retentionPolicy(value string)
```


### Round

Optional duration for rounding timestamps. 
Helpful to ensure data points land on specific boundaries 
Example: 


```javascript
    stream
       |from()
           .measurement('mydata')
           .round(1s)
```

All incoming data will be rounded to the nearest 1 second boundary. 


```javascript
node.round(value time.Duration)
```


### Truncate

Optional duration for truncating timestamps. 
Helpful to ensure data points land on specific boundaries 
Example: 


```javascript
    stream
       |from()
           .measurement('mydata')
           .truncate(1s)
```

All incoming data will be truncated to 1 second resolution. 


```javascript
node.truncate(value time.Duration)
```


### Where

Filter the current stream using the given expression. 
This expression is a Kapacitor expression. Kapacitor 
expressions are a superset of InfluxQL WHERE expressions. 
See the [expression](/kapacitor/v1.3/tick/expr/) docs for more information. 

Multiple calls to the Where method will `AND` together each expression. 

Example: 


```javascript
    stream
       |from()
          .where(lambda: condition1)
          .where(lambda: condition2)
```

The above is equivalent to this 
Example: 


```javascript
    stream
       |from()
          .where(lambda: condition1 AND condition2)
```


NOTE: Becareful to always use `|from` if you want multiple different streams. 

Example: 


```javascript
  var data = stream
      |from()
          .measurement('cpu')
  var total = data
      .where(lambda: "cpu" == 'cpu-total')
  var others = data
      .where(lambda: "cpu" != 'cpu-total')
```

The example above is equivalent to the example below, 
which is obviously not what was intended. 

Example: 


```javascript
  var data = stream
      |from()
          .measurement('cpu')
          .where(lambda: "cpu" == 'cpu-total' AND "cpu" != 'cpu-total')
  var total = data
  var others = total
```

The example below will create two different streams each selecting 
a different subset of the original stream. 

Example: 


```javascript
  var data = stream
      |from()
          .measurement('cpu')
  var total = stream
      |from()
          .measurement('cpu')
          .where(lambda: "cpu" == 'cpu-total')
  var others = stream
      |from()
          .measurement('cpu')
          .where(lambda: "cpu" != 'cpu-total')
```


If empty then all data points are considered to match. 


```javascript
node.where(lambda ast.LambdaNode)
```


Chaining Methods
----------------

Chaining methods create a new node in the pipeline as a child of the calling node.
They do not modify the calling node.
Chaining methods are marked using the `|` operator.


### Alert

Create an alert node, which can trigger alerts. 


```javascript
node|alert()
```

Returns: [AlertNode](/kapacitor/v1.3/nodes/alert_node/)


### Bottom

Select the bottom `num` points for `field` and sort by any extra tags or fields. 


```javascript
node|bottom(num int64, field string, fieldsAndTags ...string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Combine

Combine this node with itself. The data is combined on timestamp. 


```javascript
node|combine(expressions ...ast.LambdaNode)
```

Returns: [CombineNode](/kapacitor/v1.3/nodes/combine_node/)


### Count

Count the number of points. 


```javascript
node|count(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### CumulativeSum

Compute a cumulative sum of each point that is received. 
A point is emitted for every point collected. 


```javascript
node|cumulativeSum(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Deadman

Helper function for creating an alert on low throughput, a.k.a. deadman&#39;s switch. 

- Threshold -- trigger alert if throughput drops below threshold in points/interval. 
- Interval -- how often to check the throughput. 
- Expressions -- optional list of expressions to also evaluate. Useful for time of day alerting. 

Example: 


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    data
        |deadman(100.0, 10s)
    //Do normal processing of data
    data...
```

The above is equivalent to this 
Example: 


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    data
        |stats(10s)
            .align()
        |derivative('emitted')
            .unit(10s)
            .nonNegative()
        |alert()
            .id('node \'stream0\' in task \'{{ .TaskName }}\'')
            .message('{{ .ID }} is {{ if eq .Level "OK" }}alive{{ else }}dead{{ end }}: {{ index .Fields "emitted" | printf "%0.3f" }} points/10s.')
            .crit(lambda: "emitted" <= 100.0)
    //Do normal processing of data
    data...
```

The `id` and `message` alert properties can be configured globally via the &#39;deadman&#39; configuration section. 

Since the [AlertNode](/kapacitor/v1.3/nodes/alert_node/) is the last piece it can be further modified as usual. 
Example: 


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    data
        |deadman(100.0, 10s)
            .slack()
            .channel('#dead_tasks')
    //Do normal processing of data
    data...
```

You can specify additional lambda expressions to further constrain when the deadman&#39;s switch is triggered. 
Example: 


```javascript
    var data = stream
        |from()...
    // Trigger critical alert if the throughput drops below 100 points per 10s and checked every 10s.
    // Only trigger the alert if the time of day is between 8am-5pm.
    data
        |deadman(100.0, 10s, lambda: hour("time") >= 8 AND hour("time") <= 17)
    //Do normal processing of data
    data...
```



```javascript
node|deadman(threshold float64, interval time.Duration, expr ...ast.LambdaNode)
```

Returns: [AlertNode](/kapacitor/v1.3/nodes/alert_node/)


### Default

Create a node that can set defaults for missing tags or fields. 


```javascript
node|default()
```

Returns: [DefaultNode](/kapacitor/v1.3/nodes/default_node/)


### Delete

Create a node that can delete tags or fields. 


```javascript
node|delete()
```

Returns: [DeleteNode](/kapacitor/v1.3/nodes/delete_node/)


### Derivative

Create a new node that computes the derivative of adjacent points. 


```javascript
node|derivative(field string)
```

Returns: [DerivativeNode](/kapacitor/v1.3/nodes/derivative_node/)


### Difference

Compute the difference between points independent of elapsed time. 


```javascript
node|difference(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Distinct

Produce batch of only the distinct points. 


```javascript
node|distinct(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Elapsed

Compute the elapsed time between points 


```javascript
node|elapsed(field string, unit time.Duration)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Eval

Create an eval node that will evaluate the given transformation function to each data point. 
A list of expressions may be provided and will be evaluated in the order they are given. 
The results are available to later expressions. 


```javascript
node|eval(expressions ...ast.LambdaNode)
```

Returns: [EvalNode](/kapacitor/v1.3/nodes/eval_node/)


### First

Select the first point. 


```javascript
node|first(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Flatten

Flatten points with similar times into a single point. 


```javascript
node|flatten()
```

Returns: [FlattenNode](/kapacitor/v1.3/nodes/flatten_node/)


### From

Creates a new stream node that can be further 
filtered using the Database, RetentionPolicy, Measurement and Where properties. 
From can be called multiple times to create multiple 
independent forks of the data stream. 

Example: 


```javascript
    // Select the 'cpu' measurement from just the database 'mydb'
    // and retention policy 'myrp'.
    var cpu = stream
        |from()
            .database('mydb')
            .retentionPolicy('myrp')
            .measurement('cpu')
    // Select the 'load' measurement from any database and retention policy.
    var load = stream
        |from()
            .measurement('load')
    // Join cpu and load streams and do further processing.
    cpu
        |join(load)
            .as('cpu', 'load')
        ...
```



```javascript
node|from()
```

Returns: [FromNode](/kapacitor/v1.3/nodes/from_node/)


### HoltWinters

Compute the [holt-winters](/{{< latest "influxdb" >}}/query_language/functions/#holt-winters) forecast of a data set. 


```javascript
node|holtWinters(field string, h int64, m int64, interval time.Duration)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### HoltWintersWithFit

Compute the [holt-winters](/{{< latest "influxdb" >}}/query_language/functions/#holt-winters) forecast of a data set. 
This method also outputs all the points used to fit the data in addition to the forecasted data. 


```javascript
node|holtWintersWithFit(field string, h int64, m int64, interval time.Duration)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### HttpOut

Create an HTTP output node that caches the most recent data it has received. 
The cached data is available at the given endpoint. 
The endpoint is the relative path from the API endpoint of the running task. 
For example, if the task endpoint is at `/kapacitor/v1/tasks/&lt;task_id&gt;` and endpoint is 
`top10`, then the data can be requested from `/kapacitor/v1/tasks/&lt;task_id&gt;/top10`. 


```javascript
node|httpOut(endpoint string)
```

Returns: [HTTPOutNode](/kapacitor/v1.3/nodes/http_out_node/)


### HttpPost

Creates an HTTP Post node that POSTS received data to the provided HTTP endpoint. 
HttpPost expects 0 or 1 arguments. If 0 arguments are provided, you must specify an 
endpoint property method. 


```javascript
node|httpPost(url ...string)
```

Returns: [HTTPPostNode](/kapacitor/v1.3/nodes/http_post_node/)


### InfluxDBOut

Create an influxdb output node that will store the incoming data into InfluxDB. 


```javascript
node|influxDBOut()
```

Returns: [InfluxDBOutNode](/kapacitor/v1.3/nodes/influx_d_b_out_node/)


### Join

Join this node with other nodes. The data is joined on timestamp. 


```javascript
node|join(others ...Node)
```

Returns: [JoinNode](/kapacitor/v1.3/nodes/join_node/)


### K8sAutoscale

Create a node that can trigger autoscale events for a kubernetes cluster. 


```javascript
node|k8sAutoscale()
```

Returns: [K8sAutoscaleNode](/kapacitor/v1.3/nodes/k8s_autoscale_node/)


### KapacitorLoopback

Create an kapacitor loopback node that will send data back into Kapacitor as a stream. 


```javascript
node|kapacitorLoopback()
```

Returns: [KapacitorLoopbackNode](/kapacitor/v1.3/nodes/kapacitor_loopback_node/)


### Last

Select the last point. 


```javascript
node|last(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Log

Create a node that logs all data it receives. 


```javascript
node|log()
```

Returns: [LogNode](/kapacitor/v1.3/nodes/log_node/)


### Max

Select the maximum point. 


```javascript
node|max(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Mean

Compute the mean of the data. 


```javascript
node|mean(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Median

Compute the median of the data. Note, this method is not a selector, 
if you want the median point use `.percentile(field, 50.0)`. 


```javascript
node|median(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Min

Select the minimum point. 


```javascript
node|min(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Mode

Compute the mode of the data. 


```javascript
node|mode(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### MovingAverage

Compute a moving average of the last window points. 
No points are emitted until the window is full. 


```javascript
node|movingAverage(field string, window int64)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Percentile

Select a point at the given percentile. This is a selector function, no interpolation between points is performed. 


```javascript
node|percentile(field string, percentile float64)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Sample

Create a new node that samples the incoming points or batches. 

One point will be emitted every count or duration specified. 


```javascript
node|sample(rate interface{})
```

Returns: [SampleNode](/kapacitor/v1.3/nodes/sample_node/)


### Shift

Create a new node that shifts the incoming points or batches in time. 


```javascript
node|shift(shift time.Duration)
```

Returns: [ShiftNode](/kapacitor/v1.3/nodes/shift_node/)


### Spread

Compute the difference between `min` and `max` points. 


```javascript
node|spread(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### StateCount

Create a node that tracks number of consecutive points in a given state. 


```javascript
node|stateCount(expression ast.LambdaNode)
```

Returns: [StateCountNode](/kapacitor/v1.3/nodes/state_count_node/)


### StateDuration

Create a node that tracks duration in a given state. 


```javascript
node|stateDuration(expression ast.LambdaNode)
```

Returns: [StateDurationNode](/kapacitor/v1.3/nodes/state_duration_node/)


### Stats

Create a new stream of data that contains the internal statistics of the node. 
The interval represents how often to emit the statistics based on real time. 
This means the interval time is independent of the times of the data points the source node is receiving. 


```javascript
node|stats(interval time.Duration)
```

Returns: [StatsNode](/kapacitor/v1.3/nodes/stats_node/)


### Stddev

Compute the standard deviation. 


```javascript
node|stddev(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Sum

Compute the sum of all values. 


```javascript
node|sum(field string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Top

Select the top `num` points for `field` and sort by any extra tags or fields. 


```javascript
node|top(num int64, field string, fieldsAndTags ...string)
```

Returns: [InfluxQLNode](/kapacitor/v1.3/nodes/influx_q_l_node/)


### Union

Perform the union of this node and all other given nodes. 


```javascript
node|union(node ...Node)
```

Returns: [UnionNode](/kapacitor/v1.3/nodes/union_node/)


### Window

Create a new node that windows the stream by time. 

NOTE: Window can only be applied to stream edges. 


```javascript
node|window()
```

Returns: [WindowNode](/kapacitor/v1.3/nodes/window_node/)

