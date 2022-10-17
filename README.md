# EPMDEDP-10759

1 - Deploy Jenkins to edp-sandbox cluster via helm. Install Jenkins k8s plugin
Get Repo Info
```
helm repo add jenkins https://charts.jenkins.io
helm repo update
```
Install Chart
```
helm install -f jenkins.yaml jenkins jenkins/jenkins -n ms-onboarding
```
or 
```
helm install -f jenkins.yaml jenkins jenkins/jenkins --namespace ms-onboarding
```
[Jenkins](charts-config/jenkins.yaml) value file 

2 - Create 2 namespaces, dev and prod.
```
kubectl create namespace ms-onboarding-dev
kubectl create namespace ms-onboarding-prod
```
Create [secrets](charts-config/secrets.yaml) to work jenkins jobs. 

3 - Write a [Code Review](Jenkinsfile/Jenkinsfile_review) pipeline
<details><summary> Requirement </summary>

  - checkout the source code from a git repository</p>
  - run hadolint check
</details>
</p>

4 - Write a [Build](Jenkinsfile/Jenkinsfile_build) pipeline
<details><summary> Requirements </summary>

  - checkout the source code</p>
  - build Docker image in k8s agent (it can be a basic python app for example). You can use Kaniko for build image OR any other tool</p>
  - implement image substitution in the helm chart before pushing it to the [Chartmuseum](charts-config/chart-museum.yaml) . Before the push of the Helmchart to the repository, please update the image tag to the current one.

</details>
</p>


5 - Write a [Deploy](Jenkinsfile/Jenkinsfile_deploy) pipeline
<details><summary> Requirements </summary>

  - deploy [helm chart](helm/php-mysql-crud/templates/deployment.yaml) from Chartmuseum into k8s (perform install or rolling upgrade if already installed)
</details>
</p>

Create [service account](charts-config/service-account.yaml) to work jenkins jobs.

6 - Modify your [Deploy](Jenkinsfile/Jenkinsfile_deploy) pipeline 
<details><summary> Requirements </summary>

  - using ENV vars, so it will deploy your app differently, depending on ENV vars
  with 1 replica if ENV = dev, 3 replicas if ENV = prod</p>
  - app should be deployed in different namespaces depending on the same ENV var</p>
  - add 2 Jenkins test secrets (some passwords) for dev and prod</p>
  - pass different k8s secrets (previously created passwords) depending on the same ENV var. Show the display of secrets availability in the current environment.
</details>
</p>


