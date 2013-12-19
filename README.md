haproxy Cookbook
==============
Installs and configure haproxy.

Platform
--------
- Ubuntu 10.04, 12.04 (x32/x64)
- CentOS 5, 6 (x64)

Requirements
------------
Chef 10.16.2+.

Cookbooks
---------
Requires Opscode's openssl cookbook for secure password generation.
Requires Opscode's apt cookbook for adding development haproxy repo.

Attributes
----------
* `node['haproxy']['stats_user']` sets haproxy statistic's user (default is `'admin'`).
* `node['haproxy']['stats_pass']` sets haproxy statistic's user password (default is `pa55w0rd`).
* `node['haproxy']['stats_uri']` sets haproxy statistic's url (default is `/admin?stats`)
* `node['haproxy']['stats_port']` sets haproxy statistic's port (default is `1926`)

Usage
-----
`[haproxy::default]` will setup haproxy and create global config

`[haproxy::add_servers]` will add list of servers to bucket

Options should be in following format:
`server:port bucket ssl_cert`

Where
* `server` = IP or DNS name of the server
* `port` = server's application port
* `bucket` - is string like `http://roundrobin:80/url`

Where
* `http` - protocol type (http/https/tcp/ssl)
* `roundrobin` - balancing type
* `80` - haproxy port for balancing
* `/url` - haproxy url

Opton `ssl_cert` is optional (file or http path to ssl cert)

`[haproxy::del_servers]` will remove list of servers from bucket

Options should be in fiollowing format:
* `server` - IP or DNS server to delete bucket
* `port` - server's port to delete from bucket
* `bucket` - in format `http://roundrobin:80/url` is optional. If not passed, then server:port will be deleteded from all haproxy buckets

