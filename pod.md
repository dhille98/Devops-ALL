### k8s-sree cls pod & replicaset
----------------------------
* pods run are one or more containers 
# single point of failure means all pods are run single nodes 
# set the alias commands 
```
    nano .bashrc
      
      ku=kubectl
      pods="ku get pods"

## find the nodes in k8s cluster
    ```
      ku get no
    ```
### Q. what is different between kubectl create and apply
    
    * create --> create is the impertative commands 
    * apply --> useing manifast or ymal

# create pod by using implicit 
    ```
    ku run pod1 --image nginx
    
    ku get po
    ```
## get all namespace pods
    ```
    ku get po -A

    ```

## create yml formate pod 
    ```
    ku run pod2 --image nginx:latest --dry-run -o yaml
    ```
## create pod 
    ```
     echo ' write yml file ' | ku create -f -
    ``` 
# login pod
    ```
    ku exec -it test1 -- bash
    ```
# in detail information of the pod
    ```
    ku get po -o wide
    ```
# if pod can not schedule on node you can use this usecase of node update a
    ```
    ku cordon node-2
    ku get po -o wide
    ku get no
    ```
# holl node pods are drain 
 ```
  ku drain node-2 --ingnor-daemonsets --force
  ku get po
  ku uncordon node-2
  ku get po
  ```
# checking pod connection with access out side or inside  
* inside kubernetes pod is not is accessed use this commands
    ```
    ku port-forward pod/pod3 --address 0.0.0.0 8000:80
    ```

# checking the internal ports   
    ```
     sudo apt install net-tools
     netstat -nltp
    ```
# in pod run multi container how to set up access in the command 
    ```
     ku get po
     ku port-forward pod/multi -- address 0.0.0.0 8080:80 9000:80
     ku get po
     ku port-forward pod/multi-pod --address 0.0.0.0 8000:80 9000:8080
     ku port-forward pod/multi-pod --address 0.0.0.0 8000:80 9000:8080 &
     ku delete po multi
    ```
 # Note:
    'ENTRYPOINT' docker file is equl to in pod spec "cmd"
    'CMD' docker file equal to "args"

## replica set:
============ 
* in kubernetes Replicaset maintances pods, it is run on loops for explane ypu can delete pod replicaset will create pod. rs maintances diser state the pod 

    ```
    ku get po
    ku run pod1 --image nginx
    ku get po
    ku get po
    ku run pod1 --image nginx
    ku get po
    echo ' ' | ku apply -f -
    ku get all
   ku get po
   ```

# attached to label on pods 
    ```
     ku label pod pod1 tier=yoga
     ku label pod pod3 tier=yoga
     ku get po
     ku label pod multi-pod tier=yoga
     ku get po
   ```
# edit the pod / replica set /deployment use the command  
    ```
     ku edit rs yoga
     ku delete po --all
     ku get po

    ```

# scale out/in the replicas use the command 
     ```
    ku scale rs <name-rs> --replicas 6
    ku scale rs <name-rs> --replicas 6
     ```
# Note:
    RS automatically not update the image you can delete older version pods that time update the pods new version