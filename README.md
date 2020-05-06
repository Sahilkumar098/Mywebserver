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
