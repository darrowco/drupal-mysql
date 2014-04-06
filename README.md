Based on https://github.com/cl9p/docker-centos-mysql-drupal

Directions
==========

1. Install docker

2. Install Git

        yum install git

3. Change to your users home directory

		cd {$HOME}
		
4. Clone the repository

		git clone https://github.com/darrowco/drupal-mysql.git
		
5. Run the Dockerfile

                sudo docker build -t darrowco/drupal-mysql .
		
6. Run **supervisord**

                docker run -p 80:80 -t -i -e ROOT_PASS="root" darrowco/drupal-mysql:0.01 supervisord
		
7. Open a browser to your and you should see the screens for setting up drupal

Notes
=====

* The drupal database server is called **drupaldb** and the username is **drupal** and the password is **drupal**
* When you shut down the container, all of your data will be lost.  To learn how to modify the Dockerfile to enable local filesystem access, check out this link: [Docker VOLUME](http://docs.docker.io/en/latest/use/builder/#volume).  When you do this, you will also need to modify the mysql configuration at ``/etc/my.cnf``.

Handy Scripts
=============

Should you run into issues setting up your container and image, use these scripts to automatically remove them so you can test your Dockerfile

* Remove all containers
		
		docker rm $(docker ps -a -q)

* Remove all images

		docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
