# csv2influx

A CLI tool for converting csv file to influxdb database.
You can map csv fields to influxdb columns in config file.

See [examples](examples)

## Install

```
npm install -g csv2influx
```

## Usage

```
csv2influx init                                       Creates template config file
csv2influx [--config path/to/config.json] data.csv    Loads config from path/to/config.json
                                                      then imports file data.csv to your influx
                                                      Default path: ./csv2influx.conf.json
Options:
  -q              Show progress bar and only unimported records
```

## Config example

```javascript

{
  "influxdbUrl": "http://127.0.0.1:8086/INFLUXDB_URL", // Database has to exist
  "measurementName": "MEASUREMENT_NAME",
  "mapping": {
    "time": { // first you need to specify from which fields you will get time
      "from": "date",
      "type": "timestamp",
      "format": "jsDate" // field "format" is required for timestamp.
                          // in this case means that string will by parsed as
                          // JavaScript date string format
                          // https://www.w3schools.com/js/js_date_formats.asp
    },
    "fieldSchema": {
      "name": { // fields "from" and "type" are required
        "from": "name",
        "type": "string" // influxdb string target type
      },
      "latitude": {
        "from": "lat", // we use field "lat" from CSV to fill up field "latitude" in DB
        "type": "float" // influxdb float target type
      },
      "longitude": {
        "from": "lng", // we use field "lng" from CSV to fill up field "longitude" in DB
        "type": "float"
      },
      "location": {
        "from": "location",
        "type": "string"
      },
    },
  },
  "csv": { // Parser options from http://csv.adaltas.com/parse/
    "delimiter": ','
  }
}

```

See more [examples](examples) to learn more about mapping


