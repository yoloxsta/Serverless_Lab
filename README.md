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
const consulUrl = 'http://54.174.253.62:8500';

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