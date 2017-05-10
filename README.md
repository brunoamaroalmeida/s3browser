Amazon S3 Directory Browser
===========================

Please report any issues [here on GitHub](https://github.com/brunoamaroalmeida/s3browser/issues).


Configuration
-------------

The app configures itself thanks to environment variables.
The list of the supported variables are defined in the [config file](www/config.php).

Apache Setup in Debian
-------------

apt-get install apache2 -qy
apt-get install php5 libapache2-mod-php5 php5-curl libapache2-mod-proxy-html libxml2-dev -qy

a2enmod proxy
a2enmod proxy_http
a2enmod proxy_ajp
a2enmod rewrite
a2enmod deflate
a2enmod headers
a2enmod proxy_balancer
a2enmod proxy_connect
a2enmod proxy_html

service apache2 restart

Installation with Apache
----------------------

1. Check out the latest release from GitHub:

        cd /var/www/html
        git clone https://github.com/brunoamaroalmeida/s3browser.git

2. Add an Apache VirtualHost for your new subdomain. e.g.:

        <VirtualHost *:80>
          ServerName s3browser.example.com
          DocumentRoot /var/www/html/s3browser/www

          <Directory />
            AllowOverride all
            Order allow,deny
            Allow from all
          </Directory>
        </VirtualHost>

3. Tweak config to your liking. Each option is documented in the config.php file. Since it defaults to loading the values from environment variables, using [SetEnv](http://httpd.apache.org/docs/2.2/mod/mod_env.html) is probably best. You could also edit config.php to your liking.

4. Reload your Apache config:

        sudo /etc/init.d/apache2 reload


Docker integration
-------------------

1. Create a `.env` file with the configuration needed
2. Install [`docker-compose`](https://docs.docker.com/compose/)
3. Run `docker-compose up --build`

Give a look at the [Dockerfile](Dockerfile) and [docker-compose.yml](docker-compose.yml) if needed.
