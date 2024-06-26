---
layout: post
title:  "Kubernetes"
date:   2024-05-11
categories: infra
permalink: /:categories/kubernetes
---


<p><a href="#wit">What is it?</a> > <a href="#arch">Architecture</a> > <a href="#pod">Pod</a> > <a href="#rs">ReplicaSet</a> > <a href="#sa">Special Attributes</a> > <a href="#deploy">Deployment</a> > <a href="#ds">Deployment Strategy</a> > <a href="#svc">Service</a> > <a href="#ingress">Ingress</a> >  <a href="#netpolicy">Network Policy</a> > <a href="#net">Network</a> > <a href="#volume">Volume</a> > <a href="#ns">Namespace</a> > <a href="#secret">Secrets</a> > <a href="#sacc">Service Account</a> > <a href="#att">Affinity, Taints and Tolerations</a> > <a href="#security">Security</a> > <a href="#cronjob">CronJob</a> > <a href="#hon">Hands-On</a> </p>



<br />
<h2>Introduction</h2>
<h3 id="wit">What is it?</h3>

<p style="text-align: justify;">The tradicional deployment didn't scale the resource and it impact in the cost. Another alternative of deployment is the virtualiation, that isolate the apps. It is a better utilization of resources and scalability but each VM represents a enteire machine. Using containers as the third alternative is possible to have the isolation of the application and share the other resources secondary to the application. Also, the cycle of deployment is easear to handle. This last solution is considered lightweight.</p>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/overview/">kubernetes</a> or K8s comes as solution for container orchestration that <em>provides a framework to run distributed systems resiliently, takes care of scaling and failover for your application and provides deployment patterns.</em> It is a container orchestration technology. It orchestrates the deplyment and management of containers. The containers can be managed by <a href="https://fabiana2611.github.io/infra/docker">Docker</a>. Some of features available are: Service discovery and load balancing, Storage orchestration, Automated rollouts and rollbacks, Secret and configuration management, Horizontal scaling, IPv4/IPv6 dual-stack, etc. </p>

<h3 id="arch">Architecture</h3>

<p style="text-align: justify;"><b><a href="https://kubernetes.io/docs/concepts/architecture/nodes/">Node</a></b> is a machine where K8s is intalled. It includes kubelet, container runtime and kube-proxy. They are managed by the <a href="https://kubernetes.io/docs/reference/glossary/?all=true#term-control-plane">control plane</a>.</p>

<p style="text-align: justify;"><b>Cluster</b> is a group of Nodes managed to keep the application available even if one node fails. That management is done by a node called <b>Master</b>. This node is configured to have the information about the other nodes and manage them. It is responsible for the orchestration of the containers.</p>

<p style="text-align: justify;">Components in Node Master, the orchestrator <a href="https://kubernetes.io/docs/concepts/overview/components/#control-plane-components">[Control Plane Componenets]</a>:</p>
<ul>
  <li><a href="https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver">kube-apiserver:</a> it is between K8s and external Node communication. It communicates with Worker Node by kubelet.</li>
  <li><a href="https://kubernetes.io/docs/concepts/overview/components/#etcd">etcd:</a> is respnsible to store all data used to manage the cluster to be used by K8s. For instance, it implements locks to avoid conflicts between masters.</li>
  <li><a href="https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler">Scheduler:</a> responsible for distributing work or containers across multiple nodes.</li>
  <li>Controller <a href="https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager">[kube-controller-manager]</a><a href="https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager">[cloud-controller-manager]</a>: the brain behind the orchastration - noticing and responding when nodes, containers or endpoints goes down. It makes decisions to bring up new containers</li>
</ul>

<p style="text-align: justify;">Components in worker nodes <a href="https://kubernetes.io/docs/concepts/overview/components/#node-components">[Node Components]</a><:/p>
<ul>
  <li><a href="https://kubernetes.io/docs/concepts/overview/components/#container-runtime">Container Runtime:</a> software used to run container (e.g Docker).</li>
  <li><a href="https://kubernetes.io/docs/concepts/overview/components/#kubelet">kublet:</a> agent that runs on each node in the cluster. It is responsible that the containers are running on the nodes as expected</li>
  <li><a href="https://kubernetes.io/docs/concepts/overview/components/#kubelet">kube-proxy:</a> is a network proxy that runs on each node of the cluster, and maintains network rules on nodes. It allows the network communication to the Pods in the cluster</li>
</ul>

<p><center>
  <img src="/img/kubernetes/kube-arch.png" height="100%" width="100%">
</center></p>

<br />
<h2>Basic Concepts</h2>

<p>A note before we start this journey: be aware kubernetes allow two ways to manage the objects. The first one is <a href="https://kubernetes.io/docs/tasks/manage-kubernetes-objects/declarative-config/">declarative</a> that use file definitions;  and <a href="https://kubernetes.io/docs/tasks/manage-kubernetes-objects/imperative-command/">imperative</a>, that use command line directy.</p>

<h3 id="pod" >Pod</h3>
<p style="text-align: justify;">
<a href="https://kubernetes.io/docs/concepts/workloads/pods/">Pod</a> is a kubernate object that represents a deployable unit of a set of containers. The containers are encapsulated into the Pod that run an instance of the application. If you need to increase the application with more Pods then you need increase the replication number (scale up). To have an application in a Pod is assumed that the application is already developed and built into an images and it is available in some repository. Also assume that the Kubernetes cluster has set up and working. The Pod can have more than one container (only one instance), but the best practices is to have only one container by Pod. </p>

{% highlight ruby %}
// Declarative
$ kubectl create -f pod-definition.yaml // Declarative
// Extract the pod definition
$ kubectl get pod webapp -o yaml > pod-definition.yaml // edit
// Create a file from imperative before create
$ k run mypod --image=nginx:alpine --dry-run=client -o yaml > mypod-definition.yaml

// Imperative
$ kubectl run nginx --image=nginx.      
$ kubectl run custom-nginx --image=nginx --port=8080
$ kubectl run redis --image=redis:alpine --labels="tier=db"
$ kubectl run hello-minikube
$ kubectl cluster-info
$ kubectl get nodes
$ kubectl get pods

// Copy the logs
$ k logs mypod > /opt/mypod.logs
{% endhighlight %}

<p><center>
  <img src="/img/kubernetes/pod.png" height="50%" width="50%">
</center></p>

<p style="text-align: justify;">A special feature to Pods is the <a href="https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/">Pod Initialization</a>. <em>It uses an Init Container to initialize a Pod before an application Container runs.</em></p> 

<p>Any trouble with your pod you can <a href="https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/">Debug Pod</a> and <a href="https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/">Debug Running Pod</a>.</p>

<h3 id="rs">ReplicaSet</h3>
<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/">ReplicaSet</a> maintain a stable set of replicas running at any given time. it is used to guarantee the availability of a specified number of identical Pods. Then, it ensures high availability and handle loads across the pods (load balancing). Even the Pods already created, it's possible to scale that number.</p>

{% highlight ruby %}
$ kubectl get replicaset
$ kubectl replace -f replicaset-definition.yaml 
$ kubectl edit rs new-replica-set
$ kubectl scale -replicas=6 -f replicaset-definition.yaml 
$ kubectl scale rs new-replica-set --replicas=6 
{% endhighlight %}

<p><center>
  <img src="/img/kubernetes/replicaset.png" height="50%" width="50%">
</center></p>

<h3 id="sa">Special Attributes</h3>
<ul>
  <li><a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/">Labels and selectors:</a> the objects in kubernates have labels to be used to monitor that objects. For selector, the 'matchLabels' are used to filter the objects. The idea of selectors is to have flexibility when it comes to expressing which other resource be connected to or controlled by other resource.</li>
  <li><a href="https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/">Environment Variables:</a> It's possible to use env attributes to add the variables to be used. It can be a direct key-value pair or doing a reference to a external file.</li>
  <li><a href="https://kubernetes.io/docs/concepts/configuration/configmap/">ConfigMap:</a> it is a key-value pair configuration used as more organized way to create the configuration using separated files.<br />
    {% highlight ruby %}
    $ k create cm myconfigmap --from-literal=DB_NAME=SQLDB --from-literal=DB_HOST=localhost
    {% endhighlight %}
  </li>
</ul>

<h3 id="deploy">Deployment</h3>
<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/workloads/controllers/deployment/">Deployment</a> build the desired state. A Deployment provides declarative updates for Pods and ReplicaSets. It allow edit any field/property of the POD template. After the change, the deployment will automatically delete and create a new pod with the new changes. The deployment can be <a href="https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment">rollback</a> when the deployment is not stable. Also, you can <a href="https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-a-deployment">scale</a> the deployment if you need increase or decrease the replicas. If you delete the deployment object, the others object created by it will be deleted (e.g., pods and replicase).</p>

{% highlight ruby %}
// CREATE
// Declarative
$ kubectl create -f deployment-definition.yaml                
$ k create deploy mydeploy --image-nginx --dry-run=client -oyaml > deploy-def.yaml

// Imperative
$ kubectl create deployment nginx --image=nginx               
$ kubectl create deployment nginx --image=nginx --replicas=4

$ kubectl scale deployment/nginx --replicas=2 // update the replicas
$ kubetcl get deployments
$ kubectl get all

// UPGRADE - StrategyType attribute (First step is created a new replicaSet)
$ kubectl edit deployment my-deployment                // Change definition directly
$ kubectl apply –f deployment-definition.yml           // Create or update
$ kubectl replace –f deployment-definition.yml --force // delete and replace the pods
$ kubectl set image deployment/myapp-deployment nginx-container=nginx:1.9.1

// ROLLBACK (destroy the pods and go back with the olders)
$ kubectl rollout undo deployment/myapp-deployment
$ kubectl rollout status deployment/myapp-deployment
$ kubectl rollout history deployment/myapp-deployment
{% endhighlight %}

<p><center>
  <img src="/img/kubernetes/deployment.png" height="100%" width="100%">
</center></p>

<h3 id="ds">Deployment Strategy</h3>
<p style="text-align: justify;">The kubernetes allows to use different <a href="https://spot.io/resources/kubernetes-autoscaling/5-kubernetes-deployment-strategies-roll-out-like-the-pros/">Strategy</a> that define how the application should be updated. When you create a deployment, it triggers the deployment process. Also, it creates a new Deployment revision. A fancy diagrame comparing the strategies you can see <a href="https://www.linkedin.com/pulse/kubernetes-deployment-strategies-ahmad-rahimian-t2lue/">here</a>.</p>

<ul>
  <li>Rolling deployment: replace the pods one by one</li>
  <li>Recreate: terminate all the pods and replace all the pods</li>
  <li>Canary: progressivelly delivery - change the traffic step by step</li>
  <li>Blue/Green: replicate the environment</li>
</ul>

<h3 id="net">Network</h3>

<p style="text-align: justify;">When the K8s is configured it creates an internal private network and attache all PODs. The Pods will have an IP when they are deployed.</p>

<h3 id="svc">Service</h3>
<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/services-networking/service/">Service:</a> <em> Expose an application running in your cluster behind a single outward-facing endpoint.</em> Pods have an internal IP but it cannot be used to access the Pod outside of the cluster. Beside, the IP changes always when a Pod is replaced. The service groups Pods with a shared IP which will not change, and that address can be exposed internally and externally of the custer, what allow the Pods be accessible outside of the cluster.</p>

<p>Types of services <a href="https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types">[1]</a><a href="https://www.densify.com/kubernetes-autoscaling/kubernetes-service-load-balancer/">[2]</a><a href="https://medium.com/@extio/demystifying-kubernetes-service-a-reliable-and-scalable-solution-for-modern-application-deployment-646f078f45a1">[3]</a><a href="https://medium.com/devops-mojo/kubernetes-service-types-overview-introduction-to-k8s-service-types-what-are-types-of-kubernetes-services-ea6db72c3f8c
">[4]</a></p>
<ul>
  <li>ClusterIP: expose only inside the cluster (defaut). There are virtual IP to allow communication between them, e.g, frontend and backend inside the cluster.</li>
  <li>NodePort: Exposes the Service on each Node's IP at a static port (the NodePort). It makes the pod available outside of the node mapping the port on Node (NodePort - 30000 to 32767) to the port on the Pod (TargetPort).</li>
  <li>LoadBalancer: Exposes the Service externally using an external load balancer</li>
</ul>

{% highlight ruby %}
$ kubectl create service nodeport jekyll-node-service --tcp=8080:4000 --node-port=30097 -n development
$ kubectl expose pod redis --port=6379 --name redis-service       // example 1
$ kubectl run httpd --image=httpd:alpine --port=80 --expose=true  // example 2
$ kubectl get svc
$ kubectl cluster-info // get list of URLs of services running in the cluster
{% endhighlight %}

<p>Any trouble with your service you can <a href="https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/">Debug Service</a>.</p>

<p><center>
  <img src="/img/kubernetes/service.png" height="100%" width="100%">
</center></p>


<h3 id="ingress">Ingress</h3>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/services-networking/ingress/">Ingress</a> <em>is an API object that manages external access to the services in a cluster. Traffic routing is controlled by rules defined on the Ingress resource.</em> The <a href="https://medium.com/@onai.rotich/services-and-ingress-7afc517f2ec6">difference between service and ingress</a>is that service create a single point of access to a group of pods, and ingress expose multiple services using one IP through rules that define the graphic. A good example you can see <a href="https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/">here</a>.</p>


<h3 id="netpolicy">Network Policy</h3>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/services-networking/network-policies/">Network Policy</a> can be used to control the traffic.</p>

<h3 id="volume">Storage</h3>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/storage/volumes/">volume</a> is a directory which is accessible to the containers in a pod. The volume persists even if container restart. However, the volumes are removed when the Pods are destroyed. Considering One-Node environment, the hostPath property helps to keep the data visible for that Node.</p>

<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/storage/persistent-volumes/">Persistent Volume</a> is a volume in the cluster with the lifecycle independent of the Pod. Persistent Volume Claim is a request for storage by user.</p>

<p><center>
  <img src="/img/kubernetes/storage.png" height="50%" width="50%">
</center></p>

<h3 id="ns">Namespace</h3>
<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/">Namespace:</a> mechanism for isolating groups of resources (pods, rs, jobs, deployments, svc, secrets, roles, rolebinding, configmaps, PVC) within a single cluster. However, some resources (e.g Node, PV clusterroles, namespaces, clusterbindings) are cluster scope and cannot be grouped.</p>

{% highlight ruby %}
$ kubectl get namespaces
$ kubectl create -f namespace-dev.yaml
$ kubectl create namespace dev
$ kubetcl get pods --namespace=dev
$ kubetcl get pods --all-namespaces kubetcl get pods -A
$ kubectl delete deploy redis-deploy -n dev-ns
{% endhighlight %}

<p><center>
  <img src="/img/kubernetes/namespace.png" height="70%" width="70%">
</center></p>

<h3 id="secret">Secret</h3>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/configuration/secret/">Secrets</a> objects are used to store sensitive data which is done in an encoded format. It is created independent of the Pod. You can see different ways of manage the secrets <a href="https://kubernetes.io/docs/tasks/configmap-secret/">here</a>.</p>

{% highlight ruby %}
$ echo –n ‘mysql’ | base64
$ echo –n ‘bXlzcWw=’ | base64 --decode

// Imperative
kubectl create secret generic app-secret \
  --from-literal=DB_User=root \
  --from-literal=DB_Password=paswrd

// Declarative 
$ kubectl create -d secret.yaml

$ kubectl get secrets
$ kubectl describe secrets
{% endhighlight %}

<h3 id="sacc">Service Account</h3>
<p style="text-align: justify;"><a href="">Service Account</a> is an account to allow the communication machine-to-machine. When it is created, a token is generated inside a secret object. <em>When you create a cluster, Kubernetes automatically creates a ServiceAccount object named default for every namespace in your cluster</em>.</p>

{% highlight ruby %}
kubectl create serviceaccount my-sa
kubectl get serviceaccount
kubectl describe serviceaccount my-sa
kubectl describe secret my-sa-token-kbbdm
{% endhighlight %}


<h3 id="att">Affinity, Taints and Tolerations</h3>

<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity">Node affinity</a> is applied to Node and allow to constrain which nodes a Pod can be scheduled on based on node labels.</p>

<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/">Taints</a> are applied to node and allow a node to repel a set of pods.</p>

<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/">Tolerations</a> are applied to pods. Tolerations allow the scheduler to schedule pods with matching taints.</p>


<h3 id="security">Security</h3>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/security/">Security</a> is an important topic in K8s. The kube-apiserver is the first point of defense because it is the point of communication in the cluster. By default, all ports can access all other ports, allowing the communication between Pods inside the custer. It can be restricted by Network Policies.</p>
</p>

<ul>
  <li>Authentication (Who can access): static pwd and token file (deprecated 1.19), certification, LDAP, service account</li>
  <li>Authorization (what they can do): Node, RBAC, ABAC, Node authorization, Webhook mode</li>
</ul>

<p><center>
  <img src="/img/kubernetes/security.png" height="100%" width="100%">
</center></p>

<p style="text-align: justify;">The service account is managed by K8s but the other users are managed by a third system like LDAP or Okta. The K8s uses the details or certificate to validate them. </p>

<p><u><a href="https://kubernetes.io/docs/reference/config-api/kubeconfig.v1/">1 KubeConfig file</a></u></p>

<p style="text-align: justify;">This file has the credentials and there are three section: cluster (it has the server specification), users (it has keys and certification) and context (which user has access to which cluster). Pay attention that is using users that already exist. </p>

{% highlight ruby %}
// FILE - $HOME/.kube/config
$ kubectl config view 

// COMMANDS
$ kubectl get pods --kubeconfig config
$ kubectl config view // it will omit the secrets
$ kubectl config use-context colima
{% endhighlight %}

<p><u><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.30/#api-groups">2 API Group</a></u></p>

<p style="text-align: justify;">The K8s API has different groups to manipulate the resources. For instace in '/api' endpoint there is the core group where you will find the core funcionalities (pods, namespace, rs, pv, etc). The '/apis'  you will find the named group where you will find extension, apps, networking.k8s.io, storage.k8s.io, etc.</p>

<p><u><a href="https://kubernetes.io/docs/reference/access-authn-authz/authorization/">3 Authorization</a></u></p>

<p style="text-align: justify;">It will happen after the authentication. Then, API server validates if the request is allowed or not based on requests attributes and policies, and eventually some external services. The authorization modes are:</p>

<ul>
  <li>Node Authorized: Kublet access kube API to read services, endpoints, Nodes,Pods; and Write Node status, Pod status and events</li>
  <li>ABAC: external access for the API; create API with policies; any changes in those files is necessary to restart the <a href="https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/">kube-apiserver</a></li>
  <li>RBAC: Define Roles instead of associate a user or group to a set of permissions.</li>
  <li>Webhook: external policies</li>
  <li>AlwasyAllow is the default.</li>
  <li>AlwasyDeny blocks all requests.</li>
</ul>

{% highlight ruby %}
// Check acess:
$ kubectl auth can-i create deployments
$ kubectl auth can-i delete nodes
$ kubectl auth can-i create deployments --as dev-user
$ kubectl auth can-i create deployments --as dev-user --namespace test

// Identify auth mode configured in the cluster
$ cat /etc/kubernetes/manifests/kube-apiserver.yaml // ps -aux | grep authorization

// roles in all namespaces
$ kubectl get roles -A --no-headers | wc -l

//  Identify an account in a specific role in a namespace
$ kubectl get roles
$ kubectl describe rolebindings MY_ROLEBINDING -n MY_NS

// A specific user has access to GET pods
$ kubectl get pods --as dev-user

// Permission to the user1 to create, list and delete pods in the default namespace.
$ kubectl create role dev --verb=list,create,delete --resource=pods
$ kubectl describe role dev
$ kubectl create rolebinding user-binding --role=dev --user=user1
$ kubectl describe rolebinding user-binding
{% endhighlight %}


<p style="text-align: justify;"><u><a href="https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/kubectl_create_clusterrole/">3 Cluster Role</a></u></p>

<p style="text-align: justify;">It is used to give permissions in cluster scopes like view, create or delete Nodes. (e.g cluster admin). </p>

{% highlight ruby %}
$ kubectl create clusterrole pod-role --verb=get,list,watch --resource=pods
$ kubectl get clusterroles
{% endhighlight %}

<p><u><a href="https://kubernetes.io/docs/reference/kubectl/generated/kubectl_create/kubectl_create_clusterrolebinding/">4 Clusterrolebinding</a></u></p>
 
<p>It links the user to the clusterrole.</p>

{% highlight ruby %}
$ kubectl create clusterrolebinding cluster-admin --clusterrole=cluster-admin
$ kubectl get clusterrolebindings
$ kubectl describe clusterrolebindings cluster-admin
$ kubectl describe clusterrole cluster-admin

// Add permission to a Node for a new user
$ kubectl get nodes --as user1
$ kubectl create clusterrole user1-role --verb=get,list,watch --resource=nodes
$ kubectl create clusterrolebinding user1-rolebinding --clusterrole=user1-role --user=user1
$ kubectl describe clusterrole user1-role
$ kubectl describe clusterrolebindinguser1-rolebinding

// Adding permission to storage
$ kubectl api-resources // get the names os the storage would you like
$ kubectl create clusterrole storage-role --resource=persistentvolumes,storageclasses --verb=list,get,watch,create 
$ kubectl get clusterrole storage-role // you can use '-o yaml' to see in the specific format
$ kubectl create clusterrolebinding user1-storage-rolebinding --user=user1 --clusterrole=storage-role
$ kubectl --as user1 get storageclass
{% endhighlight %}


<p><u><a href="https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/">5 Admission Controllers</a></u></p>

<p style="text-align: justify;">It intercept the request after the authorization and authentication but before persist the objects. It can modify the object (Mutating). Admission controllers limit requests to create, delete, modify objects; it can also block custom verbs, however, it cannot block requests to read (get, watch or list) objects.</p>

{% highlight ruby %}
// View enable admission controllers
$ k exec kube-apiserver-controplane -n kube-system --kube-apiserver -h | grep enable-admission-plugins
$ ps aux | grep kube-apiserver | grep privileged
$ vi /etc/kubernetes/manisfest/kube-api-server.yaml
$ watch crictl ps // kube-apiserver restart after any change ok

// in case of error check logs
$ ls /var/log/pods/
$ ls /var/log/containers
{% endhighlight %}

<p><u><a href="https://kubernetes.io/docs/tasks/configure-pod-container/security-context/">6 Security Context</a></u></p>

<p style="text-align: justify;">A security context defines privilege and access control settings for a Pod or Container.</p>

{% highlight ruby %}
apiVersion: v1
kind: Pod
metadata:
  name: pod-name
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - ...
    securityContext:
      allowPrivilegeEscalation: false
      capabilities:
        add: ["SYS_TIME"]
{% endhighlight %}


<h3 id="cronjob">Job</h3>

<p style="text-align: justify;"><em>A <a href="https://kubernetes.io/docs/concepts/workloads/controllers/job/">Job</a> creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate.</em></p>

{% highlight ruby %}
$ k create job --image=nginx my-job --dry-run=client -oyaml > my-job.yaml
// add completions: 10 and backoffLimit: 6 in spec, and command "sh -c 'Hello!!!'" in container.
$ vi my-job.yaml 
$ k create -f my-job.yaml 
$ watch kubectl get jobs
{% endhighlight %}

<h3 id="cronjob">CronJob</h3>

<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/">ConJob</a> is a resource in K8s that schedule jobs to execute repeatable actions.</p>


<br />
<h2 id="hon">Hands On</h2>

<h3>Step 0 - Prepare local environment</h3>

<p style="text-align: justify;">The first steps are to install the tools necessary to make it works. It means install docker, kubectl and colima. After that you can start colima with kubernetes.</p>

{% highlight ruby %}
$ brew install docker
$ brew install kubectl
$ brew install colima
$ colima start --kubernetes
{% endhighlight %}

<h3>Step 1 - prepare the image</h3>

<p style="text-align: justify;">Considering you will create your image, we have to create the image from a project and send it to the Docker Hub. More details about Docker and commands you can see <a href="https://fabiana2611.github.io/infra/docker">here</a>. For our example we are using this <a href="https://github.com/fabiana2611/demo-kubernetes">github code</a>.</p>

{% highlight ruby %}
// create the image
$ docker build -t demo-k8s-vol .   
// run the container with a named volume
$ docker run -p 3000:8080 -d --name demo-vol --rm -v storage:/app/storage demo-k8s-vol
// List the resources created
$ docker images    
$ docker volume ls 
$ docker ps 
{% endhighlight %}

<p style="text-align: justify;">Now you have everything to test. So, do the tests using a browser and a tool for requests (Postman, Insomnia, IntelliJ).</p>

{% highlight ruby %}  
http://localhost:3000/
GET http://localhost:3000/users
POST http://localhost:3000/users -> {"name": "test"}
{% endhighlight %}

<p style="text-align: justify;">After you've checked everything is ok, you can send your image to your Docker Hub. For our local tests purpose, also is possible to used the local image.</p>

{% highlight ruby %}  
// This remote image has to be the same created in your hub
$ docker tag demo-k8s-vol YOUR_PATH/demo-volume  
$ docker login
$ docker push YOUR_PATH/demo-volume
{% endhighlight %}

<h3>Step 2 - Check the goals and plane your actions</h3>

<p style="text-align: justify;">For this scenario let's create the objects in kubernetes locally and allow to do the same tests we did before. Beside the access, let's create roles to a user 'developer' can create all the objects.</p>

<p><center>
  <img src="/img/kubernetes/scenario1.png" height="60%" width="60%">
</center></p>


<h3>Step 3 - Action</h3>

<p style="text-align: justify;">Considering the idea to practices the user restriction, let's start for this. Check your '~/.kube/config' file. Then, we will create a role and link it with the colima user.</p>

{% highlight ruby %}
$ kubectl config view
$ kubectl config set current-context colima // after test, let the original file
$ kubectl auth can-i create pods —as colima

$ k create namespace dev
$ kubectl create role dev-role --verb=list,get,watch,create,delete --resource=service,persistentvolumeclaims,pod -n dev 
$ kubectl create rolebinding dev-rb --role=dev-role --user=colima  -n dev

// Optional steps
// If you need edit any objects created, you can create a file, edit and create again
$ k get role dev-role -n dev -o yaml > role-definition.yaml
$ vi role-definition.yaml 
$ k delete role dev-role -n dev
$ k create -f role-definition.yaml
{% endhighlight %}

<p style="text-align: justify;">Now, let's create the volume that will be used by the Pod. For that, we will create an environment variable to be used to identify the folder name for store data. Then, we will create a deployment with the pod with the reference to the environment and our image. If you want to use your local image you have to add the attribute 'imagePullPolicy=Never'. The last step is to create the service to expose the application. All these files are in the <a href="https://github.com/fabiana2611/demo-kubernetes/tree/main/kubernetes">Github project</a>. </p>

{% highlight ruby %}
$ k create -f pv-definition.yaml -n dev
$ k create -f pvc-definition.yaml -n dev

$ k create -f environment.yaml -n dev 
$ k get configmaps -n dev
$ k create -f deployment.yaml -n dev
$ k get deployments -n dev
$ k get svc -n dev

$ k expose deployment demo-deploy --type=LoadBalancer --port=8080 --target-port=8080 --name demo-service -n dev
{% endhighlight %}

<p style="text-align: justify;">Now you have everything to test again.</p>

{% highlight ruby %}  
http://localhost:8080/
POST http://localhost:8080/users -> {"name": "test"}
GET http://localhost:8080/users
{% endhighlight %}

<h3>Step 3 - Rollout</h3>

<p style="text-align: justify;">Now, let's change something in the project and create the image again. Pay attention to the fact that the image has to have a new tag to be recognized as a different image.</p>

{% highlight ruby %}  
$ docker build -t YOUR_PATH/demo-volume:v2 .
$ docker push YOUR_PATH/demo-volume:v2    // do this if you are using a remote image

// update the deployment
$ k set image deployment/demo-deploy demo-k8s=fabianafreire/demo-volume:v2 -n dev

// check the deployment status
$ k rollout status deployments/demo-deploy -n dev
$ k get pods
{% endhighlight %}

<p style="text-align: justify;">As a last step for practice purposes, let's use an image that does not exist.</p>

{% highlight ruby %}  
$ k set image deployment/demo-deploy demo-k8s=test -n dev
$ k rollout status deployments/demo-deploy -n dev // blocked waiting for the immage (crt+c)
$ k get pods -n dev // there is an error but none of the other was finished

// rollback
$ k rollout undo deployment/demo-deploy -n dev
$ k rollout status deployment/demo-deploy -n dev
$ k get pods -n dev // the pod with error doesnot exist

$ k rollout history deployment/demo-deploy -n dev

// you can go to any revision
$ k rollout history deployment/demo-deploy -n dev --revision=3
$ k rollout undo deployment/demo-deploy --to-revision=1 
{% endhighlight %}


<h3>Step 4 - Minikube</h3>

<p style="text-align: justify;">Optionally, you can intall <a href="https://minikube.sigs.k8s.io/docs/start/">minikube</a> to try an interface to manage the K8s objects. It is a good option because it will help you become familiar with those kinds of tools.</p>

{% highlight ruby %}
$ minukube start     // Create a minikube cluster 
$ minikube dashboard // Open the browser

// One step more to expose the service because of menikube
// Use this URL to access the application
$ minikube service demo-deploy 
{% endhighlight %}

<p style="text-align: justify;">You can repeat all the steps to create the objects in a cluster without the namespace and see the results in minikube.</p>

<p style="text-align: justify;">Also, you can try with this application: <a href="https://github.com/neilpricetw/kubernetes-security-nodejs-mysql">kubernetes-security-nodejs-mysql</a>. It has example of insecure and secure application with the best practices.</p>


<h3>Step 5 - Extra practice</h3>

<p>First of all, let's create a new node to add k8s objects. In localhost is allow only one node. For exercice purpuse, let's pretend it works :D.</p>

{% highlight ruby %}
// Create a new node from a JSON file
{
  "kind": "Node",
  "apiVersion": "v1",
  "metadata": {
    "name": "node01",
    "labels": {
      "name": "node01"
    }
  }
}
$ k create -f node01.json

// Add Taint to node 01
$ k taint node node01 app_type=alpha:NoSchedule 

// add new label - be used by affinity
$ k label node node01 app_type=beta
{% endhighlight %}

<p>Now we are available to create deployment and service to that node by affinity and add rules of telerations. Also, you can <a href="https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/">assign a pod to a node by attribute</a>.</p>

{% highlight ruby %}
$ k create deployment test-app --image=nginx --replicas=1 --dry-run=client -oyaml > test-dep.yaml 
// add tolerations aatt in template.spec section and nodeAffinity
tolerations:
  - effect: NoSchedule
    key: app_type
    value: alpha
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: app_type
          operator: In
          values: ["beta"]

$ k create -f test-dep.yaml
$ k get pod -o wide               // check node
$ k describe pod test-app-XXXXX   // check error in pod

$ k expose deployment test-app --name test-app-service --type NodePort --port 80 --dry-run=client -oyaml > service-app.yaml
$ vi service-app.yaml // add nodePort: 30080
$ k create -f service-app.yaml
$ k get svc
{% endhighlight %}

<p>For practices purpose, lets add <a href="https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/">readiness and liveness</a> attributes to the pods. The liveness probes is used to decide when restart a container, and the readiness is used to identify when a container is ready to start accepting traffic.</p>

{% highlight ruby %}
// readinessProbe + livenessProbe: add the atts inside container
$ vi test-dep.yaml
readinessProbe:
  httpGet:
    path: /healthcheck
    port: 8080
livenessProbe:
  exec:
    command: ["echo 'Hello World!'"]
  initialDelaySeconds: 10
  periodSeconds: 60
$ k replace -f test-dep.yaml --force
{% endhighlight %}

<p>Now let's create an Ingress that will redirect and call to that service.</p>

{% highlight ruby %}
// Ingress
$ k create ingress ingress --rule="www.example.com/users*=test-app-service:80" 
$ k get ingress
{% endhighlight %}


<br />
<h2 id="hon">AWS</h2>

<table>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/E956xeOt050?si=cRAvoS-MMToNPE-w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/MTnQW9MxnRI?si=yAZ7JXJkFdqopt0Z" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></td>
  </tr>
</table>


<br />
<h2>References</h2>
<ul>
  <li><a href="https://www.udemy.com/course/docker-kubernetes-the-practical-guide/?couponCode=LETSLEARNNOWPP">Docker & Kubernetes: The Practical Guide [2024 Edition]</a></li>
  <li><a href="https://www.udemy.com/course/certified-kubernetes-application-developer/?couponCode=LETSLEARNNOWPP">Kubernetes Certified Application Developer (CKAD) with Tests</a></li>
  <li><a href="https://kubernetes.io/docs/reference/kubectl/">Command line tool (kubectl)</a></li>
  <li><a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/object-management/#imperative-commands">Command Reference</a></li>
  <li><a href="https://gist.github.com/rahulkumar-aws/65e6fbe16cc71012cef997957a1530a3">Remove minikube</a></li>
  <li><a href="https://docs.aws.amazon.com/eks/latest/userguide/creating-a-vpc.html">Creating a VPC for your Amazon EKS cluster</a></li>
</ul>  
