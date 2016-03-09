# Configure a Proxy

It is sometimes useful to front Go with a proxy server. In this section, we give you some tips and examples on how to achieve this.

## Go with Apache

An example of how to configure Go with Apache is shown below.

**Assumptions:**

-   You have Apache with mod\_proxy installed
-   The Apache server sits on the same machine as the Go server (localhost)
-   You want to enforce SSL connections

```apache
Listen nnn.nnn.nnn.nnn:80
NameVirtualHost nnn.nnn.nnn.nnn:80

<VirtualHost nnn.nnn.nnn.nnn:80>
    ServerName go.yourdomain.com
    DocumentRoot /var/www/html
    SSLProxyEngine on
    SSLEngine on
    ProxyPass / https://localhost:8154/
    ProxyPassReverse / https://localhost:8154/
</VirtualHost>
```

If you have set up Apache to use SSL, and Go is fronted with an Apache server, then you have to set `X_FORWARDED_PROTO` to "https" in the https virtual host configuration section.

```apache
RequestHeader set X_FORWARDED_PROTO 'https'
```

This directive can replace HTTP request headers. The header is modified just before the content handler is run, allowing incoming headers to be changed to 'https'.

## Also see...

-   [Configure site URLs](../installation/configuring_server_details.md#configure-site-urls)
