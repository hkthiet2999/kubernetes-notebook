# Deploy an app

# Deploy using kubectl

Tạo một Deployment kubernetes-bootcamp

`kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`

![](images/1.png)

Expose deployment kubernetes-bootcamp kubernetes-bootcamp

`kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080`

`kubectl describe services/kubernetes-bootcamp`

![](images/2.png)

Tạo một deployment mới, cc bước thực hiện dựa trên: [Day05-Jun-8/3.Deploy-Containers-Using-Kubectl](https://github.com/smoothkt4951/kubernetes-notebook/tree/main/Day05-Jun-8/3.Deploy-Containers-Using-Kubectl)

![](images/3.png)

Thử ping thì bị lỗi 😥

![](images/err.png)

# Deploy using YAML
