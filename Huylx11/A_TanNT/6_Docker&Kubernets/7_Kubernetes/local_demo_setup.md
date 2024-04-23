# 1. cài đặt docker

# 2. cài đặt minikube
- tượng trưng cho 1 node cluster, cả master process và worker process đều chạy trên node này

# 3. cài đặt các package kubectl
- tool để tương tác với API server hoặc tool để điều khiển K8S 
- kubectl là package đi kèm với minikube

# 4. chạy minikube local cluster
- `minikube start --no-vtx-check` để chạy mà không cần check có vtx hay không, `minikube start --vm-driver=virtualbox` để chạy minikube trong virtualbox đã cài trên máy (k8s cần hoạt động trên môi trường ảo)
- `minikube start` để chạy minikube đã có sẵn

> sử dụng `kubectl command` để điều chỉnh cluster trong minikube, `minkube command` dùng để start up/delete các cluster

# 5. main kubectl command
- `kubectl get pod`: status của các pod
- 
