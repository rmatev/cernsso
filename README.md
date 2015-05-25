# cern-sso
Python wrappers above cern-get-sso-cookie.

Assumptions are:
 * You have cern-get-sso-cookie on your system installed
 * You have your CERN user certificate in some secure directory named `myCert.pem` and `myCert.key`

Basic usage:
```python
from cernsso.cookie import CookieManager

# Directory should contain myCert.pem, myCert.key and be writable
m = CookieManager("/your/private/directory")

url = "http://eindex.cern.ch/"

# This cookie should be used with your http requests
cookies = m.get_cookie(url)

import requests
r = requests.get(url, cookies=cookies) # probably will fail without export REQUESTS_CA_BUNDLE=/etc/ssl/certs/CERNGridCertificationAuthority.pem
```


The `m.get_cookie` does load cached cookie, if it was obtained in last 24-hours. To force-obtain cookie one should use `m.get_new_cookie`.

All cookies are stored in sqlite storage inside working directory `"/your/private/directory"`
