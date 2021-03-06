### NOTES






## Telemetry

##### Telegraf

[Link to --> Telegraf Documentation](https://docs.influxdata.com/telegraf/v1.23/get_started/#configure-telegraf)


```sh
$ telegraf --sample-config --input-filter cpu:mem --output-filter influxdb_v2 > telegraf.conf

###############################################################################
#                            INPUT PLUGINS                                    #
###############################################################################


# Read metrics about cpu usage
[[inputs.cpu]]
  ## Whether to report per-cpu stats or not
  percpu = true
  ## Whether to report total system cpu stats or not
  totalcpu = true
  ## If true, collect raw CPU time metrics
  collect_cpu_time = false
  ## If true, compute and report the sum of all non-idle CPU states
  report_active = false
  ## If true and the info is available then add core_id and physical_id tags
  core_tags = false


# Read metrics about memory usage
[[inputs.mem]]
  # no configuration
  
###############################################################################
#                            OUTPUT PLUGINS                                   #
###############################################################################


# Configuration for sending metrics to InfluxDB 2.0
[[outputs.influxdb_v2]]
  ## The URLs of the InfluxDB cluster nodes.
  ##
  ## Multiple URLs can be specified for a single cluster, only ONE of the
  ## urls will be written to each interval.
  ##   ex: urls = ["https://us-west-2-1.aws.cloud2.influxdata.com"]
  urls = ["http://127.0.0.1:8086"]

  ## Token for authentication.
  token = ""

  ## Organization is the name of the organization you wish to write to.
  organization = ""

  ## Destination bucket to write into.
  bucket = ""

  ## The value of this tag will be used to determine the bucket.  If this
  ## tag is not set the 'bucket' option is used as the default.
  # bucket_tag = ""

  ## If true, the bucket tag will not be added to the metric.
  # exclude_bucket_tag = false

  ## Timeout for HTTP messages.
  # timeout = "5s"

  ## Additional HTTP headers
  # http_headers = {"X-Special-Header" = "Special-Value"}

  ## HTTP Proxy override, if unset values the standard proxy environment
  ## variables are consulted to determine which proxy, if any, should be used.
  # http_proxy = "http://corporate.proxy:3128"

  ## HTTP User-Agent
  # user_agent = "telegraf"

  ## Content-Encoding for write request body, can be set to "gzip" to
  ## compress body or "identity" to apply no encoding.
  # content_encoding = "gzip"

  ## Enable or disable uint support for writing uints influxdb 2.0.
  # influx_uint_support = false

  ## Optional TLS Config for use on HTTP connections.
  # tls_ca = "/etc/telegraf/ca.pem"
  # tls_cert = "/etc/telegraf/cert.pem"
  # tls_key = "/etc/telegraf/key.pem"
  ## Use TLS but skip chain & host verification
  # insecure_skip_verify = false




```
```python
import requests

url = 'https://172.29.80.100/'

request = requests.get(url,verify=False)

print(request.status_code)


```


## NSO
Primary Components
- NETCONF : for auto and mgmt on neds
- YANG: for modeling services and devices.

NSO Arch
- Core Engine
  - CDB
- Device Manager
  - SouthBound APIS
  - YANG - DEVICE MODELS
- Service Manager
  - Service Manager
  - Service Models
- Mapping Logic
  - Template
  - FASTMAP

- SDN Ref Architecture
  - Service Layer/Specification Layer(Control Program)
    - Hides Complexities, model-to-model mapping, transactional
  - Network OS Layer (e.g NSO)
    - transactional to protect error and activation complaxity
    - model to multiple protocls mapping.
  - Forwarding Layer ( Protocols)
    - Controlled by OpenFlow or CLI, SNMP and NETCONF
    - Mix of traditional and openflow devices
    - All Device behaviors describe using device Data Models
##### NSO Installation
```
$ ./nso-5.3.2.linux.x86_64.signed.bin
$ ./nso-5.3.2.linux.x86_64.installer.bin ~/nso-5.3.2
#Edit Bashrc
~/.bashrc
# Add the line at the end of the .bashrc file
source /home/$USER/ncs-5.3.2/ncsrc
source ~/.bashrc

ncs
ncs --status
# Cisco CLI
ncs_cli -C -u admin
# Juniper
ncs_cli -J -u admin


```
##### NEDS
```
$ cp -r cisco-ios-cli-6.54 /home/nso-run/packages
$ cp -r cisco-iosxr-cli-7.26 /home/nso-run/packages
$ cp -r cisco-nx-cli-5.15 /home/nso-run/packages

$ ncs_cli -C -u admin
admin@ncs# packages reload
admin@ncs# show packages package package-version

```
##### NETSIM




```

ncs-netsim --help
ncs-netsim create network ~/nso-run/packages/neds/cisco-ios.cli 3 PE
ncs-netsim start
ncs-netsim list
ncs-netsim is-alive
ncs-netsim cli-c PE11
```
    ncs_cli -C -u admin
    ssh admin@localhost -p 2024
    http://localhost:8080
