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
