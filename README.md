# K8S-Best-practises, tips and tricks.
# P.S. Namespaces are a way to divide cluster resources between multiple users. 

A- Add default memory limits and cpu limits to namespaces.

apiVersion: v1  
 kind: LimitRange  
 metadata:  
   name: mem-limit-range  
 spec:  
   limits:  
   - default:  
       memory: 512Mi  
     defaultRequest:  
       memory: 256Mi  
     type: Container
     
     
   
   
B- Segregate teams based on a namespace and then use RBAC policies.


C- Guarantee no downtime for your app withing your K8S cluster with PodDisruptionBudget, PDB’s (PodDisruptionBudget) should be placed on every deployment that has more than 1 instance.

apiVersion: policy/v1beta1  
 kind: PodDisruptionBudget  
 metadata:  
   name: app-a-pdb  
 spec:  
   minAvailable: 2  
   selector:  
       matchLabels:  
         app: app-a
         
 
D- Make sure your app is live and ready.
 
Readiness probes are used to determine when a container is ready to recieve traffic.
Liveness probes are used to determine whether a container is healthy or needs to be restarted.


E- Label everything under the sun.


F- namespace resources are not themselves in a namespace. And low-level resources, such as nodes and persistentVolumes, are not in any namespace.
