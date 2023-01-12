helm install capz1 charts/azure-managed-cluster/  \
--namespace default \
--set subscriptionID="${AZURE_SUBSCRIPTION_ID}" \
--set identity.clientId="${AZURE_CLIENT_ID}" \
--set identity.tenantId="${AZURE_TENANT_ID}" \
--set cluster.resourceGroupName=aksclusters \
--set cluster.nodeResourceGroupName=capz1 \
--set cluster.name=aks1 \
--set controlplane.sshPublicKey="$(cat ~/.ssh/id_rsa.pub)" \
--set agentpools[0].name=capz1np0 \
--set agentpools[0].mode=System \
--set agentpools[0].nodecount=1 \
--set agentpools[0].sku=Standard_B2s \
--set agentpools[0].osDiskSizeGB=100 \
--set agentpools[1].name=capz1np1 \
--set agentpools[1].mode=User \
--set agentpools[1].nodecount=1 \
--set agentpools[1].sku=Standard_B2s \
--set agentpools[1].osDiskSizeGB=100


helm template capz1 charts/azure-managed-cluster/  \
--namespace default \
--set subscriptionID="${AZURE_SUBSCRIPTION_ID}" \
--set identity.clientId="${AZURE_CLIENT_ID}" \
--set identity.tenantId="${AZURE_TENANT_ID}" \
--set cluster.resourceGroupName=aksclusters \
--set cluster.nodeResourceGroupName=capz1 \
--set cluster.name=aks1 \
--set controlplane.sshPublicKey="$(cat ~/.ssh/id_rsa.pub)" \
--set agentpools[0].name=capz1np0 \
--set agentpools[0].mode=System \
--set agentpools[0].nodecount=1 \
--set agentpools[0].sku=Standard_B2s \
--set agentpools[0].osDiskSizeGB=100 \
--set agentpools[1].name=capz1np1 \
--set agentpools[1].mode=User \
--set agentpools[1].nodecount=1 \
--set agentpools[1].sku=Standard_B2s \
--set agentpools[1].osDiskSizeGB=100


helm template capz1 charts/azure-managed-cluster/  \
--namespace test \
--set subscriptionID="${AZURE_SUBSCRIPTION_ID}" \
--set identity.clientId="${AZURE_CLIENT_ID}" \
--set identity.tenantId="${AZURE_TENANT_ID}" \
--set cluster.resourceGroupName=aksclusters \
--set cluster.nodeResourceGroupName=capz1 \
--set cluster.name=aks1 \
--set controlplane.sshPublicKey="$(cat ~/.ssh/id_rsa.pub)"


kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -n tooling-untrusted-aks-westus2

helm template pankajtestaks01 charts/azure-managed-cluster/  \
--namespace pankajtestaks01 \
--set subscriptionID="${AZURE_SUBSCRIPTION_ID}" \
--set identity.clientId="${AZURE_CLIENT_ID}" \
--set identity.tenantId="${AZURE_TENANT_ID}" \
--set controlplane.sshPublicKey="$(cat ~/.ssh/id_rsa_azure_cluster_jenkins.pub)" \
-f charts/azure-managed-cluster/values-cluster1.yaml > pankajtestaks01.yaml
