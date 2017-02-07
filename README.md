# logstash.conf
## version
[Logstash 2.2.0 All Plugins](https://www.elastic.co/downloads/past-releases/logstash-2-2-0-all-plugins)

## reference
there are 3 parts of logstash
 - [input](https://www.elastic.co/guide/en/logstash/current/input-plugins.html)
 - [filter](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)
 - [output](https://www.elastic.co/guide/en/logstash/current/output-plugins.html)
 
### filter::grok tools
  [grok match online check](http://grokconstructor.appspot.com/do/match) <br/>
  [grok Pattern](https://github.com/elastic/logstash/blob/v1.4.2/patterns/grok-patterns) <br/>
### filter::grok concept
#### Given Filter
```Shell
    grok {
      match => { "message" => "%{DATESTAMP:timestamp} %{LOGLEVEL:level} %{NOTSPACE:marker} %{NOTSPACE:method} %{NOTSPACE:message}" }
      remove_field => [ "marker" ]
      add_tag => [ "master" ]
    }
    date {
      match => [ "timestamp", "yy-MM-dd HH:mm:ss.SSS" ]
      remove_field => [ "timestamp" ]
    }
```
#### input
```Shell
   2017-02-06 07:16:55.392 INFO ANA GET /feed/category
```
#### output
```Shell
   {
     "level": "INFO",
     "method": "GET",
     "message": "/feed/category"
   }
```

## Sample
```Shell
input {
  ...
}

filter {
  ...
}

output {
  ...
}
```
