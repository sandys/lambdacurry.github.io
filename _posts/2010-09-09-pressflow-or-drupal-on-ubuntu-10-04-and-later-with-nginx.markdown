---
author: sandeep
comments: true
date: 2010-09-09 06:07:44+00:00
layout: post
link: http://www.lambdacurry.com/2010/09/pressflow-or-drupal-on-ubuntu-10-04-and-later-with-nginx/
slug: pressflow-or-drupal-on-ubuntu-10-04-and-later-with-nginx
title: Pressflow (or Drupal) on Ubuntu 10.04 and later .. with nginx, php-fpm and
  clean-urls
wordpress_id: 422
---

For god's sake do not use PHP 5.3 . Custom compile your own [php-fpm 5.2](http://www.ivankuznetsov.com/2010/05/moving-joomla-wordpress-and-other-phpfastcgi-apps-to-nginx.html). Maybe setup nginx with clean URL and the configuration given .

If you use PHP5.3, then any failure in any db connection/query (for me it was postgresql) will result in the php thread being killed ("_child process exited with status 1_"). 5.2 doesnt have this problem.


<blockquote>

>     
>     ﻿server {
>     
>       listen   8080; ## listen for ipv4
>       listen   [::]:8080 default ipv6only=on; ## listen for ipv6
>     
>       server_name  localhost;
>     
>             root /var/www/1/;
>             large_client_header_buffers 4 8k;
>             access_log  /var/log/nginx/1.access.log urchin;
>     
>            ## Serve an empty 1x1 gif _OR_ an error 204 (No Content) for favicon.ico
>           location ~* ^.+.(ico) {
>            #empty_gif;
>             return 204;
>             expires max;
>           }
>           location ~* ^.+.(jpg|jpeg|gif|css|png|js)(?[0-9]+)?$ {
>             root /var/www/1/;
>            access_log off;
>             expires max;
>             }
>     
>             location / {
>                 #root   /var/www/1/;
>                 index  index.html index.php;
>                 add_header Last-Modified "";
>                 if_modified_since off;
>                 error_page 404 = @drupal;
>             }
>     
>             location @drupal {
>                               rewrite ^(.*)$ /index.php?q=$1 last;
>             }
>     
>             location ~ .php$ {
>                     #include /usr/local/nginx/conf/fastcgi_params;
>                     include /etc/nginx/fastcgi_params;
>                     fastcgi_pass  localhost:9000;
>                     fastcgi_index index.php;
>                     fastcgi_read_timeout 500m;
>                     fastcgi_param  SCRIPT_FILENAME  /var/www/1$fastcgi_script_name;
>      fastcgi_param  SCRIPT_NAME      $fastcgi_script_name;
>                     fastcgi_param  QUERY_STRING     $query_string;
>                     fastcgi_param  REQUEST_METHOD   $request_method;
>                     fastcgi_param  CONTENT_TYPE     $content_type;
>                     fastcgi_param  CONTENT_LENGTH   $content_length;
>                     fastcgi_intercept_errors on;
>             }
>     }
> 
> 
﻿</blockquote>
