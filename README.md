## Overview

Mattazurl is an HTTP proxy service that makes a HTTP request based on parameters defined in the URL of the request it received, and returns the response.

The service expects a definition of a HTTP request message in the URL of a request to the service. The service decodes the HTTP request defined in the URL, performs the decoded HTTP request and returns the received response as the response of calling the service. In essence, the service translates the definition of a HTTP request encoded in the URL to a real HTTP request. Furthermore, the service sets the [cross-origin resource sharing](http://www.w3.org/TR/cors/) headers so that it may be invoked from a Web applications executing in browsers.

The API defines how a HTTP request should be encoded in the service request URLs. Element of a HTTP request are encoded as URL query parameters:

- (mandatory) HTTP method - `method` query parameter (e.g. `method=GET`)
- (mandatory) destination URL - `url` query parameter (e.g. `url=https://api.github.com/markdown/raw`)
- (optional) body - `body` parameter (e.g. `body=**Hello** _World_`)
- (optional, multiple) HTTP headers - multiple query parameters specified as `headerName=headerValue` (e.g. `Content-Type=text/plain`)
- (optional) debugMode - specifies debug mode and the response will be send as the body in text/plain (e.g. `debugMode=1`

Furthermore, the parameter names and values must be URL-encoded.

I cloned [Izuzak's urlreq](https://github.com/izuzak/urlreq) repo and had to make some changes.

The proxy is being hosted on [Google's App Engine](https://cloud.google.com/appengine/). For this to work I had to adapt a few things in the code.

1.  I went to [Google App Engine Downloads](https://cloud.google.com/appengine/downloads) and downloaded just the SDK for python 2.7. I also downloaded the `python-extras` but am pretty sure I did not need them.
2.  After download I went to the Google Cloud interface and since I already have a bunch of projects there I just created a new one called `mattazurl` so I was not using a client project.
3.  I went back to the command line and did the `gcloud init` command and authorized the cloud platform on my machine and then it asked me to select a project, which I selected the one I had just created.
4.  I then went back to the repo I downloaded and opened the files with VS Code. VS Code recommended I download an extension to work with Python, which I did, and I made the edits to the files.
5.  After I made the edits, I looked at one of those how-to projects to see some of the commands.
6.  I then `cd /mattazurl/src` and opened a terminal. This is where I actually used the `deploy` command which I copied from the how-to project. I used `gcloud app deploy app.yaml --project mattazurl` which is why I made sure I was in the `src` folder so I could use the `app.yaml` file.
7.  Once I did this it started throwing errors in the cli. It just told me that it did not need the `application: urlreq-hrd` so I deleted that. Tried the deploy command again and it threw the error that it did not need the version. So I deleted the `version: 1` line and tried again.

After all of this... It worked and is deployed and working.

- The environment is python 2.7
