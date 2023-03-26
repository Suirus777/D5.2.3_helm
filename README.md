# D5.2.3_helm
Minkube, kubectl, docker, helm
<br><br>
<b> Установите Helm Chart prometheus-community/prometheus так, чтобы в нём не было сервисов: </b><br>
- pushgateway; <br>
- node-exporter;  <br>
- alertnamager; <br>
были только следующие поды: <br>
- prometheus-server; <br>
- prometheus-kube-state-metrics. <br>

<b>Ответ: Для выполнения данного задания используется: <br>
  - Minikube с одной нодой <br>
<code> root@helm:/home/odmin/project_helm/prometheus# minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
 </code> <br> 
 - Kubectl  <br>
  <code> root@helm:/home/odmin/project_helm/prometheus# kubectl version
WARNING: This version information is deprecated and will be replaced with the output from kubectl version --short.  Use --output=yaml|json to get the full version.
Client Version: version.Info{Major:"1", Minor:"26", GitVersion:"v1.26.3", GitCommit:"9e644106593f3f4aa98f8a84b23db5fa378900bd", GitTreeState:"clean", BuildDate:"2023-03-15T13:40:17Z", GoVersion:"go1.19.7", Compiler:"gc", Platform:"linux/amd64"}
Kustomize Version: v4.5.7
Server Version: version.Info{Major:"1", Minor:"26", GitVersion:"v1.26.1", GitCommit:"8f94681cd294aa8cfd3407b8191f6c70214973a4", GitTreeState:"clean", BuildDate:"2023-01-18T15:51:25Z", GoVersion:"go1.19.5", Compiler:"gc", Platform:"linux/amd64"}
 </code> <br>
  
  
  
  Был создан "values.yaml" где </b> 




helm upgrade --install --namespace prometheus prometheus prometheus-community/prometheus --values /home/odmin/project_helm/prometheus/values.yaml
