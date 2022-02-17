#### Pod: Life Cycle
- **Pending:** API->etcd, pod created, pod id created, but not running on the node.
- **Creating:** Scheduler take pod from etcd, assing on node. Kubelet on the Node pull images from docker registry or repository.
- **ImagePullBackOff:** Kubelet can not pull image from registry. E.g. Image name is fault (typo error), Authorization Failure, Username/Pass error.
- **Running:** 
    - Container closes in 3 ways:
        1. App completes the mission and closes automatically without giving error,
        2. Use or System sends close signal and closes automatically without giving error,
        3. Giving error, collapsed and closes with giving error code. 
    - Rastart Policies (it can defined in the pod definition): 
        1. Always: Default value, kubelet starts always when closing with or without error, 
        2. On-failure: It starts again when it gets only error, 
        3. Never: It never restarts in any case.
 - **Successed (completed)**: If the container closes successfully without error and restart policy is configured as on-failure/never, it converts to succeed.
 - **Failed**
 - **CrashLoopBackOff:** 
    - If restart policy is configured as always and container closes again and again, container restarts again and again (Restart waiting duration before restarting again: 10 sec -> 20 sec -> 40 sec -> .. -> 5mins), It runs every 5 mins if the pod is crashed.
    - If container runs more than 10 mins, status converted from 'CrashLoopBackOff' to 'Running'.