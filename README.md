#git set origin url

# set git origin url
git remote set-url origin https://github.com/harshanaDisa/github-actions-gcp-demo.git


--------------------

Error: The v0 series of google-github-actions/setup-gcloud is no longer maintained. It will not receive updates, improvements, or security patches. Please upgrade to the latest supported versions: 

-------------------------------

Determining workspace structure

Deciding which workspace information to collect

Gathering workspace info

To create HTTPS for this deployment, you need to set up an SSL certificate for your service. This can be done using a Kubernetes Ingress with a cert-manager or using Google Cloud's managed SSL certificates if you're using Google Kubernetes Engine (GKE).

Here's a basic example of how you can set up an Ingress with a managed certificate on GKE:

```yaml
apiVersion: networking.gke.io/v1
kind: ManagedCertificate
metadata:
  name: example-certificate
spec:
  domains:
    - example.com
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    networking.gke.io/managed-certificates: example-certificate
spec:
  rules:
  - host: example.com
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: nginx
            port:
              number: 80
```

In this example, replace `example.com` with your domain name. This YAML file creates a ManagedCertificate resource and an Ingress that uses it. The Ingress routes traffic to your `nginx` service.

Please note that you need to have a domain name and it needs to be configured to point to the IP address of your Ingress. Also, the managed certificates can take some time to provision after you create the Ingress.

You can add this to your deployment process in the build-and-deploy.yaml file. After the `kubectl apply -f resources.yaml` command, you can apply the YAML file that contains your Ingress and ManagedCertificate.

Remember to replace `example.com` with your actual domain and `example-certificate` with a suitable name for your certificate.

This is a basic example and might need to be adjusted based on your specific needs and environment.



apiVersion: networking.gke.io/v1
kind: ManagedCertificate
metadata:
    name: example-certificate
spec:
    domains:
        - example.com
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
    name: example-ingress
    annotations:
        networking.gke.io/managed-certificates: example-certificate
spec:
    rules:
    - host: example.com
        http:
            paths:
            - pathType: Prefix
                path: "/"
                backend:
                    service:
                        name: nginx
                        port:
                            number: 80

-------------------------
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

helm install ingress-nginx ingress-nginx/ingress-nginx

kubectl delete ingressclass nginx
helm install ingress-nginx ingress-nginx/ingress-nginx


-----------------------------




