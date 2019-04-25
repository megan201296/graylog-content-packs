# Graylog Content Packs

This repository contains various content packs I have created and want to share with the community:

## XFE IP Risk Score
### Details
**Filename**: `xfe-ip-risk-score.json`
**Description**: Performs an API lookup against an IP and returns the risk score calculated by [X-Force Exchange](https://exchange.xforce.ibmcloud.com)   
**Requirements**: X-Force Exchange IP Key    
**Parameters**: auth_header  

### Notes
**Creating the auth_header value**
- Run `echo "${XFE_APIKEY?}:${XFE_PASSWD?}" | base64` where `${XFE_APIKEY?}` is your XFE API key and `${XFE_PASSWD?}` is your XFE API password
- Prepend `Basic ` (note the space) to the value returned above

### To Do
- Expand to include more XFE values/data (IP risk score reason, hash lookup, etc.)
- Create examples of pipeline rules leveraging this lookup table.
