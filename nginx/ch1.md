# 1.4 Verifying Your Installation
You can verify that NGINX is installed and check its version by using the following command:

```
$ nginx -v
nginx version: nginx/1.25.3
```

# 1.5 Key Files, Directories, and Commands

## NGINX files and directories 

```
/etc/nginx/
```
The /etc/nginx/ directory is the default configuration root for the NGINX server. Within this directory you will find configuration files that instruct NGINX on how to behave.

```
/etc/nginx/nginx.conf
```
The /etc/nginx/nginx.conf file is the default configuration entry point used by the NGINX daemon. This configuration file sets up global settings for things like worker processes, tuning, logging, loading dynamic modules, and references to other NGINX configuration files. In a default configuration, the /etc/nginx/nginx.conf file includes the top-level http block, or context, which includes all configuration files in the directory described next.

```
/etc/nginx/conf.d/
```
The /etc/nginx/conf.d/ directory contains the default HTTP server configuration file. Files in this directory ending in .conf are included in the top-level http block from within the /etc/nginx/nginx.conf file. It’s best practice to utilize include statements and organize your configuration in this way to keep your configuration files concise. In some package repositories, this folder is named sites-enabled, and configuration files are linked from a folder named site-available; this convention is deprecated.
```
/var/log/nginx/
```
The /var/log/nginx/ directory is the default log location for NGINX. Within this directory you will find an access.log file and an error.log file. By default the access log contains an entry for each request NGINX serves. The error logfile contains error events and debug information if the debug module is enabled.

## NGINX commands

`nginx -v`

Shows the NGINX version.

`nginx -V`

Shows the NGINX version, build information, and configuration arguments, which show the modules built into the NGINX binary.

`nginx -t`

Tests the NGINX configuration.

`nginx -T`

Tests the NGINX configuration and prints the validated configuration to the screen. This command is useful when seeking support.

`nginx -s signal`

The -s flag sends a signal to the NGINX master process. You can send signals such as stop, quit, reload, and reopen. The stop signal discontinues the NGINX process immediately. The quit signal stops the NGINX process after it finishes processing in-flight requests. The reload signal reloads the configuration. The reopen signal instructs NGINX to reopen logfiles.


# 1.6 Using Includes for Clean Configs


Use the include directive to reference configuration files, directories, or masks:

```
http {
  include conf.d/compression.conf;
  include ssl_config/*.conf
}
```

By logically grouping your configurations together, you can rest assured that your configurations are neat and organized. 
Changing a set of configuration files can be done by editing a single file rather than changing multiple sets of configuration blocks in multiple locations within a massive configuration file.
Grouping your configurations into files and using include statements is good practice for your sanity and the sanity of your colleagues.
The include directive takes a single parameter of either a path to a file or a mask that matches many files. This directive is valid in any context.


# 1.7 Serving Static Content

Overwrite the default HTTP server configuration located in /etc/nginx/conf.d/default.conf with the following NGINX configuration example:

```
server {
  listen 80 default_server; 
  server_name www.example.com; 

  location / {
    root /usr/share/nginx/html;
    # alias /usr/share/nginx/html;
    index index.html index.htm;
  }
}
```

This configuration serves static files over HTTP on port 80 from the directory /usr/share/nginx/html/. 
The first line in this configuration defines a new server block. 
This defines a new context that specifies what NGINX listens for.
Line two instructs NGINX to listen on port 80, and the default_server parameter instructs NGINX to use this server as the default context for port 80. 
The listen directive can also take a range of ports. The server_name directive defines the hostname or the names of requests that should be directed to this server.
If the configuration had not defined this context as the default_server, NGINX would direct requests to this server only if the HTTP host header matched the value provided to the server_name directive. 
With the default_server context set, you can omit the server_name directive if you do not yet have a domain name to use.


The location block defines a configuration based on the path in the URL. The path, or portion of the URL after the domain, is referred to as the uniform resource identifier (URI). NGINX will best match the URI requested to a location block. The example uses / to match all requests. The root directive shows NGINX where to look for static files when serving content for the given context. The URI of the request is appended to the root directive’s value when looking for the requested file. If we had provided a URI prefix to the location directive, this would be included in the appended path, unless we used the alias directive rather than root. The location directive is able to match a wide range of expressions. Visit the first link in the “See Also” section for more information. Finally, the index directive provides NGINX with a default file, or list of files to check, in the event that no further path is provided in the URI.
