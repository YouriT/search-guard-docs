# Search Guard Enterprise Edition

Search Guard ships the Enterprise Edition by default. All Enterprise modules and features are included and enabled by default. In order to use this edition on productive systems you need to [obtain a license](https://floragunn.com/searchguard-license-support/). 

## Trial License

When installing Search Guard for the first time, a trial license is automatically generated. This license is valid for 60 days and includes all enterprise features.

## Enterprise License

For running Search Guard on production systems you need to [obtain a license](https://floragunn.com/searchguard-license-support/). Search Guard is licensed per cluster, and the license covers all non-production systems like development, staging and QA as well.

## Academic and Scientific License

Because we love to support education and science, we offer free licenses for non-profit academic and scientific usage. 

Free enterprise licenses are available for:

* Non-profit academic and scientific projects
* Non-profit educational purposes
* Unlimited amount of clusters
* Unlimited amount of time

Please see the [License and Support page](https://floragunn.com/searchguard-license-support/) to see if your institution is eligible for this programme. 

## OEM license

If you're a system integrator or want to ship Search Guard as part of your own product, please [see our partners page](https://floragunn.com/search-guard-partners/) for further information.

## License Handling

### Displaying your current license

You have several ways to check the contents of your current license.

#### Logfile

On startup, Search Guard will print license information to the Elasticsearch logfile.

#### HTTP license endpoint

The following endpoint will return your current license and information about the active Search Guard modules in JSON format:

```
https://<Elasticsearch Host>:<HTTP Port>/_searchguard/license
```

For example:

```
https://example.com:9200/_searchguard/license
```

You don't need to authenticate to access this endpoint.

#### REST API

The REST API offers an endpoint to retrieve your current license information. To access it, you need to use an account that has the privilege to use the REST API. If you used the demo installation script for installing and initializing Search Guard, you can use the admin user for that, e.g.:

```
curl -Ss --insecure -u admin:admin -XGET https://example.com:9200/_searchguard/license?pretty
```

See the [REST management API](managementapi.md) configuration chapter for further information on how to configure API users.

#### Kibana Configuration GUI

If you're using the Search Guard Kibana plugin, you can display your license and system information by clicking on "Search Guard" / "License & System Info".

### Applying an Enterprise License

After obtaining an enterprise license, you can apply it in two ways. 

#### sg_config.yml

Add the license string to sg_config.yml and upload the configuration by using sgadmin. You can either configure the license on a single line, or use YAML multi-line format:

```
searchguard:
  dynamic:
    license: LS0tLS1CRUdJTiBQR1A...
    http:
      ...
    authc:          
      ...
```

```
searchguard:
  dynamic:
    license: |-
      LS0tLS1CRUdJTiBQR1AgU0lHTkVEIE1FU
      1NBR0UtLS0tLQpIYXNoOiBTSEE1M
      ...    
    http:
      ...
    authc:          
      ...
```

When using `sgadmin` to upload the changed `sg_config.yml` with the new license, any existing license will be overwritten. In order to backup your existing license, you can use the the `-r` (`--retrieve`) switch with [sgadmin](sgadmin.md), e.g.:

```
./sgadmin.sh \ 
  -ks kirk.jks -kspass changeit \  
  -ts truststore.jks -tspass changeit \ 
  -icl -nhnv -r
``` 
#### REST API

You can use the [REST management API](managementapi.md) license endpoint to `POST` an Enterprise License to Search Guard.

#### Kibana Configuration GUI

If you're using the Search Guard Kibana plugin, you upload a new license by clicking on "Search Guard" / "License & System Info" / "Upload new license". Paste the complete license string in the input field and click on "Upload".