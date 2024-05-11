---
layout: post
title:  "Kubernetes"
date:   2024-05-11
categories: infra
permalink: /:categories/kubernetes
---


<p><a href="#arch">What is it?</a> > <a href="#arch">Architecture</a> > <a href="#pod">Pod</a> > <a href="#rs">ReplicaSet</a> > <a href="sa">Special Attributes</a> > <a href="#deploy">Deployment</a> > <a href="ds">Deployment Strategy</a> > <a href="svc">Service</a> > <a href="net">Network</a> > <a href="volume">Volume</a> > <a href="ns">Namespace</a> > <a href="secret">Secrets</a> >  <a href="hon">Hands-On</a> </p>

<br />
<h2 id="wit">Introduction</h2>
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

<h3 id="pod" >Pod</h3>
<p style="text-align: justify;">
<a href="https://kubernetes.io/docs/concepts/workloads/pods/">Pod</a> is a kubernate object that represents a deployable unit of a set of containers. The containers are encapsulated into the Pod that run an instance of the application. If you need to increase the application with more Pods then you need increase the replication number (scale up). To have an application in a Pod is assumed that the application is already developed and built into an images and it is available in some repository. Also assume that the Kubernetes cluster has set up and working. The Pod can have more than one container (only one instance), but the best practices is to have only one container by Pod. </p>

{% highlight ruby %}
$ kubectl create -f pod-definition.yaml // Declarative

// you cannot edit a pod. Extract the pod definition and make changes. 
// Delete the old POD and create a new one
$ kubectl get pod webapp -o yaml > pod-definition.yaml // edit

$ kubectl run nginx --image=nginx.      // Imperative
$ kubectl run custom-nginx --image=nginx --port=8080
$ kubectl run redis --image=redis:alpine --labels="tier=db"
$ kubectl run hello-minikube
$ kubectl cluster-info
$ kubectl get nodes
$ kubectl get pods
{% endhighlight %}

<p><center>
  <img src="/img/kubernetes/pod.png" height="100%" width="100%">
</center></p>

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
  <img src="/img/kubernetes/replicaset.png" height="70%" width="70%">
</center></p>

<h3 id="sa">Special Attributes</h3>
<ul>
  <li><a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/">Labels and selectors:</a> the objects in kubernates have labels to be used to monitor that objects. For selector, the 'matchLabels' are used to filter the objects. The idea of selectors is to have flexibility when it comes to expressing which other resource be connected to or controlled by other resource.</li>
  <li><a href="https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/">Environment Variables:</a> It's possible to use env attributes to add the variables to be used. It can be a direct key-value pair or doing a reference to a external file.</li>
  <li><a href="https://kubernetes.io/docs/concepts/configuration/configmap/">ConfigMap:</a> it is a key-value pair configuration used as more organized way to create the configuration using separated files</li>
</ul>

<h3 id="deploy">Deployment</h3>
<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/workloads/controllers/deployment/">Deployment</a> build the desired state. A Deployment provides declarative updates for Pods and ReplicaSets. It allow edit any field/property of the POD template. After the change, the deployment will automatically delete and create a new pod with the new changes. The deployment can be <a href="https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment">rollback</a> when the deployment is not stable. Also, you can <a href="https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-a-deployment">scale</a> the deployment if you need increase or decrease the replicas. If you delete the deployment object, the others object created by it will be deleted (e.g., pods and replicase).</p>

{% highlight ruby %}
// CREATE
$ kubectl create -f deployment-definition.yaml                // Declarative
$ kubectl scale deployment nginx --replicas=4
$ kubectl create deployment nginx --image=nginx               // Imperative
$ kubectl create deployment nginx --image=nginx --replicas=4
$ kubetcl get deployments
$ kubectl get all

// UPGRADE - StrategyType attribute (First step is created a new replicaSet)
$ kubectl edit deployment my-deployment         // Change definition directly
$ kubectl apply –f deployment-definition.yml    // Change the file and apply
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
$ kubectl expose pod redis --port=6379 --name redis-service       // example 1
$ kubectl run httpd --image=httpd:alpine --port=80 --expose=true  // example 2
$ kubectl get svc
{% endhighlight %}

<p><center>
  <img src="/img/kubernetes/service.png" height="100%" width="100%">
</center></p>

<h3 id="volume">Storage</h3>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/storage/volumes/">volume</a> is a directory which is accessible to the containers in a pod. The volume persists even if container restart. However, the volumes are removed when the Pods are destroyed. Considering One-Node environment, the hostPath property helps to keep the data visible for that Node.</p>

<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/storage/persistent-volumes/">Persistent Volume</a> is a volume in the cluster with the lifecycle independent of the Pod. Persistent Volume Claim is a request for storage by user.</p>

<p><center>
  <img src="/img/kubernetes/storage.png" height="70%" width="70%">
</center></p>

<h3 id="ns">Namespace</h3>
<p style="text-align: justify;"><a href="https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/">Namespace:</a> mechanism for isolating groups of resources within a single cluster.</p>

{% highlight ruby %}
$ kubectl get namespaces
$ kubectl create -f namespace-dev.yaml
$ kubectl create namespace dev
$ kubetcl get pods --namespace=dev
$ kubetcl get pods --all-namespaces kubetcl get pods -A
$ kubectl delete deploy redis-deploy -n dev-ns
{% endhighlight %}

<h3 id="secret">Secret</h3>

<p style="text-align: justify;">The <a href="https://kubernetes.io/docs/concepts/configuration/secret/">Secrets</a> objects are used to store sensitive data which is done in an encoded format. It is created independent of the Pod.</p>

{% highlight ruby %}
$ echo –n ‘mysql’ | base64
$ echo –n ‘bXlzcWw=’ | base64 --decode

// Imperative
kubectl create secret generic \
  app-secret --from-literal=DB_Host=mysql --from-literal=DB_User=root \
  kubectl create secret generic SECRET_NAME --from-file=<path-to-file> kubectl create secret generic \
  app-secret --from-file=app_secret.properties --from-literal=DB_Password=paswrd

// Declarative 
$ kubectl create -d secret.yaml

$ kubectl get secrets
$ kubectl describe secrets
{% endhighlight %}

<h3 id="secret">Secret</h3>
<p style="text-align: justify;"><a href="">Service Account</a> is an account to allow the communication machine-to-machine. When it is created, a token is generated inside a secret object. <em>When you create a cluster, Kubernetes automatically creates a ServiceAccount object named default for every namespace in your cluster</em>.</p>

{% highlight ruby %}
kubectl create serviceaccount my-sa
kubectl get serviceaccount
kubectl describe serviceaccount my-sa
kubectl describe secret my-sa-token-kbbdm
{% endhighlight %}


<br />
<h2 id="hon">Hands On</h2>

{% highlight ruby %}
$ brew install docker
$ brew install kubectl
$ brew install colima
$ colima start --kubernetes

// Create an image by docker 
$ docker build -t kube-first-app . 

// Imperative Commands

// Create a deployment with the local image
$ k create deployment first-app --image=kube-first-app // Create the pod with ErrImagePull
$ k get deployments
$ k get rs
$ k edit deployment first-app // imagePullPolicy=Never to use the local image (it is vim editor)
$ k get pods // The old one is suppose to be removed and a new one Running
$ k expose deployment first-app --type=LoadBalancer --port=8080 // create the service accessed out of cluster
$ k get svc

// go to your browser and put http://localhost:8080
// go to your browser and put http://localhost:8080/error -> the deployment monitor to restart the pod

// change replicas 
$ k edit deployment first-app // k scale remote/first-app --replicas=3 (in case using remote image)
$ k get pods

// go to your browser and put http://localhost:8080/error -> one will running (traffic scalling to who is running)


// change the code of the project
// Rebuild the image. It has to have a different tags or the deployment will not recognize difference
$ docker build -t kube-first-app:2 . 
// update the deployment
$ k set image deployment/first-app kube-first-app=kube-first-app:2 // update the image to the deployment first-app that exist
// check the deployment status
$ k rollout status deployment/first-app
$ k get pods

// try use an image that does not exist
$ k set image deployment/first-app kube-first-app=kube-first-app:3
$ k rollout status deployment/first-app // blocked waiting for the immage (crt+c)
$ k get pods // thire is an error but none of the other was finished
// rollback
$ k rollout undo deployment/first-app
$ k rollout status deployment/first-app
$ k get pods // the pod with error doesnot exist
$ k rollout history deployment/first-app
$ k rollout history deployment/first-app --revision=3
$ k rollout undo deployment/first-app --to-revision=1 // If you are using local image is necessary edit again imagePullPolicy attribute
{% endhighlight %}


<br />
<h2>References</h2>
<ul>
  <li><a href="https://www.udemy.com/course/docker-kubernetes-the-practical-guide/?couponCode=LETSLEARNNOWPP">Docker & Kubernetes: The Practical Guide [2024 Edition]</a></li>
  <li><a href="https://www.udemy.com/course/certified-kubernetes-application-developer/?couponCode=LETSLEARNNOWPP">Kubernetes Certified Application Developer (CKAD) with Tests</a></li>
  <li><a href="https://kubernetes.io/docs/reference/kubectl/">Command line tool (kubectl)</a></li>
</ul>  
