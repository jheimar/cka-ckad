# Ejercicios de la certificación CKAD y CKA

### Noticia: 30% de descuento en las certificaciones hasta el 30 de abril [Coupon Code](https://training.linuxfoundation.org/april-2020-promo)

El objetivo de este repositorio es ayudar a pasar los examenes de Certified Kubernetes Application Developer (CKAD) y Certified Kubernetes Administrator (CKA) utilizando recursos en línea, especialmente utilizando recursos de [Documentación oficial de Kubernetes] (https://kubernetes.io).

Las referencias se seleccionaron para el Currículo de examen 1.18, que utiliza la versión Kubernetes 1.18, y hay información exclusiva para objetos API y anotaciones. Para obtener más información, consulte [CKA Curriculum 1.18](https://github.com/cncf/curriculum/blob/master/CKA_Curriculum_V1.18.pdf) y [CKAD Curriculum 1.18](https://github.com/cncf/curriculum/blob/master/CKAD_Curriculum_V1.18.pdf)

# Certified Kubernetes Application Developer (CKAD)

Lista de recursos y notas para aprobar el examen Certified Kubernetes Application Developer (CKAD). Enlaces oficiales a continuación.

Ademas de un conjunto de ejercicios que te ayudaron a prepararme para el examen [Certified Kubernetes Application Developer] (https://www.cncf.io/certification/ckad/), ofrecido por la Cloud Native Computing Foundation. 

## CKAD Curriculum

- [Core Concepts - 13%](./ckad/core_concepts.md)
- [Multi-container pods - 10%](./ckad/multi_container_pods.md)
- [Pod design - 20%](./ckad/pod_design.md)
- [Configuration - 18%](./ckad/configuration.md)
- [Observability - 18%](./ckad/observability.md)
- [Services and networking - 13%](./ckad/services.md)
- [State persistence - 8%](./ckad/state.md)


# Certified Kubernetes Administrator (CKA)

Lista de recursos y notas para aprobar el examen Certified Kubernetes Administrator (CKA). 

Ademas de un conjunto de ejercicios que te ayudaron a prepararme para el examen [Certified Kubernetes Application Developer] (https://www.cncf.io/certification/cka/), ofrecido por la Cloud Native Computing Foundation. 


# CKA Curriculum

Exam objectives that outline of the knowledge, skills and abilities that a Certified Kubernetes Administrator (CKA) can be expected to demonstrate.

## Application Lifecycle Management 8%

- Understand Deployments and how to perform rolling updates and rollbacks.

    - [Concepts: Workloads: Controllers: Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

    - Example Deployment File (dep-nginx.yaml) using NGINX 

        ```yaml
        apiVersion: apps/v1
            kind: Deployment
            metadata:
            name: nginx-deployment
            labels:
                app: nginx
            spec:
            replicas: 3
            selector:
                matchLabels:
                app: nginx
            template:
                metadata:
                labels:
                    app: nginx
                spec:
                containers:
                - name: nginx
                    image: nginx:1.15.4
                    ports:
                    - containerPort: 80
        ```

        ```bash
        # Create Deployment
        kubectl create -f dep-nginx.yaml

        # Get Deployments
        kubectl get deployments

        # Update Deployment
        kubectl edit deployment.v1.apps/nginx-deployment

        # See rollout status
        kubectl rollout status deployment.v1.apps/nginx-deployment

        # Describe Deployment
        kubectl describe deployment

        # Rolling back to a previous revision
        kubectl rollout undo deployment.v1.apps/nginx-deployment

- Know various ways to configure applications.

    - [Concepts: Cluster Administration: Managing Resources](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)

- Know how to scale applications.

    - [Concepts: Cluster Administration: Managing Resources: #Scaling Your Application](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#scaling-your-application).

        ```bash
        # Increase replicas number for nginx-deployment
        kubectl scale deployment/nginx-deployment --replicas=5

        # Using autoscaling
        kubectl autoscale deployment/nginx-deployment --min=2 --max=5
        ```

- Understand the primitives necessary to create a self-healing application.

    - [Concepts: Workloads: Pods: Pod Lifecycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

    - [Tasks: Configure Pods and Containers: Liveness and Readiness Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)

## Installation, Configuration & Validation 12%

- Design a Kubernetes cluster.

    - [Concepts: Cluster Administration: Overview: Planning a Cluster](https://kubernetes.io/docs/concepts/cluster-administration/cluster-administration-overview/#planning-a-cluster)

- Install Kubernetes masters and nodes.

    - [Setup: Creating a Custom Cluster from Scratch](https://kubernetes.io/docs/setup/scratch/)

- Configure secure cluster communications.

    - [Tasks: TLS: Manage TLS Certificates in a Cluster](https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/)

- Configure a Highly-Available Kubernetes cluster.

    - [Setup: Bootstrapping Clusters with kubeadm: Creating Highly Available Clusters with kubeadm](https://kubernetes.io/docs/setup/independent/high-availability/)

- Know where to get the Kubernetes release binaries.

    - [Setup: Downloading Kubernetes: Bulding from Source](https://kubernetes.io/docs/setup/release/building-from-source/)

- Provision underlying infrastructure to deploy a Kubernetes cluster.

    - [Setup: Picking the Right Solution](https://kubernetes.io/docs/setup/pick-right-solution/)

- Choose a network solution.

    - [Setup: Creating a Custom Cluster from Scratch: #Network](https://kubernetes.io/docs/setup/scratch/#network)

- Choose your Kubernetes infrastructure configuration.

    - [Setup: Creating a Custom Cluster from Scratch: #Nodes](https://kubernetes.io/docs/setup/scratch/#nodes)
    - [Setup: Building Large Clusters](https://kubernetes.io/docs/setup/cluster-large/)

- Run end-to-end tests on your cluster.

    - [Reference: Kubectl Commands: Cluster Management](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-cluster-management-strong-)

    - [Extra: End-to-End Testing in Kubernetes](https://github.com/kubernetes/community/blob/master/contributors/devel/e2e-tests.md)

- Analyse end-to-end tests results.

    - [Extra: Kubetest](https://github.com/kubernetes/test-infra/tree/master/kubetest)

- Run Node end-to-end tests.

    - [Node End-To-End tests](https://github.com/kubernetes/community/blob/master/contributors/devel/e2e-node-tests.md)

```bash
# Kucebtl Cheatsheet commands to end-to-end tests

# Display addresses of the master and services
kubectl cluster-info

# Dump current cluster state to stdout
kubectl cluster-info dump

# Check health of cluster components
kubectl get componentstatuses

# List the nodes
kubectl get nodes

# Show metrics for a given node
kubectl top node my-node

# List all pods in all namespaces, with more details
kubectl get pods -o wide --all-namespaces

# List all services in all namespaces, with more details
kubectl get svc  -o wide --all-namespaces
```

## Core Concepts 19%

- Understand the Kubernetes API primitives

    - [Concepts: Kubernetes API Overview](https://kubernetes.io/docs/concepts/overview/kubernetes-api/)
    - [Concepts: Understanding Kubernetes Objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/).
    - [Reference: API Reference - V1.12](https://kubernetes.io/docs/reference/kubernetes-api/)
    - [Optional: Kubernetes Architecture 101 (Video Youtube)](https://www.youtube.com/watch?v=zeS6OyDoy78)

- Understand the Kubernetes cluster architecture.

    - [Concepts: Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)
    - [Concepts: Concepts Underlying the Cloud Controller Manager](https://kubernetes.io/docs/concepts/architecture/cloud-controller/)

- Understand Services and other network primitives.

    - [Concepts: Services, Load Balancing and Networking](https://kubernetes.io/docs/concepts/services-networking/service/)

## Networking 11%

- Understand the networking configuration on the cluster nodes.

    - [Concepts: Cluster Administration: Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

- Understand Pod networking concepts.

    - [Kubernetes Project: Design Proposals - Network](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/network/networking.md)

- Understand service networking.

    - [Concepts: Services, Load Balancing, and Networking: Services](https://kubernetes.io/docs/concepts/services-networking/service/)

- Deploy and configure network load balancer.

    - [Tasks: Access Applications in a Cluster: Create an External Load Balancer](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/)

- Know how to use Ingress rules.

    - [Concepts: Services, Load Balancing, and Networking: Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

- Know how to configure and use the cluster DNS.

    - [Concepts: Services, Load Balancing, and Networking: DNS for Services and Pods](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

- Understand CNI.

    - [Concepts: Extending Kubernetes: Compute, Storage, and Networking Extensions: Network Plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

## Scheduling 5%

- Use label selectors to schedule Pods.

    - [Concepts: Overview: Working with Kubernetes Objects: Labels and Selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

- Understand the role of DaemonSets.

    - [Concepts: Workloads: Controllers: DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

- Understand how resource limits can affect Podscheduling.

    - [Tasks: Administer a Cluster: Manage Memory, CPU, and API Resources: Configure Default Memory Requests and Limits for a Namespace](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/)
    - [Tasks: Administer a Cluster: Manage Memory, CPU, and API Resources: Configure Default CPU Requests and Limits for a Namespace](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/cpu-default-namespace/)

- Understand how to run multiple schedulers and how to configure Pods to use them.

    - [Tasks: Administer a Cluster: Configure Multiple Schedulers](https://kubernetes.io/docs/tasks/administer-cluster/configure-multiple-schedulers/)

- Manually schedule a pod without a scheduler.

    - [Tasks: Administer a Cluster: Static Pods](https://kubernetes.io/docs/tasks/administer-cluster/static-pod/)

- Dispaly scheduler events.

    - [Tasks: Administer a Cluster: Configure Multiple Schedulers: #Verifying that the pods were scheduled using the desired schedulers](https://kubernetes.io/docs/tasks/administer-cluster/configure-multiple-schedulers/#verifying-that-the-pods-were-scheduled-using-the-desired-schedulers)

        ```bash
        $ kubectl get events
        # or
        $ kubectl describe pods | grep -A7 ^Events

        # Master/Control node 
        $ tail /var/log/kube-scheduler.log
        ```
- Know how to configure the Kubernetes scheduler.

    - [Tasks: Administer a Cluster: Configure Multiple Schedulers](https://kubernetes.io/docs/tasks/administer-cluster/configure-multiple-schedulers/)

## Security 12%

- Know how to configure authentication and authorization.

    - [Tasks: Administer a Cluster: Securing a Cluster](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/)

- Understand Kubernetes security primitives.

    - [Reference: Accessing the API: Authorization Overview](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)
        - Check all sub resources (Node Authorization, ABAC, RBAC, and Webhook)

- Know to configure network policies.

    - [Tasks: Administer a Cluster: Declare Network Policy](https://kubernetes.io/docs/tasks/administer-cluster/declare-network-policy/)

- Create and manage TLS certificates for cluster components.

    - [Tasks: TLS: Manage TLS Certificates in a Cluster](https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/)

- Work with images securely.

    - [Concepts: Containers: Images](https://kubernetes.io/docs/concepts/containers/images/)

    - [Concepts: Configuration: Best Practices: #Container Images](https://kubernetes.io/docs/concepts/configuration/overview/#container-images)

- Define security contexts.

    - [Tasks: Configure Pods and Containers: Configure a Security Context for a Pod or Container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

- Secure persistent key value store.

    - [Concepts: Configuration: Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

## Cluster (Maintenance) 11%

- Understand Kubernetes cluster upgrade process.

    - [Tasks: Administration with kubeadm: Upgrading kubeadm clusters from v1.11 to v1.12](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade-1-12/)
    - [Tasks: Administration with kubeadm: Upgrading kubeadm HA clusters from v1.11 to v1.12](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade-ha-1-12/)

- Facilitate operating system upgrades.
- Implement backup and restore methodologies.

    - [Tasks: Administer a Cluster: Operating etcd clusters for Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

## Logging / Monitoring 5%

- Understand how to monitor all cluster components.

    - [Tasks: Monitor, Log, and Debug: Tools for Monitoring Resources](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)

- Understand how to monitor applications.

    - [Tasks: Monitor, Log, and Debug: Application Introspection and Debugging](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application-introspection/)

- Manage cluster component logs.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)

        - Master Log Files
        ```
        /var/log/kube-apiserver.log - API Server, responsible for serving the API
        /var/log/kube-scheduler.log - Scheduler, responsible for making scheduling decisions
        /var/log/kube-controller-manager.log - Controller that manages replication controllers
        ```

         - Worker Nodes Log Files
        ```
        /var/log/kubelet.log - Kubelet, responsible for running containers on the node
        /var/log/kube-proxy.log - Kube Proxy, responsible for service load balancing
        ```

- Manage application logs.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Applications](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/)


## Storage 7%

- Understand persistent volumes and know how to create them.

    - [Concepts: Storage: Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

- Understand access modes for volumes.

    - [Concepts: Storage: Persistent Volumes: #Access Modes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes)

- Understand persistent volume claims primitive.

    - [Concepts: Storage: Persistent Volumes: #PersistentVolumeClaims](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)

- Understand Kubernetes storage objects.

    - [Concepts: Storage: Volumes](https://kubernetes.io/docs/concepts/storage/volumes)

- Know how to configure applications with persistent storage.

    - [Concepts: Storage: Volumes: #local](https://kubernetes.io/docs/concepts/storage/volumes/#local)
    - [Concepts: Storage: Volumes: #hostPath](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath)

## Troubleshooting 10%

- Troubleshoot application failure.


    - [Tasks: Monitor, Log, and Debug: Troubleshoot Applications](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/)
    - [Tasks: Monitor, Log, and Debug: Determine the Reason for Pod Failure](https://kubernetes.io/docs/tasks/debug-application-cluster/determine-reason-pod-failure/)

- Troubleshoot control plane failure.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)

- Troubleshoot worker node failure.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Clusters: #Worker Nodes](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/#worker-nodes)

- Troubleshoot networking.

# Cursos de preparación para CKA y CKAD 

- [Certified Kubernetes Administrator (CKA) with Practice Tests - Udemy](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/)


- [Kubernetes Certified Application Developer (CKAD) with Tests - Udemy](https://www.udemy.com/course/certified-kubernetes-application-developer/)

- [Certified Kubernetes Administrator (CKA) - Linux Academy](https://linuxacademy.com/cp/modules/view/id/155)

- [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)

- [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)

