node {

def mvnHome

stage('Prepare') {

git url: 'git@github.com:Debraj68/product-app.git', branch: 'develop'

mvnHome = tool 'mvn'

}

stage('Build') {

if (isUnix()) {

sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"

} else {

bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)

}

}

stage('Unit Test') {

junit '**/target/surefire-reports/TEST-*.xml'

archive 'target/*.jar'

}

stage('Integration Test') {

if (isUnix()) {

sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean verify"

} else {

bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean verify/)

}

}



stage('Deploy') {

sh 'curl -u admin:admin -T target/**.war "http://localhost:9080/manager/text/deploy?path=/ibmdevops&update=true"&#39;

}

stage("Smoke Test"){

sh "curl --retry-delay 10 --retry 5 http://localhost:5050/ibmdevops/api/v1/products&quot;

}

}


Announcement: "<role rolename="tomcat"/> <role…"
pradeep murthy
Created YesterdayYesterday
<role rolename="tomcat"/>


  <role rolename="manager-gui"/>


  <role rolename="manager-script"/>
  <user username="tomcat" password="tomcat" roles="tomcat"/>
  <user username="manager" password="tomcat" roles="tomcat, manager-gui"/>
  <user username="jenkins" password="jenkins" roles="manager-script"/>