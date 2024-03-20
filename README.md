# mynewtest
<img src="https://jenkins.io/sites/default/files/jenkins_logo.png"/>

## cmd to start jenkins in docker
```
docker run -itd -v v1:/var/jenkins_home --restart=on-failure  -v /run/docker.sock:/run/docker.sock -v /usr/bin/docker:/bin/docker  -p 8080:8080 -p 50000:50000 jenkins/jenkins
```
