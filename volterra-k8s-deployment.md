# Deploy YugabyteDB on F5/Volterra k8s

## Background
F5 provide the F5 Distributed Cloud Services(a.k.a Volterra), which provides k8s cluster in cloud and edge.
We would like to run YugabyteDB on top of that, and see the deployment options of YugabyteDB Clusters.

| Deploy k8s on `network cloud (RE)` | Virtual Site should be `RE` | vk8s Objects and Virtual Sites |
|-|-|-|
|![image](https://user-images.githubusercontent.com/1793451/169200160-9ffa0062-997f-44ec-8fd9-c14e34dd6960.png)|![image](https://user-images.githubusercontent.com/1793451/169201395-1faf6c8f-638a-4c3b-b103-c6236fbb26e0.png)|![image](https://user-images.githubusercontent.com/1793451/169197667-7593d213-23d7-4f66-8060-5de565594cd3.png)|

- Overview of Distributed Application Management
  https://docs.cloud.f5.com/docs/ves-concepts/dist-app-mgmt


## Steps
1. Create an Account
1. [Create Virtual K8s (vK8s) Object](https://github.com/yugabytedb-japan/demos/volterra-k8s-deployment#1-create-virtual-k8s-object)

   See details at: https://docs.cloud.f5.com/docs/how-to/app-management/create-vk8s-obj

    There are [Prerequisites](https://docs.cloud.f5.com/docs/how-to/app-management/create-vk8s-obj), but we can skip it.
    - Cloud or Edge site ( -> we use `RE`, so skipped it )
    - [Create a Virtual Site](https://docs.cloud.f5.com/docs/how-to/fleets-vsites/create-virtual-site) ( -> we will setup in vK8s object )
 
1. [Create vk8s Deployment](https://github.com/yugabytedb-japan/demos/new/main#create-vk8s-deployment)
  See details at: https://docs.cloud.f5.com/docs/how-to/app-management/vk8s-deployment


## 1. Create Virtual k8s object
- access to the console, select "Distributed Apps" > "Applications" > "Virtual K8s"
![image](https://user-images.githubusercontent.com/1793451/169180721-3ff09bfc-db5e-413a-9bf1-e4400b93f4ae.png)


- Edit the configuration
![image](https://user-images.githubusercontent.com/1793451/169260612-2c7773ab-35c0-4fa9-a277-26ca75c2bf84.png)

  - Add Metadata Name
  ![image](https://user-images.githubusercontent.com/1793451/169260868-42ed90f8-4cb6-4233-95d1-46409470a7fd.png)


  - Configure Virtual Sites
  ![image](https://user-images.githubusercontent.com/1793451/169260968-e5dcf520-6b54-401f-ae32-6b9dbe4eedd7.png)
  
  - Select `Add new Virutal Site`
  ![image](https://user-images.githubusercontent.com/1793451/169261271-c376a922-8d1e-40df-8ee6-a374723cdfd9.png)

  - Add Metadata Name for Virtual Site, and Select `Site Type`
  ![image](https://user-images.githubusercontent.com/1793451/169261682-2d79cb2a-7145-4c64-bab7-d168b6ce9e96.png)

  - Configure `Site Selector Expression`
  ![image](https://user-images.githubusercontent.com/1793451/169263141-db2e7018-2b0d-4ceb-bcdf-0daab44a1e21.png)
  
    | Select or add key | Select operator | Assign value or type to add |
    |-|-|-|
    |![image](https://user-images.githubusercontent.com/1793451/169262898-3e58213f-2498-4b98-ba7f-0c67a83847cd.png)|![image](https://user-images.githubusercontent.com/1793451/169262948-04c1d1ac-8089-4c69-a8b8-ea2b7c42df47.png)|![image](https://user-images.githubusercontent.com/1793451/169263001-62bdf066-fd68-42b3-b0af-532dacd4764a.png)|

  - Configure `Choose Service Isolation` as `Disabled`
  ![image](https://user-images.githubusercontent.com/1793451/169264031-ae2ada69-f612-4ab7-a049-f8d147550972.png)
  
  - Configure `Default Workload Flavor` 
  ![image](https://user-images.githubusercontent.com/1793451/169264274-5470b8ac-a4cd-4ca6-8235-cb60fd9870b8.png)

    - Select `Create new Workload Flavor`
    ![image](https://user-images.githubusercontent.com/1793451/169264529-8ee6cb72-02de-4749-b599-b781c1bdbf69.png)

      - Memory is 1-32678 range
      ![image](https://user-images.githubusercontent.com/1793451/169264764-fed03ac5-d82e-4f10-8ceb-e0b47942be07.png)

      - Ephemeral Storage is 1-60000 range
      ![image](https://user-images.githubusercontent.com/1793451/169264869-54b15458-f645-4036-8705-91f0f6575370.png)


  - k8s Cluster is Deployed 
   
  ![image](https://user-images.githubusercontent.com/1793451/169212242-954f88d8-da3e-4203-89a6-7c851658850a.png)


## Create vk8s Deployment

https://docs.cloud.f5.com/docs/how-to/app-management/create-vk8s-obj

- Donwload kubeconfig from console UI
![image](https://user-images.githubusercontent.com/1793451/169212278-40a3895e-a348-4688-98f5-1d9927054931.png)

 - setting expiration of `kubeconfig` 1-90 days

   | select the date | up to 90 days |
   | - | - |
   |![image](https://user-images.githubusercontent.com/1793451/169212504-625e7908-dfb2-4442-b401-5558ebd8280e.png)|![image](https://user-images.githubusercontent.com/1793451/169212530-dc711ed3-e989-486a-8f38-b00664f62369.png)|

- Get the sample YAML for yb cluster

  [https://github.com/yugabyte/yugabyte-db/tree/master/cloud/kubernetes](https://github.com/yugabyte/yugabyte-db/tree/master/cloud/kubernetes#readme)
  
  - Use this [stateful set](https://github.com/yugabyte/yugabyte-db/blob/master/cloud/kubernetes/yugabyte-statefulset.yaml) sample code
  
  FYI: Deploy k8s Statefulset on GKE, AKS
  - https://docs.yugabyte.com/preview/deploy/kubernetes/single-zone/gke/statefulset-yaml/
  - https://docs.yugabyte.com/preview/deploy/kubernetes/single-zone/aks/statefulset-yaml/
  

- Verify the `kubeconfig` with `kubectl config --kubeconfig=./ves_default_yb-japan-k8s.yaml view`

- Run `apply command`

  ```
  % kubectl apply -f yugabyte-statefulset.yaml --kubeconfig=./ves_default_yb-japan-k8s.yaml  
  service/yb-masters created
  Error from server: error when creating "yugabyte-statefulset.yaml": admission webhook "default.ves.io" denied the request: Service Type LoadBalancer is not allowed, only ClusterIP is allowed
  Error from server: error when creating "yugabyte-statefulset.yaml": admission webhook "default.ves.io" denied the request: 1 error occurred:
    * Specifying StorageClassName is not allowed

  Error from server (Forbidden): error when creating "yugabyte-statefulset.yaml": services "yb-tservers" is forbidden: exceeded quota: yb-japan-k8s, requested: count/services=1, used: count/services=2, limited: count/services=2
  Error from server: error when creating "yugabyte-statefulset.yaml": admission webhook "default.ves.io" denied the request: Service Type LoadBalancer is not allowed, only ClusterIP is allowed
  Error from server: error when creating "yugabyte-statefulset.yaml": admission webhook "default.ves.io" denied the request: 1 error occurred:
    * Specifying StorageClassName is not allowed
  ```

  - It seems resource quota is too limited.

  ```
  % kubectl get resourcequota --kubeconfig=./ves_default_yb-japan-k8s.yaml  
  NAME           AGE    REQUEST                                                                                                                                                                                                                                                                  LIMIT
  yb-japan-k8s   114m   count/configmaps: 0/2, count/cronjobs.batch: 0/2, count/daemonsets.apps: 0/2, count/deployments.apps: 0/2, count/jobs.batch: 0/4, count/persistentvolumeclaims: 0/2, count/secrets: 0/2, count/serviceaccounts: 0/2, count/services: 2/2, count/statefulsets.apps: 0/2
  ```

