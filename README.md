# cern-sso
Python wrappers above cern-get-sso-cookie.


Basic usage:
```python
from cernsso.cookie import CookieManager

# Directory should contain myCert.pem, myCert.key and be writable
m = CookieManager("/your/private/directory")

# This cookie should be used with your http requests
print m.get_cookie("http://eindex.cern.ch/")
```


The `m.get_cookie` does load cached cookie, if it was obtained in last 24-hours. To force-obtain cookie one should use `m.get_new_cookie`.

All cookies are stored in sqlite storage inside working directory `"/your/private/directory"`
