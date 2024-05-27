WOTS ElasticSearch
===
# General

## Host
| Env | IP Address |
| -------- | -------- | 
| Dev     | http://10.4.31.250:5601 | 
| QA     | http://10.4.31.230:5601 | 
| Live     | http://10.4.31.20:5601 | 

## Header
| Key | Value | 
| -------- | -------- | 
| Authorization     | Basic aGFwcHl0dWtkZXY6eUBxcWh0dWtTRUpKMzgxMw==

## Url
/system-log*/_search
example: http://10.4.31.250:9200/system-log*/_search


------------------------------------------------------------------------------------------------------------------------------------------------


# Daily Active User
Get daily active user, change startTime and EndTime can get more

## Request body

| Name      | Description       | Example                   |
| --------- | ----------------- | ------------------------- |
| StartTime | timeRange's begin | 2023-10-16T00:00:00+08:00 |
| EndTime   | timeRange's end   | 2023-10-17T00:00:00+08:00 |

please replace bodyJSON's {{startTime}} and {{endTime}}
e.g. "gte":"2023-10-16T00:00:00+08:00"

if we need get daily interval, change **fixed_interval** to 1d

* bodyJSON:
```json
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "time": {
              "gte":"2015-01-01T00:00:00Z", 
              "lte":"2015-01-01T23:59:59Z"
            }
          }
        }
      ]
    }
  },
  "size": 0,
  "aggs": {
    "called": {
      "filter": {
        "exists": {
          "field": "playerID"
        }
      },
      "aggs": {
        "called_histogram": {
          "date_histogram": {
            "field": "time",
            "fixed_interval": "5m",
            "time_zone": "+08:00",
            "min_doc_count": 0,
            "extended_bounds": {
              "min": "2015-01-01T00:00:00Z",
              "max": "2015-01-01T23:59:59Z"
            }
          },
          "aggs": {
            "count": {
              "terms": {
                "field": "playerID.keyword",
                "size": 10000
              }
            }
          }
        }
      }
    }
  }
}
```
## Response 
please counting **aggregations.called.called_histogram.buckets.count.buckets** , it will be that interval's active user count.

example:
```json
{
    "took": 4,
    "timed_out": false,
    "_shards": {
        "total": 3,
        "successful": 3,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 167,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "called": {
            "doc_count": 160,
            "called_histogram": {
                "buckets": [
                    {
                        "key_as_string": "2023-10-16T11:00:00.000+08:00",
                        "key": 1697425200000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:05:00.000+08:00",
                        "key": 1697425500000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:10:00.000+08:00",
                        "key": 1697425800000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:15:00.000+08:00",
                        "key": 1697426100000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:20:00.000+08:00",
                        "key": 1697426400000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:25:00.000+08:00",
                        "key": 1697426700000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:30:00.000+08:00",
                        "key": 1697427000000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:35:00.000+08:00",
                        "key": 1697427300000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:40:00.000+08:00",
                        "key": 1697427600000,
                        "doc_count": 107,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": [
                                {
                                    "key": "5xMLVqBkqJ",
                                    "doc_count": 107
                                }
                            ]
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:45:00.000+08:00",
                        "key": 1697427900000,
                        "doc_count": 53,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": [
                                {
                                    "key": "5xMLVqBkqJ",
                                    "doc_count": 53
                                }
                            ]
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:50:00.000+08:00",
                        "key": 1697428200000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T11:55:00.000+08:00",
                        "key": 1697428500000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    },
                    {
                        "key_as_string": "2023-10-16T12:00:00.000+08:00",
                        "key": 1697428800000,
                        "doc_count": 0,
                        "count": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": []
                        }
                    }
                ]
            }
        }
    }
}
```

------------------------------------------------------------------------------------------------------------------------------------------------


# Purchase Information

## Request body
| Name      | Description       | Example                   |
| --------- | ----------------- | ------------------------- |
| StartTime | timeRange's begin | 2023-10-16T00:00:00+08:00 |
| EndTime   | timeRange's end   | 2023-10-17T00:00:00+08:00 |

please replace bodyJSON's {{startTime}} and {{endTime}} to time value
e.g. 2023-10-16T00:00:00+08:00 and 2023-10-17T00:00:00+08:00

* bodyJSON:
```json
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "time": {
              "gte":{{startTime}},
              "lte":{{endTime}}
            }
          }
        }, 
        {
            "exists": {
                "field": "price"
            }
        }
      ]
    }
  },
  "size": 10000
}
```
## Response 
| Name          | Description                                           | Example                                  |
| ------------- | ----------------------------------------------------- | ---------------------------------------- |
| device        | {{device system}}-{{client machine hash code}}        | Android-d9a6fafa36a044b2689e6e51e46043b2 |
| index         | GoodsID, please ref to excel store.xlsx - sheet: shop |                                          |
| price         | purchase amount                                       |                                          |
| transactionID | android or iOS's transactionID  (In progress)         |                                          |

example:
```json
{
    "took": 3,
    "timed_out": false,
    "_shards": {
        "total": 3,
        "successful": 3,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 3,
            "relation": "eq"
        },
        "max_score": 0.0,
        "hits": [
            {
                "_index": "system-log-2023-10",
                "_id": "FBdcI4sBRfiMs9EccpJj",
                "_score": 0.0,
                "_source": {
                    "level": "INFO",
                    "time": "2023-10-12T18:08:15.938+08:00",
                    "msg": "",
                    "caller": "querys.(*PlayerStorePremium).BuyGoods",
                    "playerID": "5xWeXmsDNB",
                    "device": "Android-d9a6fafa36a044b2689e6e51e46043b2",
                    "cause": "StorePremiumBuy",
                    "index": 10002,
                    "before": "{\"GoodsID\":10002,\"SeasonID\":0,\"Count\":0,\"Bought\":false}",
                    "after": "{\"GoodsID\":10002,\"SeasonID\":1,\"Count\":0,\"Bought\":true}",
                    "certificate": "bckpibnmelelcgpieblfbkim.AO-J1OytRuw3JD5JyTQzE7iiVj8DfWzOLuTdkcjaQdnyeiX2sofo3U4MIgQ-5fW18Rfl0atmsjSqlsib8nsvFjJaW8scunr3HQ",
                    "price": 170
                }
            },
            {
                "_index": "system-log-2023-10",
                "_id": "RhdcI4sBRfiMs9EccpJj",
                "_score": 0.0,
                "_source": {
                    "level": "INFO",
                    "time": "2023-10-12T18:08:30.146+08:00",
                    "msg": "",
                    "caller": "querys.(*PlayerStorePremium).BuyGoods",
                    "playerID": "5xWeXmsDNB",
                    "device": "Android-d9a6fafa36a044b2689e6e51e46043b2",
                    "cause": "StorePremiumBuy",
                    "index": 10035,
                    "before": "{\"GoodsID\":10035,\"SeasonID\":0,\"Count\":0,\"Bought\":false}",
                    "after": "{\"GoodsID\":10035,\"SeasonID\":0,\"Count\":1,\"Bought\":true}",
                    "certificate": "oglmeihgbkocpmajopdcplnl.AO-J1Oyp_Hk6_pr0qkK17myvDGYC5Q0S3td2OpHB9fN676q1bJU0Uypaf3Jdvz7lKtSwDZ_DIXskLhaV0AWiFz6ouVDRcANdug",
                    "price": 490
                }
            },
            {
                "_index": "system-log-2023-10",
                "_id": "dBdcI4sBRfiMs9EccpJj",
                "_score": 0.0,
                "_source": {
                    "level": "INFO",
                    "time": "2023-10-12T18:08:56.806+08:00",
                    "msg": "",
                    "caller": "querys.(*PlayerStorePremium).BuyGoods",
                    "playerID": "5xWeXmsDNB",
                    "device": "Android-d9a6fafa36a044b2689e6e51e46043b2",
                    "cause": "StorePremiumBuy",
                    "index": 10115,
                    "before": "{\"GoodsID\":10115,\"SeasonID\":0,\"Count\":0,\"Bought\":false}",
                    "after": "{\"GoodsID\":10115,\"SeasonID\":0,\"Count\":1,\"Bought\":true}",
                    "certificate": "penaecbaecgeifbbkadldagd.AO-J1OyqSpKDB9bEYre1Mj50i_THWvT71320gNTn9kOIhrZnP0sLyGleT--Tcr6j3aN6qOZEXypDqWZHStuxBUU6iLuvXL6D8Q",
                    "price": 30
                }
            }
        ]
    }
}
```



```json
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "time": {
              "gte":_{{startTime}}_,
              "lte":_{{endTime}}_
            }
          }
        }, 
        {
            "match": {
                "caller": "Signin"
            }
        }
      ]
    }
  },
  "size": 10000
}
```


### purchase request sample
```json
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "time": {
            "gte":"2023-10-10T00:00:00+08:00", 
            "lte":"2023-10-30T00:00:00+08:00"
            }
          }
        }, 
        {
            "exists": {
               "field": "transactionID"
            }
        }
      ]
    }
  },
  "size": 10000
}
```

### daily active user request sample
```json
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "time": {
              "gte":"2023-10-16T00:00:00+08:00", 
              "lte":"2023-10-17T00:00:00+08:00"
            }
          }
        }, 
        {
            "match": {
                "caller": "Signin"
            }
        }
      ]
    }
  },
  "size": 10000
}
```
