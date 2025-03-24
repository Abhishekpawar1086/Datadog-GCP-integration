# Datadog-GCP-integration
# Step1- Create one Vm or existing Vm and install Datadog Agent on it 
sudo apt-get update
DD_API_KEY=(                       ) DD_SITE="us5.datadoghq.com" bash -c "$(curl -L https://install.datadoghq.com/scripts/install_script_agent7.sh)"
