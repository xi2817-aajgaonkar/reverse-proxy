# reverse-proxy
- Copy the following `grafana.ini` file and place it in `data` directory
```
[server]
protocol= http
domain= localhost
http_port= 3000
root_url= "%(protocol)s://%(domain)s:%(http_port)s/grafana/"
serve_from_sub_path= true

[auth.proxy]
enabled = true
# HTTP Header name that will contain the username or email
header_name = X-WEBAUTH-USER
# HTTP Header property, defaults to `username` but can also be `email`
header_property = username
# Set to `true` to enable auto sign up of users who do not exist in Grafana DB. Defaults to `true`.
auto_sign_up = true
# Define cache time to live in minutes
# If combined with Grafana LDAP integration it is also the sync interval
sync_ttl = 60
# Limit where auth proxy requests come from by configuring a list of IP addresses.
# This can be used to prevent users spoofing the X-WEBAUTH-USER header.
# Example `whitelist = 192.168.1.1, 192.168.1.0/24, 2001::23, 2001::0/120`
whitelist =
# Optionally define more headers to sync other user attributes
# Example `headers = Name:X-WEBAUTH-NAME Role:X-WEBAUTH-ROLE Email:X-WEBAUTH-EMAIL Groups:X-WEBAUTH-GROUPS`
headers =
# Non-ASCII strings in header values are encoded using quoted-printable encoding
;headers_encoded = false
# Check out docs on this for more details on the below setting
enable_login_token = false
```
- Command to start Docker container
 `docker run --name grafana --rm -v "$PWD/data:/etc/grafana" -p 3000:3000 grafana/grafana`
- Command to start Go server
  `go run main.go`