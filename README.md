# webproject

First job

Go to SCM -GIT  ---->Repositoyr URL---->http://github.com/anurag08-git/webproject.git -----> Branch- specifier   *dev1/ ---> Repository browser - (Auto)
Build Triggers  ----> Poll Scm ==========> Schedule - * * * * *
Build Execute shell  ----> sudo cp -v -r -f * /myweb
                           if sudo docker ps | grep weba
                            then
                            echo "already running"
                             else
                            sudo docker run -d -t -i -p 8081:80 -v /myweb:/usr/local/apache2/htdocs/ --name weba httpd
                             fi
   Apply and Save
   
   Second job
   
   Go to SCM -GIT  ---->Repositoyr URL---->http://github.com/anurag08-git/webproject.git -----> Branch- specifier   *master/ ---> Repository browser - (Auto)
Build Triggers  ----> Poll Scm ==========> Schedule - * * * * *
Build Execute shell  ----> sudo cp -v -r -f * /myweb1
                           if sudo docker ps | grep webb
                            then
                            echo "already running"
                             else
                            sudo docker run -d -t -i -p 8083:80 -v /myweb1:/usr/local/apache2/htdocs/ --name webb httpd
                             fi
   Apply and Save
   
   Third job
   
    Go to SCM -GIT  ---->Repositoyr URL---->http://github.com/anurag08-git/webproject.git -----> Credentials - ADD  User name  and  Password of github
    Branch- specifier   *master/ ---> Repository browser - (Auto)
    	Additional Behaviours	-  Merge before build 
                                                 Name of repository- origin	
                                                 Branch to merge to	- master
                                               
 	                                              Merge strategy	- default	
 	                                              Fast-forward mode --ff
                                                
 Post-build Actions - Build other projects - Projects to build	- Second job  - Trigger only if build is stable
 
 Execute shell- 
       status=$(curl  -o  /dev/null  -s  -w "%{http_code}"  192.168.99.102:8081/a.html)
       echo $status
       
       if [[ $status == 200 ]]
       then
        exit 0
       else
        exit 1
       fi 
 Git publisher - 	Push Only If Build Succeeds		right
 	                   Merge Results                right
      Apply and save               

                             
