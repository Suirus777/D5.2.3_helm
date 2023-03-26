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
  - Minikube с одной нодой
<code> root@helm:/home/odmin/project_helm/prometheus# minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
 </code>  
  
  
  
  
  Был создан "values.yaml" где </b> 




helm upgrade --install --namespace prometheus prometheus prometheus-community/prometheus --values /home/odmin/project_helm/prometheus/values.yaml
