# Interface: [HttpClientConnectionManager](https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/conn/HttpClientConnectionManager.html)
- Implementing class 1. [BasicHttpClientConnectionManager](https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/impl/conn/BasicHttpClientConnectionManager.html) : manages only one active connection
- Implementing class 2. [PoolingHttpClientConnectionManager](https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/impl/conn/PoolingHttpClientConnectionManager.html) : manages the number of connections requests from multiple execution threads.


# HttpClient
## Redirect strategy
A strategy for determining if a HTTP request should be redirected to a new location in response to an HTTP response received from the target server.

https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/client/RedirectStrategy.html
