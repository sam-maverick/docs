# geoip_client.repy

XMl-RPC client for remote GeoIP server. Given an IP:port of a GeoIP XML-RPC server, allows location lookup of hostnames and IP addresses.

This module is an addition to the basic implementation found in [wiki:SeattleLib/xmlrpc_client.repy]. A GeoIP client essentially allows for on the go location lookup of various nodes around the world. This module is optional and not required, as clients can freely choose to use the more tested [wiki:SeattleLib/xmlrpc_client.repy] instead.


### Functions

```
def geoip_init_client(url="http://geoip.poly.edu:12679"):
``` 
   Creates a new GeoIP XML-RPC client object.
   
   Notes: 

   * url is a URL (protocol://ip:port) of GeoIP XML-RPC server.
   * url is defaulted to http://geoip.poly.edu:12679


```
def geoip_record_by_addr(addr):
```
   Request location data of provided IP address from GeoIP XML-RPC server

   Notes: 

   * addr is the IP address of which to look up location.
   * Returns a dictionary of location data of provided IP address.


```
def geoip_record_by_name(name):
```
   Request location data of provided hostname from GeoIP XML-RPC server

   Notes: 

   * name is the hostname of which to look up location.
   * Returns a dictionary of location data of provided hostname.


```
def geoip_location_str(location_dict):
```
   Pretty-prints a location specified by location_dict as a comma-separated list. Prints location info as specifically as it can, according to the

   format 'CITY, STATE/PROVINCE, COUNTRY'.
   location_dict['city'], location_dict['region_name'], and
   location_dict['country_name'] are added if defined, and
   location_dict['region_name'] is added if the location is in the US or Canada.
      
   Notes:

   * location_dict is the dictionary of location information, as returned by a call to geoip_record_by_addr or geoip_record_by_name.
   * Returns a string representation of a location.


### Usage

```
client = geoip_init_client(server_address)
# Where server_address is the ip address of a remote GeoIP XMl-RPC server.
```

Example:
```
geoip_init_client(["http://geoipserver.poly.edu:12679"]) 
# with no parameters, geoip_init_client() uses 
# ["http://geoipserver.poly.edu:12679", "http://geoipserver2.poly.edu:12679"] by default
# then it assigns the returned client to geoip_clientlist

client=geoip_clientlist[0]
client.send_request("record_by_addr", ("173.194.33.16",), 100)
```

### Includes

[wiki:SeattleLib/xmlrpc_client.repy]