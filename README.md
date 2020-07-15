# jenkins-docker
## Running Jenkins locally on docker using apache as a reverse proxy.

### Steps to do
  - use `docker-compose up` or `docker-compose up -d` (to start process running in background).
  - go to `http://localhost:8080` to setup the jenkins admin user and required plugins. (make sure you have copied `initaladminpassword` for first login).
  - #### Setting up the apache reverse proxy
      - enable proxy mod using `sudo a2enmod proxy proxy_html rewrite headers proxy_http proxy_connect deflate`
      - restart apache2 using `sudo systemctl restart apache2`
      - confiure `/etc/hosts` to add `local.jenkins.com` as a local-domain. (it can be anything, make sure in conf file servername should be same as your local domain name).
      - copy `jenkins-docker.conf` and paste it on your `/etc/apache2/sites-available/` directory.
      - create log directory and required files using `sudo mkdir /var/log/apache2/jenkins-docker`, `sudo touch /var/log/apache2/jenkins-docker/error.log` and `sudo touch /var/log/apache2/jenkins-docker/access.log`.
      - run `sudo a2ensite ./jenkins-docker.conf` to enable site on apache2.
      - check your config using `apachectl -t`.
      - restart your apache server.
      - visit your local domain using any browser `http://local.jenkins.com`, it must redirect to your running jenkins container on docker.
      - done.
      
      
