## Overview

URL Req is an HTTP proxy service that makes a HTTP request based on parameters defined in the URL of the request it received, and returns the response.

The service expects a definition of a HTTP request message in the URL of a request to the service. The service decodes the HTTP request defined in the URL, performs the decoded HTTP request and returns the received response as the response of calling the service. In essence, the service translates the definition of a HTTP request encoded in the URL to a real HTTP request. Furthermore, the service sets the [cross-origin resource sharing](http://www.w3.org/TR/cors/) headers so that it may be invoked from a Web applications executing in browsers.

The API defines how a HTTP request should be encoded in the service request URLs. Element of a HTTP request are encoded as URL query parameters:

- (mandatory) HTTP method - `method` query parameter (e.g. `method=GET`)
- (mandatory) destination URL - `url` query parameter (e.g. `url=https://api.github.com/markdown/raw`)
- (optional) body - `body` parameter (e.g. `body=**Hello** _World_`)
- (optional, multiple) HTTP headers - multiple query parameters specified as `headerName=headerValue` (e.g. `Content-Type=text/plain`)
- (optional) debugMode - specifies debug mode and the response will be send as the body in text/plain (e.g. `debugMode=1`

Furthermore, the parameter names and values must be URL-encoded.
