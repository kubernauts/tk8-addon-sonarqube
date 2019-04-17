# TK8 addon - SonarQube

## What are TK8 addons?

- TK8 add-ons provide freedom of choice for the user to deploy tools and applications without being tied to any customized formats of deployment.
- Simplified deployment process via CLI (will also be available via TK8 web in future).
- With the TK8 add-ons platform, you can also build your own add-ons.

### Prerequisites

This addon was created for the tk8 cli you could find it here: https://github.com/kubernauts/tk8
Addon integration is supported on Version 0.5.0 and greater

Alternative you can apply the main.yml directly with kubectl

To get more support join us on [Slack](https://kubernauts-slack-join.herokuapp.com)

## What is Sonarqube?

[SonarQube®](http://www.sonarqube.org/) is an automatic code review tool to detect bugs, vulnerabilities and code smells in your code. It can integrate with your existing workflow to enable continuous code inspection across your project branches and pull requests.

## Get Started

You can install SonarQube on the Kubernetes cluster via TK8 addons functionality. What do you need:
- tk8 binary
- A Kubernetes cluster that supports Service objects of type: LoadBalancer

## Deploy Contour on the Kubernetes Cluster

Run **tk8 addon install sonarqube**

    $ tk8 addon install sonarqube
    Search local for sonarqube
    check if provided a url
    Search addon on kubernauts space.
    Cloning into 'sonarqube'...
    Install sonarqube
    execute main.sh
    Creating main.yaml
    add  ./sonarqube-config/00-postgres-secrets.yaml
    add  ./sonarqube-config/01-sonarqube-configmap.yaml
    add  ./sonarqube-config/02-sonarqube-copy-plugins.yaml
    add  ./sonarqube-config/03-sonarqube-install-plugins.yaml
    add  ./sonarqube-config/04-postgres-pvc.yaml
    add  ./sonarqube-config/05-sonarqube-pvc.yaml
    add  ./sonarqube-config/06-postgres-svc.yaml
    add  ./sonarqube-config/07-sonarqube-svc.yaml
    add  ./sonarqube-config/08-postgres-deploy.yaml
    add  ./sonarqube-config/09-sonarqube-deploy.yaml
    apply sonarqube/main.yml
    secret/sonarqube-postgresql created
    configmap/sonarqube-config created
    configmap/sonarqube-copy-plugins created
    configmap/sonarqube-install-plugins created
    persistentvolumeclaim/sonarqube-postgresql created
    persistentvolumeclaim/sonarqube-pvc created
    service/sonarqube-postgresql created
    service/sonarqube created
    deployment.extensions/sonarqube-postgresql created
    deployment.extensions/sonarqube-deploy created
    sonarqube installation complete
This command will clone the https://github.com/kubernauts/tk8-addon-sonarqube repository locally and will create the necessary resources to run SonarQube. This command also creates:
- A service of LoadBalancer type for exposing SonarQube UI
- Setups Postgres for using with SonarQube

## Accessing SonarQube

Once, the addon is deployed successfully, it is quite easy to access the web UI. Firstly, find out the SonarQube service' IP/DNS by running **kubectl get svc -l app=sonarqube**

    $ kubectl get svc -l app=sonarqube
    NAME        TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)          AGE
    sonarqube   LoadBalancer   10.43.150.17   84.200.100.228   9000:30875/TCP   157m
Now, open http://EXTERNAL-IP:9000 in your browser. The default login credentials are admin:admin.

![image](https://user-images.githubusercontent.com/38726510/56272667-7d7e5580-60fb-11e9-924b-9f7e73567c45.png)

If you can see something like the above image, then everything went well. Now, you can proceed with integrating SonarQube with the dev workflows for writing cleaner, bug-free code.

## Uninstall SonarQube

For removing SonarQube from your cluster, we can use TK8 addon's destroy functionality. Run **tk8 addon destroy sonarqube**

    $ tk8 addon destroy sonarqube
    Search local for sonarqube
    Addon sonarqube already exist
    Found sonarqube local.
    Destroying sonarqube
    execute main.sh
    Creating main.yaml
    add  ./sonarqube-config/00-postgres-secrets.yaml
    add  ./sonarqube-config/01-sonarqube-configmap.yaml
    add  ./sonarqube-config/02-sonarqube-copy-plugins.yaml
    add  ./sonarqube-config/03-sonarqube-install-plugins.yaml
    add  ./sonarqube-config/04-postgres-pvc.yaml
    add  ./sonarqube-config/05-sonarqube-pvc.yaml
    add  ./sonarqube-config/06-postgres-svc.yaml
    add  ./sonarqube-config/07-sonarqube-svc.yaml
    add  ./sonarqube-config/08-postgres-deploy.yaml
    add  ./sonarqube-config/09-sonarqube-deploy.yaml
    delete sonarqube from cluster
    secret "sonarqube-postgresql" deleted
    configmap "sonarqube-config" deleted
    configmap "sonarqube-copy-plugins" deleted
    configmap "sonarqube-install-plugins" deleted
    persistentvolumeclaim "sonarqube-postgresql" deleted
    persistentvolumeclaim "sonarqube-pvc" deleted
    service "sonarqube-postgresql" deleted
    service "sonarqube" deleted
    deployment.extensions "sonarqube-postgresql" deleted
    deployment.extensions "sonarqube-deploy" deleted
    sonarqube destroy complete
