# Datadog-GCP-integration
# Step1- Create one Vm or existing Vm and install Datadog Agent on it 
sudo apt-get update
DD_API_KEY=(                       ) DD_SITE="us5.datadoghq.com" bash -c "$(curl -L https://install.datadoghq.com/scripts/install_script_agent7.sh)"

 Step 2- Now You need to cretate conectivity between datadog and Gcp
 
![image](https://github.com/user-attachments/assets/d9913173-e609-4948-babf-fdb710efbd7b)

 Step 3- You need to add datadog principle to Gcp Service Account and Gcp Service Account To data dog email for 2 way Authentication
 
![image](https://github.com/user-attachments/assets/7bca0e30-06e4-44fa-9519-cbc78be58a33)

 Step 4- Add a required permission to that prinsiple 
 
![image](https://github.com/user-attachments/assets/f48fa248-e1c7-4e09-803f-fc6c825642f6)

 Now With This Steps you crate the authentication with Gcp with that specific project so any resource you create in this gcp project you just need to add that data dog agent 

 # Datadog-docker-integration
 step 1 you need to install Docker in Your Vm first 
 
 step 2 and than /etc/datadog-agent/conf.d/docker.d/docker_daemon.yaml
 inside this yaml file 
 
 ![image](https://github.com/user-attachments/assets/3ad4e705-af41-48f8-8051-f18d6a171311)
 
 step 3 and restart data dog agent 
 no inside your datadog container you can see all container in ui

 # Datadog-K8s-integration
step 1 

helm repo add datadog https://helm.datadoghq.com   //This adds Datadog's official Helm chart repository to your local Helm setup.

helm install datadog-operator datadog/datadog-operator  // Installs the Datadog Operator in your current Kubernetes namespace.
                                                        // The Operator will watch for DatadogAgent custom resources (CRDs) to deploy Agents.

kubectl create secret generic datadog-secret --from-literal api-key=<DATADOG_API_KEY>        //This securely stores the API key as a Kubernetes Secret named datadog-secret

step 2 create // datadog-agent.yaml

apiVersion: datadoghq.com/v2alpha1
kind: DatadogAgent
metadata:
  name: datadog
spec:
  global:
    clusterName: kubernetes-clusterv1
    site: us5.datadoghq.com
    credentials:
      apiSecret:
        secretName: datadog-secret
        keyName: api-key
        
step 3 kubectl apply -f datadog-agent.yaml
What Happens Next?
The Datadog Operator detects the DatadogAgent custom resource.

It deploys the following components:

Datadog Agent Pods (DaemonSet for node-level monitoring).

Cluster Agent (Optional, for cluster-wide metrics).

Kube State Metrics (Optional, for Kubernetes object metrics).

The Agent starts collecting:

Node metrics (CPU, memory, disk).

Kubernetes metrics (pods, deployments).

Logs (if configured).

APM traces (if enabled).






