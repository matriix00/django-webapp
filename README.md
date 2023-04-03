# Demo
![Image](images/webapp-started.png)

## Brief
- Deploy a django webapp on kubernetes using helm chart.
- Monitoring django webapp logs using Loki and Promtail. 


![Image](images/Loki.png)

## Pre-requisits:
* Setup K8s , I used eks on AWS using terrafrom to build my infrastructure on "AWS" [My infra repo ](https://github.com/matriix00/finalproject/tree/master/terraform)
   then create use terraform commands to build this infra.

* Install [Helm](https://helm.sh/docs/intro/install/) on your local machine.
* Install [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) on your local machine to be able to run kubectl commands.

## Tools Used
<p align="center">
<a href="https://aws.amazon.com/" target="_blank" rel="noreferrer"> 
<img src="images/aws.png" alt="aws" width="90" height="80"/>
</a>
<a href="https://www.terraform.io/" target="_blank" rel="noreferrer">
<img src="images/terraform.png" alt="terraform" width="90" height="80"/>
</a>
<a href="https://kubernetes.io/" target="_blank" rel="noreferrer">
<img src="images/k8s.png" alt="k8s" width="90" height="80"/>
<a href="https://helm.sh/" target="_blank" rel="noreferrer">
<img src="images/helm.png" alt="helm" width="90" height="80"/>

<a href="https://grafana.com/oss/loki/" target="_blank" rel="noreferrer">
<img src="images/loki-grafana.png" alt="loki" width="90" height="80"/>
</a> 
</p>

## :rocket: Get started

### Cloning this project
```bash
$ git clone https://github.com/matriix00/django-webapp.git
```
* First we use helm to install (deploy) django chart on k8s .


```bash
$ helm install release1 django-chart/ --namespace django-namespace --create-namespace
```
* Now u can open you web app using loadbalancer url
```bash
kubectl get svc -n django-namespace
```
and add this to url

```bash
:8000/myfood/home/

```

* Second we use helm to install(deploy) grafana loki and grafan promtail charts .
```bash
$ helm upgrade --install loki grafana/loki-stack  --set grafana.enabled=true,prometheus.enabled=true,promtail.enabled=true
```

* Third we should get password to login into grafana
```bash
kubectl get secret loki-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
To access the Grafana UI, run the following command:

```bash
kubectl port-forward service/loki-grafana 3000:80
```
* Now u can open grafana ui 

```bash
http://localhost:3000/
```



### Hopefully I helped you with anything.
## Clean
- Please make sure to Destroy the resources once the testing is over to save the billing.
```bash
$ helm uninstall release1
$ terraform destroy -auto-approve

```
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.