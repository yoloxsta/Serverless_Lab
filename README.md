# Severless_Lab

https://github.com/ansarshaik965/AWS-SERVERLESS-DEPLOYMENT

https://youtu.be/pK52mfm69i0?si=sXG2qJwuPPr_uyzY

https://medium.com/@xiaolancara/using-aws-api-gateway-to-build-an-end-to-end-http-api-efd8fbd917c6 

https://loginov-rocks.medium.com/authorize-access-to-websocket-api-gateway-with-aws-signature-v4-f7e6b0e39f0a

https://youtu.be/L-C7bQM-OO8?si=stKSdcbg_Vdvy9Qe (Secure API Gateway using Lambda Authorizer : Hands-On (Part - 2))

https://youtu.be/xSKRyv08mo8?si=lkz-MJXIYSwQRi-L (Build Serverless Web Application on AWS | AWS Amplify)

https://medium.com/@inderjotsingh141/aws-serverless-hands-on-project-b678f69f5e98

##

## EFS
https://harsh05.medium.com/amazon-efs-a-comprehensive-guide-with-practical-steps-2c4a4b528fde

#

## Istio

https://praveendandu24.medium.com/mastering-istio-service-mesh-basics-a-comprehensive-guide-with-real-time-examples-6fbd6d6322ba#:~:text=Envoy%20is%20a%20high%2Dperformance,policies%20and%20collecting%20telemetry%20data.

https://ankanwrites.hashnode.dev/implementing-istio-for-microservices-management-a-how-to-guide

https://medium.com/@muppedaanvesh/getting-started-with-istio-a-hands-on-guide-for-beginners-0f73939e153a

https://medium.com/@eshant.sah/istio-in-simple-words-with-hands-on-34fef2b2735d 

https://jay75chauhan.medium.com/setting-up-istio-on-minikube-and-other-kubernetes-clusters-with-kiali-dashboard-17b9a1b22598

### VirtualService vs DestinationRule in Istio
- Both VirtualService and DestinationRule work together to control traffic in Istio, but they serve different purposes.
#### VirtualService (Traffic Routing)
- A VirtualService defines how incoming requests are routed to a service.
It specifies hostnames, traffic rules, path rewrites, weighted routing, retries, and fault injection.

🔹 Key Responsibilities:
- Defines routing rules based on path, headers, or other request properties.
- Supports traffic splitting (e.g., 80% to v1, 20% to v2).
- Performs URI rewriting and redirection.
- Attaches to a Gateway for ingress traffic.

🔹 Example VirtualService (Traffic Splitting 80-20)
```
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: myapp
spec:
  hosts:
  - "myapp.example.com"
  gateways:
  - myapp-gateway
  http:
  - match:
    - uri:
        prefix: /myapp
    route:
    - destination:
        host: myapp
        subset: v1
      weight: 80
    - destination:
        host: myapp
        subset: v2
      weight: 20

```

#### DestinationRule (Traffic Policies & Load Balancing)
- A DestinationRule defines traffic policies (e.g., load balancing, timeouts, connection pools) for a service after it has been routed by a VirtualService.

🔹 Key Responsibilities:
- Defines subsets of a service (e.g., v1, v2 based on labels).
- Configures load balancing (round-robin, least connections, etc.).
- Applies connection pooling (limits requests per connection).
- Controls failover & traffic policies.

🔹 Example DestinationRule (Defining v1 & v2 Subsets)
```
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: myapp
spec:
  host: myapp
  subsets:
    - name: v1
      labels:
        version: v1
    - name: v2
      labels:
        version: v2
  trafficPolicy:
    loadBalancer:
      simple: ROUND_ROBIN

```
🔹 Key Differences

| Feature      | VirtualService                | DestinationRule  |
|--------------|-----------------------------|---------|
| Purpose | Routes requests to the correct service	  | Defines traffic policies for routed requests |
| Traffic Splitting	 | ✅ Yes (e.g., 80% to v1, 20% to v2)  | ❌ No |
| Path-based Routing | ✅ Yes (e.g., /api → backend)	  | ❌ No |
| Subsets | ✅ References subsets  | ✅ Defines subsets (v1, v2) |
| Load Balancing | ❌ No	  | ✅ Yes (Round Robin, Least Connections, etc.) |
| Retries & Timeouts	 | ✅ Yes  | ✅ Yes |
| Connection Pooling	 | ❌ No  | ✅ Yes |

🔹 How They Work Together
- DestinationRule defines subsets (e.g., v1, v2).
- VirtualService routes traffic based on path, weight, or headers.
- Traffic flows through Istio’s Envoy proxies based on these rules.

🔹 Conclusion
- Use VirtualService to control request routing (paths, weights, retries).
- Use DestinationRule to define subsets and apply traffic policies.
#

## Monitoring

https://medium.com/@muppedaanvesh/a-hands-on-guide-to-kubernetes-logging-using-grafana-loki-%EF%B8%8F-b8d37ea4de13

https://aws.plainenglish.io/building-a-centralized-logging-solution-with-grafana-loki-7794c198d45c

https://medium.com/@abdulfayis/using-prometheus-loki-and-grafana-to-monitor-in-kubernetes-904dc7ac9143 

https://harshitsahu2311.hashnode.dev/mini-project-github-monitoring-using-grafana

https://readmedium.com/en/https:/alexandrev.medium.com/how-to-deploy-scalable-loki-on-kubernetes-592566be0982 

https://blog.devops.dev/aws-eks-monitoring-d94827a0c57f

## Ingress

https://aws.plainenglish.io/how-to-install-nginx-ingress-controller-in-aws-eks-6a15713ef4ab

```
kubectl patch svc prometheus-grafana -n prometheus-grafana -p '{"spec": {"type": "NodePort"}}'

kubectl patch svc nginx-ingress-ingress-nginx-controller -n ingress-nginx --type=merge -p "{\"spec\": {\"type\": \"NodePort\"}}"

kubectl patch ingress nginx-ingress -p '{"spec": {"ingressClassName": "nginx"}}' --type=merge

```
## Jfrog
https://narenchejara.medium.com/getting-started-with-jfrog-artifactory-ec5b58461ab1

https://medium.com/@riimoonriimoon/understanding-the-basics-of-jfrog-artifactory-8167ce582c86

https://blog.devops.dev/deployed-java-application-using-maven-sonarqube-jfrog-artifactor-jenkins-argocd-and-finally-ac25420dcdf4 (https://github.com/AmanPathak-DevOps/Scripts-Installation)

## Consul

https://www.skynats.com/blog/how-to-install-consul-on-ubuntu-24/ (sudo mkdir -p /etc/consul.d)

https://www.howtoforge.com/how-to-install-consul-server-on-ubuntu-22-04/

```
>app.js

npm init -y
npm install express

const express = require('express');
const app = express();
const port = 8080;

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.get('/health', (req, res) => {
  res.send('OK');
});

app.listen(port, () => {
  console.log(`App is listening on port ${port}`);
});

```
###

```
> discovery-app.js
npm init -y
npm install axios


const axios = require('axios');

// Consul server URL
const consulUrl = 'http://server-ip:8500';

async function discoverService() {
  try {
    // Query Consul to get details of the 'my-web-app' service
    const response = await axios.get(`${consulUrl}/v1/catalog/service/my-web-app`);
    const service = response.data[0];

    // Get the service's IP and port
    const serviceAddress = service.Address;
    const servicePort = service.ServicePort;

    // Print out the service discovery result
    console.log(`Discovered my-web-app at http://${serviceAddress}:${servicePort}`);

    // Optionally, make a request to the discovered service
    const appResponse = await axios.get(`http://${serviceAddress}:${servicePort}`);
    console.log('Response from my-web-app:', appResponse.data);
  } catch (error) {
    console.error('Error discovering service:', error);
  }
}

// Start service discovery
discoverService();

```
```
> my-web-app.json

{
  "ID": "my-web-app-1",
  "Name": "my-web-app",
  "Tags": ["web"],
  "Port": 8080,
  "Check": {
    "HTTP": "http://localhost:8080/health",
    "Interval": "10s"
  }
}


curl --request PUT \
--data @my-web-app.json \
http://server-ip:8500/v1/agent/service/register

```
### Graylog

https://blog.stackademic.com/centralize-logs-kubernetes-cluster-in-to-graylog-server-with-fluent-bit-log-collector-26c22e1b21f1

https://computingforgeeks.com/install-graylog-on-ubuntu-with-lets-encrypt/

https://www.cherryservers.com/blog/graylog-install-ubuntu

https://www.skynats.com/blog/how-to-install-graylog-on-ubuntu-24-04/

https://blog.stackademic.com/centralize-logs-kubernetes-cluster-in-to-graylog-server-with-fluent-bit-log-collector-26c22e1b21f1

https://medium.com/@kaant43/implementing-logging-in-nestjs-with-graylog-a-step-by-step-guide-4375004222f3

https://github.com/mouaadaassou/K8s-Graylog/blob/master/graylog-deploy.yaml (k8s)
```
sudo nano /etc/rsyslog.d/90-graylog.conf
*.* @server-IP:5140;RSYSLOG_SyslogProtocol23Format
sudo systemctl restart rsyslog

## Java-App

sudo apt install maven -y

mkdir GraylogJavaApp
cd GraylogJavaApp
mvn archetype:generate -DgroupId=com.example -DartifactId=GraylogJavaApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd GraylogJavaApp

>> pom.xml

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>GraylogJavaApp</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>GraylogJavaApp</name>
    <description>A simple Java application with Graylog logging</description>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- SLF4J API -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.36</version>
    </dependency>
       <!-- JUnit for testing -->
       <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
    </dependency>

        <!-- Graylog Gelf Logger -->
        <dependency>
            <groupId>de.siegmar</groupId>
            <artifactId>logback-gelf</artifactId>
            <version>3.0.0</version>
        </dependency>

        <!-- Logback Classic for logging -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.11</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>11</source>
                    <target>11</target>
                </configuration>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.2.0</version>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>com.example.App</mainClass>
                        </manifest>
                    </archive>
                </configuration>
        </plugin>
        <!-- Shade Plugin to create an executable JAR -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.3.0</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        </plugins>
    </build>
</project>

###

Create a new file src/main/resources/logback.xml and add:

<configuration>
    <appender name="GRAYLOG" class="de.siegmar.logbackgelf.GelfUdpAppender">
        <graylogHost>ip</graylogHost>  <!-- Graylog Server IP -->
        <graylogPort>12201</graylogPort>         <!-- Graylog GELF Port -->
        <includeRawMessage>true</includeRawMessage>
        <version>1.1</version>
    </appender>

    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="info">
        <appender-ref ref="GRAYLOG"/>
        <appender-ref ref="STDOUT"/>
    </root>
</configuration>

###
Edit src/main/java/com/example/App.java

package com.example;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class App {
    private static final Logger logger = LoggerFactory.getLogger(App.class);

    public static void main(String[] args) {
        logger.info("✅ Application Started!");
        logger.warn("⚠️ Warning log example");
        logger.error("❌ Error log example");

        for (int i = 1; i <= 5; i++) {
            logger.info("📢 Log message number " + i);
        }
    }
}

###

Run
mvn clean package
java -jar target/GraylogJavaApp-1.0-SNAPSHOT.jar

ls -lh target/
jar tf target/GraylogJavaApp-1.0-SNAPSHOT.jar META-INF/MANIFEST.MF

Testing > curl -X POST -H "Content-Type: application/json" -d '{"version":"1.1","host":"localhost","short_message":"Test message"}' http://ip:12201/gelf
```
### Signoz

https://teamoptimizers.hashnode.dev/signoz-a-complete-setup-tour-with-logs

https://github.com/SigNoz/signoz

https://medium.com/@karanjanthe/observability-monitoring-in-nodejs-using-signoz-0b804c1605ec

https://medium.com/@ifeomafayeorika/understanding-observability-with-signoz-b4675fcb035b

https://medium.com/@codewithalfredo/monitoring-in-production-a-guide-to-using-opentelemetry-with-nestjs-and-signoz-aeee59a8be0a

https://medium.com/@jjhayes100/signoz-16-000-stars-and-rising-835ac08d5341

### RDS Snapshot Sharing

https://medium.com/@kosnaramanakumar/how-to-share-and-restore-an-rds-cluster-with-default-kms-in-another-aws-account-c6f79ad09203 

###Flutter
```
flutter create -t app --platforms android,ios --org com.firstapp setup

```
#