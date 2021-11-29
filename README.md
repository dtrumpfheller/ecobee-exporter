# ecobee_exporter
Ecobee exporter for metrics in Prometheus format

This is a fork of [https://github.com/billykwooten/ecobee-exporter](https://github.com/billykwooten/ecobee-exporter), see there for more details and to check out the great work Billy Wooten is doing!

# Changes
I made following changes in my fork:
- Added `holdTempMetric` metrics
- Added `hvacInOperation` metrics (limited to "CompCool1", "AuxHeat1", "Fan" as that is all I need)

# Usage
Please see Billys repository for detailed instructions.

To run with docker-compose, following steps are necessary to get it up and running.
There might be better and/or more elegant ways, but this is how I id dit id ;)

1. Add following to your docker-compose file (adjust based on your needs)
```
  ecobee-exporter:
    container_name: ecobee-exporter
    image: billykwooten/ecobee-exporter
    restart: unless-stopped
    ports:
      - 9098:9098
    environment:
      - ECOBEE_APPKEY=<ADD APP KEY HERE>
    volumes:
      - ./data/ecobee:/db
    stdin_open: true
    tty: true
```
2. Run `docker-compose up -d && docker attach ecobee-exporter`
3. Open a browser and go to http://localhost:9098/metrics
4. Docker will now print a pin like `Pin is "ABCD-EFGH"`
5. Go to [https://www.ecobee.com/consumerportal/index.html#/my-apps](https://www.ecobee.com/consumerportal/index.html#/my-apps)
6. Register your app pin from step 4
7. Confirm completion by clicking the enter key in the attached terminal
8. Remove or comment out `stdin_open` & `tty` in the docker-compose file and restart via `docker-compose up -d`
