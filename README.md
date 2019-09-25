# CARMAcloud

## Documentation
CARMAcloud provides some of the infrastructure components for CARMA. It enables users to define geofences, rules of practice, replay storms to test weather-related rules of practice, as well as monitor CARMA-enabled vehicles and the messages and controls exchanged with them.

## Deployment
CARMAcloud can be deployed on a Linux server running the Debian Operating System by executing the following commands as root in the console:
1.  cd /tmp
2.  git clone https://github.com/kruegersp/cc.git
3.  sudo -u root apt-get update && sudo -u root apt-get install pkg-config sqlite3 libsqlite3-dev
4.  cd /tmp && wget http://apache.mirrors.lucidnetworks.net/tomcat/tomcat-9/v9.0.26/bin/apache-tomcat-9.0.26.tar.gz && tar -xzf apache-tomcat-9.0.26.tar.gz && mv apache-tomcat-9.0.26 tomcat
5.  find ./cc/src -name "*.java" > sources.txt && mkdir -p tomcat/webapps/carmacloud/ROOT/WEB-INF/classes
6.  javac -cp tomcat/lib/servlet-api.jar:cc/lib/commons-compress-1.18.jar:cc/lib/javax.json.jar:cc/lib/protobuf-javalite-3.8.0-rc-1.jar -d tomcat/webapps/carmacloud/ROOT/WEB-INF/classes @sources.txt
7.  sed -i '/<\/Engine>/ i \ \ \ \ \  <Host name="carmacloud" appBase="webapps/carmacloud" unpackWARs="false" autoDeploy="false">\n      </Host>' tomcat/conf/server.xml 
8.  echo -e '127.0.0.1\tcarmacloud' | sudo -u root tee -a /etc/hosts
9.  java -cp tomcat/webapps/carmacloud/ROOT/WEB-INF/classes/:tomcat/lib/servlet-api.jar cc.ws.UserMgr ccadmin admin_testpw > tomcat/webapps/carmacloud/user.csv
10.  mv tomcat /opt/
11.  sudo -u root /opt/tomcat/bin/catalina.sh start

## Configuration


## Contribution
Welcome to the CARMA contributing guide. Please read this guide to learn about our development process, how to propose pull requests and improvements, and how to build and test your changes to this project. [CARMA Contributing Guide](Contributing.md) 

## Code of Conduct 
Please read our [CARMA Code of Conduct](Code_of_Conduct.md) which outlines our expectations for participants within the CARMA community, as well as steps to reporting unacceptable behavior. We are committed to providing a welcoming and inspiring community for all and expect our code of conduct to be honored. Anyone who violates this code of conduct may be banned from the community.

## Attribution
The development team would like to acknowledge the people who have made direct contributions to the design and code in this repository. [CARMA Attribution](ATTRIBUTION.md) 

## License
By contributing to the Federal Highway Administration (FHWA) Connected Automated Research Mobility Applications (CARMA), you agree that your contributions will be licensed under its Apache License 2.0 license. [CARMA License](<docs/License.md>) 

## Contact
Please click on the CARMA logo below to visit the Federal Highway Adminstration(FHWA) CARMA website. For more information, contact CARMA@dot.gov.

[![CARMA Image](docs/image/CARMA_icon2.png)](https://highways.dot.gov/research/research-programs/operations/CARMA)
