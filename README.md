# Severless_Lab

https://github.com/ansarshaik965/AWS-SERVERLESS-DEPLOYMENT

https://youtu.be/pK52mfm69i0?si=sXG2qJwuPPr_uyzY

https://medium.com/@xiaolancara/using-aws-api-gateway-to-build-an-end-to-end-http-api-efd8fbd917c6 

https://loginov-rocks.medium.com/authorize-access-to-websocket-api-gateway-with-aws-signature-v4-f7e6b0e39f0a

https://youtu.be/L-C7bQM-OO8?si=stKSdcbg_Vdvy9Qe (Secure API Gateway using Lambda Authorizer : Hands-On (Part - 2))

https://youtu.be/xSKRyv08mo8?si=lkz-MJXIYSwQRi-L (Build Serverless Web Application on AWS | AWS Amplify)

https://medium.com/@inderjotsingh141/aws-serverless-hands-on-project-b678f69f5e98

https://medium.com/@madithatisreedhar123/a-simple-e2e-cicd-application-with-aws-amplify-5898f9439a35

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

https://youtu.be/FgkSZbfkpCI?si=COYbqGpZghE7J2Oa

https://medium.com/@tylerauerbeck/metallb-and-kind-loads-balanced-locally-1992d60111d8 (metal-lb)

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

https://medium.com/@nikitasharma1342/exploring-service-discovery-with-consul-a-practical-example-dfedacf1d465 

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

https://medium.com/@gayatripawar401/implementation-of-an-opensource-apm-tool-using-signoz-and-opentelemetry-6c3cebea919e

```
npm init -y
npm install express
npm install @opentelemetry/sdk-node @opentelemetry/auto-instrumentations-node @opentelemetry/exporter-trace-otlp-http


> index.js

require('./tracing');

const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello from Node.js with OpenTelemetry!');
});

app.listen(3000, () => {
  console.log('App listening on port 3000');
});

> tracing.js

// tracing.js
const { NodeSDK } = require('@opentelemetry/sdk-node');
const { OTLPTraceExporter } = require('@opentelemetry/exporter-trace-otlp-http');
const { getNodeAutoInstrumentations } = require('@opentelemetry/auto-instrumentations-node');

const sdk = new NodeSDK({
  traceExporter: new OTLPTraceExporter({
    url: 'https://ingest.us.signoz.cloud:443/v1/traces',
    headers: {
      'signoz-access-token': '******', // <-- your actual key here
    },
  }),
  instrumentations: [getNodeAutoInstrumentations()],
});

sdk.start();

>> node index.js
```
#### for signoz metric
```
npm install @opentelemetry/exporter-metrics-otlp-http

> tracing.js

const { NodeSDK } = require('@opentelemetry/sdk-node');
const { getNodeAutoInstrumentations } = require('@opentelemetry/auto-instrumentations-node');

const { OTLPTraceExporter } = require('@opentelemetry/exporter-trace-otlp-http');
const { OTLPMetricExporter } = require('@opentelemetry/exporter-metrics-otlp-http');
const { PeriodicExportingMetricReader } = require('@opentelemetry/sdk-metrics');

const traceExporter = new OTLPTraceExporter({
  url: 'https://ingest.us.signoz.cloud:443/v1/traces',
  headers: {
    'signoz-access-token': '05bd*****4cc3',
  },
});

const metricExporter = new OTLPMetricExporter({
  url: 'https://ingest.us.signoz.cloud:443/v1/metrics',
  headers: {
    'signoz-access-token': '05bd*****4cc3',
  },
});

const sdk = new NodeSDK({
  traceExporter,
  metricReader: new PeriodicExportingMetricReader({
    exporter: metricExporter,
    exportIntervalMillis: 10000,
  }),
  instrumentations: [getNodeAutoInstrumentations()],
});

sdk.start();


```
## RDS Snapshot Sharing

https://medium.com/@kosnaramanakumar/how-to-share-and-restore-an-rds-cluster-with-default-kms-in-another-aws-account-c6f79ad09203 

###Flutter
```
flutter create -t app --platforms android,ios --org com.firstapp setup

```
## ELK

- https://medium.com/@muppedaanvesh/a-hands-on-guide-to-kubernetes-logging-using-elk-stack-filebeat-part-4-%EF%B8%8F-48e233443961

- https://surajsoni3332.medium.com/setting-up-elk-stack-on-kubernetes-a-step-by-step-guide-227690eb57f4

- https://adex.ltd/elk-stack-deployment-on-kubernetes-with-helm-charts

- https://dzone.com/articles/how-to-deploy-the-elk-stack-on-kubernetes

- https://readmedium.com/en/https:/blog.devops.dev/installing-elasticsearch-with-logstash-kibana-and-apm-using-elastic-cloud-on-kubernetes-operator-f214130bf199

- https://www.linode.com/docs/guides/how-to-deploy-the-elastic-stack-on-kubernetes/

- https://phoenixnap.com/kb/elasticsearch-helm-chart (Minikube)

- https://medium.com/@davis.angwenyi/how-to-install-elastic-search-using-helm-into-kubernetes-de1fb1011076
### Hello World (Frontend-backend-kind)

```
- Frontend/

> index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Frontend</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        button {
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
        }
        #response {
            margin-top: 20px;
            font-size: 24px;
            color: #333;
        }
    </style>
</head>
<body>
    <h1>Frontend</h1>
    <button onclick="callBackend()">Click me!</button>
    <p id="response"></p>

    <script>
        function callBackend() {
            fetch('/api/')
                .then(response => response.text())
                .then(data => {
                    document.getElementById('response').innerText = data;
                })
                .catch(error => {
                    document.getElementById('response').innerText = 'Error: ' + error;
                });
        }
    </script>
</body>
</html>

> nginx.conf

events {}
http {
  server {
    listen 80;

    location / {
      root /usr/share/nginx/html;
      index index.html;
    }

    location /api/ {
      proxy_pass http://backend-service:8080/;
    }
  }
}

> Dockerfile

FROM nginx:alpine

# Copy the app code to the appropriate NGINX directory
COPY . /usr/share/nginx/html

# Copy the custom NGINX config
COPY nginx.conf /etc/nginx/nginx.conf

>> docker build -t frontend:latest .
  kind load docker-image frontend:latest --name metallb-kind

- Backend

> main.go

package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "Hello from Backend")
}

func main() {
	http.HandleFunc("/", handler)
	http.ListenAndServe(":8080", nil)
}

> Dockerfile

FROM golang:1.21-alpine
WORKDIR /app
COPY . .
RUN go build -o main .
CMD ["./main"]

> backend.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
      - name: backend
        image: backend:latest
        imagePullPolicy: Never
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  selector:
    app: backend
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
  type: ClusterIP


> frontend.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
      - name: frontend
        image: frontend:latest
        imagePullPolicy: Never
        ports:
        - containerPort: 80

---
apiVersion: v1
kind: Service
metadata:
  name: frontend-service
spec:
  type: NodePort
  selector:
    app: frontend
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30000

>>> docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps -f name=kind-control-plane -q)

```
## EKS-EBS
- https://harsh05.medium.com/simplifying-persistent-storage-in-amazon-eks-with-amazon-ebs-6516474159f3

- https://medium.com/turknettech/how-to-use-ebs-and-efs-in-aws-eks-part-1-ebs-3508cb2cf1c4

- https://medium.com/turknettech/how-to-use-ebs-and-efs-in-aws-eks-part-2-efs-35d5dba5a387

- https://medium.com/@chrisdevops/this-is-a-short-guide-to-set-up-dynamic-volume-provisioning-on-an-aws-eks-cluster-16a48d1f8c74

- https://youtu.be/JWi6lFUpSuw?si=g5qU0lJp38OLmjuT

- https://youtu.be/B0CGyboZnjg?si=yZqg7fmb3V9bxDSF

- https://freedium.cfd/https://awstip.com/the-need-for-ebs-csi-driver-in-amazon-eks-and-full-setup-276958b0a8c8

## Prod-EKS

- https://medium.com/@alex-tsvetkov/how-to-create-a-production-ready-eks-cluster-on-aws-using-terraform-part-1-vpc-e7e08d8045bb

- https://blog.stackademic.com/configuring-production-ready-eks-clusters-with-terraform-and-github-actions-c046e8d44865

- https://blog.searce.com/optimizing-external-and-internal-access-to-multiple-kubernetes-services-in-eks-with-nginx-ingress-7c27d9fe937f (Ingress-EKS)

- https://youtu.be/FgkSZbfkpCI?si=u7vuOqv4hEZndcCH (Nlb ingress)

- https://awswithatiq.com/how-to-create-an-nginx-ingress-controller-with-aws-classic-load-balancer/

## Cognito

- https://medium.com/@jith/a-practical-introduction-to-aws-lambda-api-gateway-cognito-dynamo-db-s3-hosting-and-60002b22947a

## OpenTelementry

- https://medium.com/@kedarnath93/understanding-opentelemetry-with-demo-example-d7991a4fc237

- https://www.linkedin.com/posts/nasiullha-chaudhari_otel-app-project-step-by-step-document-activity-7232614782866980864-bsMb/?utm_source=share&utm_medium=member_desktop

- https://medium.com/@codewithalfredo/monitoring-in-production-a-guide-to-using-opentelemetry-with-nestjs-and-signoz-aeee59a8be0a

### Signoz note 
```
OTEL_LOGS_EXPORTER=otlp \
OTEL_EXPORTER_OTLP_ENDPOINT="https://ingest.us.signoz.cloud:443" \
OTEL_EXPORTER_OTLP_HEADERS="signoz-access-token=***********" \
OTEL_RESOURCE_ATTRIBUTES=service.name=spring-petclinic \
java -javaagent:/mnt/c/Users/soetintaung/Downloads/opentelemetry-javaagent.jar -jar target/*.jar

- https://github.com/orgs/SigNoz/repositories

- https://dev.to/infrasity-learning/observability-with-signoz-for-java-app-16oe

```
## Domain
- https://towardsaws.com/how-to-add-a-domain-with-amazon-route-53-fc4452fa2b60

- https://medium.com/@lukwagoasuman236/step-by-step-guide-to-getting-an-ssl-tls-certificate-9d027856dec3

### Ansible
- https://medium.com/@a_tsai5/creating-an-ec2-instance-using-ansible-764cf70015f6

- https://medium.com/@somashekarvedadevops/ansible-control-node-manage-nodes-setup-657af3c6e163

- https://blog.devops.dev/simple-ansible-hands-on-project-on-aws-ec2-instances-dad09f9ee521

```
🔹 Connect to control node:
ssh -i my-key.pem ec2-user@<control-node-ip>
🔹 On control node, upload the key:
scp -i my-key.pem my-key.pem ec2-user@<control-node-ip>:~
chmod 400 ~/my-key.pem

✅ Example hosts.ini for Ansible:

[webservers]
host1 ansible_host=ip ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/ansible.pem
host2 ansible_host=ip ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/ansible.pem

--- install_git.yml

- name: Install Git on web servers
  hosts: webservers
  become: yes
  tasks:
    - name: Install Git
      package:
        name: git
        state: present
###

ansible-playbook -i hosts.ini install_git.yml

```
## Kong
- https://medium.com/api-leadership/expose-backend-api-using-kong-gateway-step-by-step-guide-fcd3aeeaba73

## EFS

- https://linuxbeast.com/blog/how-to-mount-amazon-efs-on-ec2-ubuntu-22-04-instance/

## Let Encrypt

- https://youtu.be/uEAzcLw_nSI?si=9UNQ4jJXrSS9LXiB

## Action (self-hosted)

- https://ougabriel.medium.com/how-to-configure-self-hosted-runners-for-your-ci-cd-pipelines-using-gitactions-fcaf516bef3a

- https://blog.stackademic.com/how-to-create-a-self-hosted-github-action-runner-and-run-a-workflow-on-it-0607694bf257

- https://faun.pub/continuous-integration-of-java-project-with-github-actions-7a8a0e8246ef

- https://shrihariharidas73.medium.com/deploying-a-simple-web-application-to-aws-ecs-with-github-actions-and-terraform-dd57200baa50

## Site to Site VPN 

- https://medium.com/@jeff.turner0590/accelerated-vpn-site-to-site-vpn-step-by-step-guide-f6f09a9197d2

- https://medium.com/@sruthianem89/project-10-implementing-a-site-to-site-vpn-in-aws-ef822e736277

- https://youtu.be/XonAC_Z9s8Y?si=1kY_6hg5Lv5mA0Gz

- https://youtu.be/h6YuZ9k9nzo?si=oWy6G4Oil7gsxzrv

## NAT

- https://medium.com/@shubhamchavan4554/mastering-private-subnet-connectivity-aws-nat-gateway-guide-a35ecfd30190

## SSL Case

- https://www.youtube.com/watch?v=DEkygFyNbQg  

## Dockerfile

```
- node

# Stage 1: Install Dependencies
FROM node:16.15-alpine as base
WORKDIR /base
COPY package*.json yarn.lock ./
RUN NOPOSTINSTALL=1 yarn install --frozen-lockfile

# Stage 2: Build
FROM base as build
WORKDIR /build
COPY . .
# RUN cp /build/cicd/prod/.env.example .env
COPY --from=base /base ./
RUN yarn cache clean && yarn build

# Stage 3: Running Prod
FROM nginx:alpine as prod
COPY --from=build /build/dist /usr/share/nginx/html

# overrides default nginx conf
COPY nginx.conf /etc/nginx/conf.d
RUN rm /etc/nginx/conf.d/default.conf; exit 0

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

---
FROM maven:3.8.5-openjdk-17 as build

WORKDIR /build
COPY . .

RUN mvn clean install -Dmaven.test.skip=true -f /build/pom.xml



FROM openjdk:17.0.1-slim
COPY --from=build /build/target/*.jar app.jar
CMD java   -Duser.timezone=+06:30 -jar app.jar --spring.config.location=file:/deployment/config/application.properties

---

#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base

COPY . App/
WORKDIR /App
ENV TZ="Asia/Yangon"
ENTRYPOINT ["dotnet", "wxyz.UI.dll"]
```

## Homework

- https://github.com/chyke007/Yum-food

- https://github.com/realexcel2021/3-tier-Architecture-design

- https://sheriffexcel.hashnode.dev/3-tier-architecture-on-aws-using-terraform (iac day-01)