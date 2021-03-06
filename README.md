# Graylog Content Packs

This repository contains various content packs I have created and want to share with the community.

## GeoIP Lookup
### Details
- **Filename**: `geoip-lokup.json` 
- **Description**: Check source and destination IPs for geolocation and set associated fields 
- **Requirements**: MaxMind GeoLite2 City Database    
- **Parameters**: `maxmind_db` (path to maxmind db on Graylog server; default: `/etc/graylog/server/GeoLite2-City.mmdb`

### Notes
**Content Pack Entities**
- Lookup adapter, cache, and table for getting MaxMind data.
- `dst_ip RFC1918` and `src_ip RFC1918` pipeline rules (must come before the geoip lookup rules but after normalizations and should be edited to use whatever you normalize the destination and source IP fields to)
- `src_ip geoip lookup` and `dst_ip geoip lookup` pipeline rules (should be edited to use whatever you normalize the destination and source IP fields to)

## Volatility Analysis
### Details
- **Filename**: `volatility-analysis.json` 
- **Description**: See: https://medium.com/@megansroddie/volatility-analysis-with-graylog-ffb7048c4e76
- **Requirements**: See: https://github.com/megan201296/vol2graylog   
- **Parameters**: N/A

### Notes
**Recommendations**
- I recommend creating a "Volatility" stream and then creating a pipeline rule to redirect any messages from your Volatility input to that stream.  

**Content Pack Entities**
- Pipeline with various rules to normalize and enrich Volatility results.

## XFE IP Risk Score
### Details
- **Filename**: `xfe-ip-risk-score.json` 
- **Description**: Performs an API lookup against an IP and returns the risk score calculated by [X-Force Exchange](https://exchange.xforce.ibmcloud.com)   
- **Requirements**: X-Force Exchange IP Key    
- **Parameters**: auth_header  

### Notes
**Creating the auth_header value**
- Run `echo "${XFE_APIKEY?}:${XFE_PASSWD?}" | base64` where `${XFE_APIKEY?}` is your XFE API key and `${XFE_PASSWD?}` is your XFE API password
- Prepend `Basic ` (note the space) to the value returned above

**Limits**
- Free tier allows for "non-commercial usage of up to 5,000 records per month for querying across the range of threat information from X-Force Exchange".
- "IBM reserves the right to disable any account deemed abusing our system. Abuse-related activity includes, but is not limited to sharing accounts, bulk registrations, abuse of API calls, suspicious/malicious query parameters and accessing restricted resources. Additionally, users are expected to follow our limiting practices as outlined in the HTTP responses. To avoid limiting errors, no more than 3,000 requests should be made in a one minute period to the X-Force Exchange API."

### To Do
- Expand to include more XFE values/data (IP risk score reason, hash lookup, etc.)
- Create examples of pipeline rules leveraging this lookup table.
