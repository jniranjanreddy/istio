## What is Istio
Notes: to simulate as domain
## Bookinfo - https://istio.io/latest/docs/examples/bookinfo/
```
curl -H "Host:deepdive.com" http://x.x.x.x:31797    # <Node Pord>
```



```
Istio is a service mesh.

CRD - Customer Resource Definitions


Istio componentes
1. Pilot - Configuration Discovery
2. Citadel - Certificates
3. Galley - Configuration
4. Ingress Gateway

WHat does it do
  1. Service to service communication
```
```
How to install Istio
$ curl -L https://istio.io/downloadIstio | sh -
$ curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.14.1 TARGET_ARCH=x86_64 sh -

[root@k8s-helm ~]# curl -L https://istio.io/downloadIstio | sh -
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   101  100   101    0     0    108      0 --:--:-- --:--:-- --:--:--   108
  0     0    0     0    0     0      0      0 --:--:--  0:03:31 --:--:--     0
100  4926  100  4926    0     0     17      0  0:04:49  0:04:40  0:00:09  1176

Downloading istio-1.14.1 from https://github.com/istio/istio/releases/download/1.14.1/istio-1.14.1-linux-amd64.tar.gz ...

Istio 1.14.1 Download Complete!

Istio has been successfully downloaded into the istio-1.14.1 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /root/istio-1.14.1/bin directory to your environment path variable with:
         export PATH="$PATH:/root/istio-1.14.1/bin"

Begin the Istio pre-installation check by running:
         istioctl x precheck


[root@k8s-helm ~]# istioctl install --set profile=demo -y
v Istio core installed
v Istiod installed
v Egress gateways installed
v Ingress gateways installed
v Installation complete    

[root@k8s-helm ~]# kubectl label namespace default istio-injection=enabled
namespace/default labeled

root@dev-server01:~# k describe ns prod
Name:         prod
Labels:       istio-injection=enabled
              kubernetes.io/metadata.name=prod
Annotations:  <none>
Status:       Active

No resource quota.
No LimitRange resource.


[root@k8s-helm ~]# istioctl verify-install
1 Istio control planes detected, checking --revision "default" only
✔ ClusterRole: istiod-istio-system.istio-system checked successfully
✔ ClusterRole: istio-reader-istio-system.istio-system checked successfully
✔ ClusterRoleBinding: istio-reader-istio-system.istio-system checked successfully
✔ ClusterRoleBinding: istiod-istio-system.istio-system checked successfully
✔ ServiceAccount: istio-reader-service-account.istio-system checked successfully
✔ Role: istiod-istio-system.istio-system checked successfully
✔ RoleBinding: istiod-istio-system.istio-system checked successfully
✔ ServiceAccount: istiod-service-account.istio-system checked successfully
✔ CustomResourceDefinition: wasmplugins.extensions.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: destinationrules.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: envoyfilters.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: gateways.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: proxyconfigs.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: serviceentries.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: sidecars.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: virtualservices.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: workloadentries.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: workloadgroups.networking.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: authorizationpolicies.security.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: peerauthentications.security.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: requestauthentications.security.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: telemetries.telemetry.istio.io.istio-system checked successfully
✔ CustomResourceDefinition: istiooperators.install.istio.io.istio-system checked successfully
✔ ClusterRole: istiod-clusterrole-istio-system.istio-system checked successfully
✔ ClusterRole: istiod-gateway-controller-istio-system.istio-system checked successfully
✔ ClusterRoleBinding: istiod-clusterrole-istio-system.istio-system checked successfully
✔ ClusterRoleBinding: istiod-gateway-controller-istio-system.istio-system checked successfully
✔ ConfigMap: istio.istio-system checked successfully
✔ Deployment: istiod.istio-system checked successfully
✔ ConfigMap: istio-sidecar-injector.istio-system checked successfully
✔ MutatingWebhookConfiguration: istio-sidecar-injector.istio-system checked successfully
✔ PodDisruptionBudget: istiod.istio-system checked successfully
✔ ClusterRole: istio-reader-clusterrole-istio-system.istio-system checked successfully
✔ ClusterRoleBinding: istio-reader-clusterrole-istio-system.istio-system checked successfully
✔ Role: istiod.istio-system checked successfully
✔ RoleBinding: istiod.istio-system checked successfully
✔ Service: istiod.istio-system checked successfully
✔ ServiceAccount: istiod.istio-system checked successfully
✔ EnvoyFilter: stats-filter-1.11.istio-system checked successfully
✔ EnvoyFilter: tcp-stats-filter-1.11.istio-system checked successfully
✔ EnvoyFilter: stats-filter-1.12.istio-system checked successfully
✔ EnvoyFilter: tcp-stats-filter-1.12.istio-system checked successfully
✔ EnvoyFilter: stats-filter-1.13.istio-system checked successfully
✔ EnvoyFilter: tcp-stats-filter-1.13.istio-system checked successfully
✔ EnvoyFilter: stats-filter-1.14.istio-system checked successfully
✔ EnvoyFilter: tcp-stats-filter-1.14.istio-system checked successfully
✔ EnvoyFilter: stats-filter-1.15.istio-system checked successfully
✔ EnvoyFilter: tcp-stats-filter-1.15.istio-system checked successfully
✔ ValidatingWebhookConfiguration: istio-validator-istio-system.istio-system checked successfully
✔ Deployment: istio-ingressgateway.istio-system checked successfully
✔ PodDisruptionBudget: istio-ingressgateway.istio-system checked successfully
✔ Role: istio-ingressgateway-sds.istio-system checked successfully
✔ RoleBinding: istio-ingressgateway-sds.istio-system checked successfully
✔ Service: istio-ingressgateway.istio-system checked successfully
✔ ServiceAccount: istio-ingressgateway-service-account.istio-system checked successfully
✔ Deployment: istio-egressgateway.istio-system checked successfully
✔ PodDisruptionBudget: istio-egressgateway.istio-system checked successfully
✔ Role: istio-egressgateway-sds.istio-system checked successfully
✔ RoleBinding: istio-egressgateway-sds.istio-system checked successfully
✔ Service: istio-egressgateway.istio-system checked successfully
✔ ServiceAccount: istio-egressgateway-service-account.istio-system checked successfully
Checked 15 custom resource definitions
Checked 3 Istio Deployments
✔ Istio is installed and verified successfully
[root@k8s-helm ~]#

[root@k8s-helm istio-1.14.1]# kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
service/details created
serviceaccount/bookinfo-details created
deployment.apps/details-v1 created
service/ratings created
serviceaccount/bookinfo-ratings created
deployment.apps/ratings-v1 created
service/reviews created
serviceaccount/bookinfo-reviews created
deployment.apps/reviews-v1 created
deployment.apps/reviews-v2 created
deployment.apps/reviews-v3 created
service/productpage created
serviceaccount/bookinfo-productpage created
deployment.apps/productpage-v1 created
```

## Virtual Service
Virtual Service  - https://istio.io/latest/docs/reference/config/networking/virtual-service/
Destination Rule - https://istio.io/latest/docs/reference/config/networking/destination-rule/

## 3. Classic demo: Bookinfo
```
curl -L https://istio.io/downloadIstio | sh -
cd istio-* 
export PATH=$PWD/bin:$PATH
istioctl install --set values.pilot.env.PILOT_ENABLE_STATUS=true -y
kubectl label namespace default istio-injection=enabled --overwrite

kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml


minikube tunnel   # often needed for LoadBalancer in another terminal
# or
minikube service list
istioctl analyze


podman pull docker.io/istio/examples-bookinfo-productpage-v1:1.20.2
podman pull docker.io/istio/examples-bookinfo-ratings-v1:1.20.2
podman pull docker.io/istio/examples-bookinfo-reviews-v1:1.20.2
podman pull docker.io/istio/examples-bookinfo-reviews-v2:1.20.2
podman pull docker.io/istio/examples-bookinfo-reviews-v3:1.20.2


minikube image load docker.io/istio/examples-bookinfo-productpage-v1:1.20.2

minikube image load docker.io/istio/examples-bookinfo-reviews-v1:1.20.2



minikube image load docker.io/istio/examples-bookinfo-reviews-v2:1.20.2
minikube image load docker.io/istio/examples-bookinfo-reviews-v3:1.20.2

## Remove Istio
```
 istioctl manifest generate --set profile=demo | kubectl delete -f -
customresourcedefinition.apiextensions.k8s.io "authorizationpolicies.security.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "destinationrules.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "envoyfilters.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "gateways.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "peerauthentications.security.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "proxyconfigs.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "requestauthentications.security.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "serviceentries.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "sidecars.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "telemetries.telemetry.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "virtualservices.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "wasmplugins.extensions.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "workloadentries.networking.istio.io" deleted
customresourcedefinition.apiextensions.k8s.io "workloadgroups.networking.istio.io" deleted
serviceaccount "istio-egressgateway-service-account" deleted from istio-system namespace
serviceaccount "istio-ingressgateway-service-account" deleted from istio-system namespace
serviceaccount "istio-reader-service-account" deleted from istio-system namespace
```

```
<img width="1230" height="671" alt="image" src="https://github.com/user-attachments/assets/20b46187-3e35-4284-b9da-735f3364f381" />

<img width="1099" height="628" alt="image" src="https://github.com/user-attachments/assets/a228c1f7-dbd6-4495-aed5-b854a5cb3256" />

## Profiles
<img width="1057" height="504" alt="image" src="https://github.com/user-attachments/assets/7625e57f-6e34-437e-bb87-65adae76d7ff" />

## Labelling, after labeling, if any pod created, it will inject a envoy container.
##  kubectl label namespace kube-system istio-injection=enabled
<img width="1279" height="737" alt="image" src="https://github.com/user-attachments/assets/c64d31c3-2923-4cae-985b-e209becb49b2" />

## Traffic Management

<img width="949" height="595" alt="image" src="https://github.com/user-attachments/assets/aae1a65e-6597-4e9a-94a4-39d1555bce66" />

## Gateways
<img width="593" height="305" alt="image" src="https://github.com/user-attachments/assets/be70a9d2-2fce-45ba-bab1-c57f96c5f8e6" />

# Service Entry
<img width="587" height="321" alt="image" src="https://github.com/user-attachments/assets/f31cf6ef-8fc7-4b7a-b43b-3b954fbedac0" />

