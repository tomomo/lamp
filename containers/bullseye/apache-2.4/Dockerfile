FROM httpd:2.4-bullseye

RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN \
  sed -i '/LoadModule expires_module/s/^#//g'     /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule authnz_fcgi_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule proxy_module/s/^#//g'       /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule proxy_http_module/s/^#//g'  /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule proxy_http2_module/s/^#//g' /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule proxy_html_module/s/^#//g'  /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule proxy_fcgi_module/s/^#//g'  /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule rewrite_module/s/^#//g'     /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule ssl_module/s/^#//g'         /usr/local/apache2/conf/httpd.conf && \
  sed -i '/LoadModule http2_module/s/^#//g'       /usr/local/apache2/conf/httpd.conf && \
  { \
    echo ''; \
    echo '# customize'; \
    echo '<Directory "/var/www/html">'; \
    echo '    Options FollowSymLinks'; \
    echo '    AllowOverride All'; \
    echo '    Require all granted'; \
    echo ''; \
    echo '    DirectoryIndex disabled'; \
    echo '    DirectoryIndex index.php index.html'; \
    echo '</Directory>'; \
    echo 'Include conf/common/*.conf'; \
    echo 'Include conf/vhosts/*.conf'; \
  } >> /usr/local/apache2/conf/httpd.conf

COPY common /usr/local/apache2/conf/common
COPY vhosts /usr/local/apache2/conf/vhosts

RUN { \
    echo 'export PS1="\[\e[0;36m\][\u@\h \W]\\$ \[\e[m\]"'; \
  } >> "$HOME/.bashrc"
