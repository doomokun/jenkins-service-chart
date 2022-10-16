# Jenkins servser chart

# Chart pages
pages: https://doomokun.github.io/jenkins-service-chart

repo: git@github.com:doomokun/jenkins-service-chart.git

branch: gh-pages


# How to use
Install this chart called 'jenkins-service' to namespace 'jenkins-server', use values-jenkins.yaml values
```
$ kubectl create namespace jenkins-server
$ helm install jenkins-service -f values-jenkins.yaml -n jenkins-server .
```

# Package
```
$ helm package .
$ helm repo index . --url https://doomokun.github.io/jenkins-service-chart
```

# Version update
Update Chart.yaml :version and package
```
$ helm package .
$ helm repo index . --url https://doomokun.github.io/jenkins-service-chart
```

# About this project
1. In Chart.yaml, added jenkins into dependencies
2. Get dependencies by Chart.yaml, ```$ helm dep update```
3. Addtional k8s resources in ./template for jenkins
4. New jenkins values ./values-jenkins.yaml
5. 如dependencies要落values，yaml要比dependency name

# Jenkins Repo
link (https://artifacthub.io/packages/helm/jenkinsci/jenkins)

# Infromation of Jenkins (LoadBalancer)
NAME: jenkins-service
LAST DEPLOYED: Sun Oct 16 17:54:15 2022
NAMESPACE: jenkins-server
STATUS: deployed
REVISION: 1
NOTES:
1. Get your 'admin' user password by running:
  kubectl exec --namespace jenkins-server -it svc/jenkins-service -c jenkins -- /bin/cat /run/secrets/additional/chart-admin-password && echo
2. Get the Jenkins URL to visit by running these commands in the same shell:
  NOTE: It may take a few minutes for the LoadBalancer IP to be available.
        You can watch the status of by running 'kubectl get svc --namespace jenkins-server -w jenkins-service'
  export SERVICE_IP=$(kubectl get svc --namespace jenkins-server jenkins-service --template "{{ range (index .status.loadBalancer.ingress 0) }}{{ . }}{{ end }}")
  echo http://$SERVICE_IP:8080/login

3. Login with the password from step 1 and the username: admin
4. Configure security realm and authorization strategy
5. Use Jenkins Configuration as Code by specifying configScripts in your values.yaml file, see documentation: http:///configuration-as-code and examples: https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos

For more information on running Jenkins on Kubernetes, visit:
https://cloud.google.com/solutions/jenkins-on-container-engine

For more information about Jenkins Configuration as Code, visit:
https://jenkins.io/projects/jcasc/


NOTE: Consider using a custom image with pre-installed plugins