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
  - Helm 3 <br>
  <code> root@helm:/home/odmin/project_helm/prometheus# helm version
version.BuildInfo{Version:"v3.11.2", GitCommit:"912ebc1cd10d38d340f048efaf0abda047c3468e", GitTreeState:"clean", GoVersion:"go1.18.10"}
  </code><br>
  - Далее был создан namespace Prometheus <br>
  <code> #kubectl create ns prometheus </code> <br>
  - Далее задеплоен prometheus в Minikube <br>
  <code> #helm upgrade --install -n prometheus prometheus prometheus-community/prometheus  <br>
  root@helm:/home/odmin/project_helm/prometheus# kubectl get pods -n prometheus
NAME                                                READY   STATUS    RESTARTS   AGE
prometheus-alertmanager-0                           1/1     Running   0          26s
prometheus-kube-state-metrics-7f6769f7c6-bzlth      1/1     Running   0          36m
prometheus-prometheus-node-exporter-w99h5           1/1     Running   0          26s
prometheus-prometheus-pushgateway-684dc6674-74ngj   1/1     Running   0          26s
prometheus-server-68f6dcdbb9-dnjnz                  2/2     Running   0          36m </code>
  - Следующим этапом был создан "values.yaml" с следующими настройками: <br>
  <code>
prometheus-pushgateway:
  enabled: false
prometheus-node-exporter:
  enabled: false
alertmanager:
  enabled: false
prometheus-server:
  enabled: true
prometheus-kube-state-metrics:
  enabled: true
  </code>
  - Применяем данные настройки с учётом "values.yaml" <br>
  <code> #helm upgrade --install --namespace prometheus prometheus prometheus-community/prometheus --values values.yaml </code>
  - Результат: <br>
  <code> root@helm:/home/odmin/project_helm/prometheus# kubectl get pods -n prometheus
NAME                                             READY   STATUS    RESTARTS   AGE
prometheus-kube-state-metrics-7f6769f7c6-bzlth   1/1     Running   0          45m
prometheus-server-68f6dcdbb9-dnjnz               2/2     Running   0          45m
  </code>
</b> 





