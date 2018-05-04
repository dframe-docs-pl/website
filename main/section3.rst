.. div:: row
 .. div:: col-md-6
  |img/restful.jpg|

 .. div:: col-sm-6
  Przyjazne linki
  ^^^^^^^^^^^^^^^

  W wersji produkcyjnej dla samego nawet bezpieczeństwa warto używać.
  |listing|

.. |img/restful.jpg| router:: img/restful.jpg
 :publicWeb:
 :img:
 :width: 100%


.. |listing| customLi:: myTab
 :apache2: Apache (.htaccess)
 :nginx: active/Nginx (.conf)
  .. code-block:: apache
   RewriteEngine On
   
   #Deny access for hidden folders and files
   RewriteRule (^|/)\.([^/]+)(/|$) - [L,F]
   RewriteRule (^|/)([^/]+)~(/|$) - [L,F]
   
   # Ustawia folder web jako katalog głowny
   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteRule ^(.*)$ web/$1
   
   # Przekazuje zapytanie na index.php
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteRule ^(.*)$ web/index.php [QSA,L]
  next
  .. code-block:: nginx
  
   # Ustawia folder web jako katalog głowny
   location / {
       root   /home/[project_path]/htdocs/web;
       index  index.html index.php index.htm;
       if (!-e $request_filename) {
           rewrite ^/(.*)$ /index.php?q=$1 last;
       }
   }
   
   # Przekazuje zapytanie na index.php
   location ~ .php$ {
       try_files $uri = 404;
       fastcgi_pass 127.0.0.1:9000;
       #fastcgi_pass unix:/run/php/php7.1-fpm.sock;
       fastcgi_index web/index.php;
       fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
       include fastcgi_params;
   }



