# Historical Data via Direct API Access

## Format

### Endpoint
https://api.rriv.org/data/readings/{eui}

### Query Variables
* rangeStart: YYYY-MM-DD
* rangeEnd: YYYY-MM-DD
* format: csv | json


## cURLs
curl https://api.rriv.org/data/readings/ac1f09fffe1397e7

curl 'https://api.rriv.org/data/readings/ac1f09fffe1397e7?rangeStart=2025-01-01&rangeEnd=2025-12-31'

curl 'https://api.rriv.org/data/readings/ac1f09fffe1397e7?rangeStart=2025-01-01&rangeEnd=2025-12-31&format=csv' > out
