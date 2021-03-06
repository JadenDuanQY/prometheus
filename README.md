# 基于Prometheus+alertmanager的kubernetes监控方案

## 部署环境

openshift

## 组件

* prometheus
* alertmanager
* node exporter

## 预操作

* 修改yaml文件中namespace为实际部署project
* 角色授权  
`oc adm policy add-scc-to-user privileged -njaden-test -z default`
* 修改pv中的挂载配置与pv&pvc中的存储配置

## 部署

### node exporter
`oc project $NAMESPCE`  
`oc apply -f node-exporter-daemonset.yaml`  

### prometheus

```
  oc apply -f prometheus-ClusterRole.yaml  
  oc apply -f prometheus-ServiceAccount.yaml  
  oc apply -f prometheus-ClusterRoleBinding.yaml  
  oc apply -f prometheus-service.yaml  
  oc apply -f prometheus-config.yaml  
  oc apply -f prometheus-rule-config.yaml  
  oc apply -f prometheus-pv.yaml  
  oc apply -f prometheus-pvc.yaml  
  oc apply -f prometheus-deployment.yaml
```

### alertmanager

配置alertmanager-config中的邮件收发人
```
  oc apply -f alertmanager-service.yaml  
  oc apply -f alertmanager-config.yaml  
  oc apply -f alertmanager-pv.yaml  
  oc apply -f alertmanager-pvc.yaml  
  oc apply -f alertmanager-deployment.yaml  
```

## api
https://prometheus.io/docs/prometheus/latest/querying/api/#alerts
## prometheus kubernetes config
https://github.com/prometheus/prometheus/blob/master/documentation/examples/prometheus-kubernetes.yml
