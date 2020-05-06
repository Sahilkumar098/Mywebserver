# Mywebserver
## What is this project ?
 This project is a CI pipeline implementation of a webapp on Docker technology with jenkins.
## Tasks/Jobs
  **Job1** - Constantly checks Github for changes on Master branch and builds Production_server on sucessfull Job1 build
  
  **Production server** - Deploys Docker container for web hosting with concept of port forwarding.
  
  **Job2** - Constantly checks for changes on dev1 branch and build Testing server on sucess of job2 build.
  
  **Testing server** - Deploys Docker container for Testing my web app  (Testing server) with concept of port forwarding.
  
  **Approval** - A jenkins job which tester runs manually to approve a webapp. And the  build automatically merges the two branches 
                 if the webapp is manually approved by the tester.
## How I did it.
 **Job1 and Job2**
  - downloaded the git pulgin from the pulgin manager in jenkins.
  - Created a new freestyle job/item 
  - clicked on configure and selected git under SCM.
  - Entered my repo link and the branch from which i wanted to interact with.
  - Did the setup of my trigger for github Hooks.
  - And copied my repo to a folder in base system which is linked to my production server and testing server respectively.
  - and Setup my downstream jobs (That deployed my production and testing server respectively)
 
 **Production and testing server**
   - Under the build category, execute the docker containers:
    
    for example: 
    if sudo docker ps | grep production_server
    then
    echo "already running"
    elif sudo docker ps -a |grep production_server
    then
    sudo docker start production_server
    else
    sudo docker container run -dit -p 80:80 -v /root/web/:/usr/local/apache2/htdocs/ --name production_server httpd:latest
    fi
    
   - Similarily you can do for Testing_Server as well.
 
 **Approval**
   - unfortunately I don't know any automatic testing tools so I settled for manual testing and Made a Job named Approval where the 
   tester himself manually builds the job if the testing is sucessfull. 
   - the main focus was how to merge two branches if tesing was sucessfull.
   - for that under the "after build" category, click on add and specify git merge and provide the branch to be merged there.
   - once the build is complete the Job will automatically merge the two branches and upload the merged master branch to you git repo.
   
### Conclusion
 
 After this setup is done, we have our own pipeline where we can continously upload our code , change our code and test our code with 
 almost Zero effort and cost. Creating a Continous Integration and continous deploment culture while developing.
 
 Try for yourself.
 
