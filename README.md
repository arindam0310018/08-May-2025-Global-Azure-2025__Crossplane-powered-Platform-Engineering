# Global Azure 2025: Crossplane powered Platform Engineering:-

Greetings and Welcome to another amazing Session in __Global Azure 2025 powered by Azure Zurich User Group.__

Discover how __Crossplane simplifies cloud infrastructure__.

Join me to learn more!

| <img src="Images/01-Global-Azure.jpg" alt="Global Azure"> | <img src="Images/02-AZUG.jpg" alt="Azure Zurich User Group"> |
| --------- | --------- |

| Agenda:- |
| --------- |

| __#__ | __Topics__ |
| --------- | --------- |
| 1. | Introduction to Crossplane and its key feature. |
| 2. | Visual overview: Integration of Crossplane and Azure. |
| 3. | Crossplane Use case. |
| 4. | Setting up Crossplane with Azure. |
| 5. | Deploying Azure resources using Crossplane - Command-Line. |

| 01: Introduction to Crossplane and its key features:- |
| --------- |
| <img src="Images/03-Crossplane.jpg" alt="Crossplane"> |

| Defination:- |
| --------- |

Crossplane is a CNCF project that helps you manage cloud resources in a Kubernetes-native way. 
With Kubernetes, we used to manage only application, but with Crossplane, we can now manage cloud infrastructure.
For Ease of understanding, consider like this -
- With Crossplane, we can write a Kubernetes YAML file, and it will create the desired Cloud Resources (For Example - A Resource Group), directly from Kubernetes cluster.

| Reference Links:- |
| --------- |
- https://www.crossplane.io/
- https://docs.crossplane.io/latest/getting-started/introduction/

| Key Features:- |
| --------- |


| 02: Visual overview: Integration of Crossplane and Azure:- |
| --------- |
| <img src="Images/04-Crossplane-Azure.jpg" alt="Crossplane-Azure"> |


| 03: Crossplane Use cases:- |
| --------- |

| Primary Use case:- |
| --------- |
| Earlier Kubernetes was used only for Containerization and Deployment. Now with Crossplane, Kubernetes can be used to provision Infrastructure using same YAML file and apply it with kubectl. |

| Additional Use cases:- |
| --------- |

| I. GitOps-Based Infrastructure Management |
| --------- |
| Write YAML to describe cloud resources, push it to any Git repository, A tool like FluxCD or ArgoCD notices the change, informs Crossplane to create those resources |
| <img src="Images/06-Crossplane-GitOps.jpg" alt="Crossplane-GitOps">  |
| __II. Multi-Cloud Abstraction__ |
| One tool and one set of instructions to manage resources (not always true) across different cloud providers (like Azure, AWS, and GCP). |
| <img src="Images/07-Crossplane-MultiCloud.jpg" alt="Crossplane-MultiCloud"> |
| __III. Self-Service Platforms__ |
| The platform team (DevOps/SRE) sets up the rules, templates, and permissions using Crossplane. |
| A developer writes a small YAML file and runs using Kubectl. |
| <img src="Images/08-Crossplane-SS.jpg" alt="Crossplane-SS"> |
| __IV. Policy & Security Governance__ |
| Platform teams (DevOps or SREs) define "Compositions". These are like blueprints. |
| Platform teams also apply "constraints or limits". These are like Azure Policies (No Public IPs, Location is West Europe Only, VM Size... |
| Developer creates a resource using YAML. |
| Crossplane checks against these "constraints or limits". |
| Only allowed and safe resources are actually created in the cloud. |
| <img src="Images/09-Crossplane-Policy-Security.jpg" alt="Crossplane-Policy-Security"> |

| 04: Setting up Crossplane with Azure:- |
| --------- |

| Requirements:- |
| --------- |

1. An AKS Cluster (In Azure Cloud)
2. Kubectl (Installed in your working Notbook/VM)
3. Kubelogin (Installed in your working Notbook/VM)
4. Helm (Installed in your working Notbook/VM)

| AKS Cluster Details:- |
| --------- |

- Subscription: __Visual Studio Enterprise Subscription__
- Resource group: __AM-CrossPlane-RG__
- Region: __West Europe__
- Kubernetes cluster name: __AM-Crossplane-AKS__
- Kubernetes version: __1.31.7__
- Automatic upgrade: __patch__
- Automatic upgrade scheduler: __Every week on Sunday (recommended)__
- Node security channel type: __NodeImage__
- Security channel scheduler: __Every week on Sunday (recommended)__
- Node pools: __1__
- Enable virtual nodes: __Disabled__
- Resource identity: __System-assigned managed identity__
- Local accounts: __Disabled__
- Authentication and Authorization: __Microsoft Entra ID authentication with Azure RBAC__
- Encryption type: __(Default) Encryption at-rest with a platform-managed key__
- Private cluster: __Disabled__
- Authorized IP ranges: __Disabled__
- Network configuration: __Azure CNI Node Subnet__
- Virtual network: __AM-CrossPlane-AKS-VNet__
- Cluster subnet: __(new) Container-Subnet__
- Kubernetes service address range: __10.0.0.0/16__
- Kubernetes DNS service IP address: __10.0.0.10__
- DNS name prefix: __AM-Crossplane-AKS-dns__
- Network policy: __Azure__
- Load balancer: __Standard__
- Integrations: __Container registry__ 
- resource group: __AM-CrossPlane-RG__
- Container registry location: __West Europe__
- Container registry admin user: __Enabled__
- Container registry SKU: __Standard__
- Container registry: __(new) AMCrossPlaneACR__
- Service mesh: __Disabled__
- Azure Policy: __Disabled__
- Enable Container Logs: __Disabled__
- Enable Prometheus metrics: __Enabled__
- Azure Monitor workspace: __(new) AM-Azure-Monitor-Workspace-WEU__
- Enable Grafana: __Disabled__
- Alert rules: __2 rules__
- Infrastructure resource group: __AM-CrossPlane-RG_AM-Crossplane-AKS_WestEurope__
- Microsoft Defender for Cloud: __Free__
- OpenID Connect (OIDC): __Enabled__
- Workload Identity: __Enabled__
- Image Cleaner: __Enabled__
- Tags: __None__

| Windows System on which below application was Installed ? |
| --------- |
| Microsoft Windows Server 2022 Datacenter Azure Edition. |

I. __Install Kubectl on Windows.__

| Reference Link: https://community.chocolatey.org/packages/kubernetes-cli |
| --------- |

| Kubectl Installation Logs:- |
| --------- |

```
PS C:\Users\amadmin> choco install kubernetes-cli

Chocolatey v2.4.3
Installing the following packages:
kubernetes-cli
By installing, you accept licenses for the packages.
Downloading package from source 'https://community.chocolatey.org/api/v2/'
Progress: Downloading kubernetes-cli 1.33.0... 100%

kubernetes-cli v1.33.0 [Approved]
kubernetes-cli package files install completed. Performing other installation steps.
The package kubernetes-cli wants to run 'chocolateyInstall.ps1'.
Note: If you don't run this script, the installation will fail.
Note: To confirm automatically next time, use '-y' or consider:
choco feature enable -n allowGlobalConfirmation
Do you want to run the script?([Y]es/[A]ll - yes to all/[N]o/[P]rint): A

Extracting 64-bit C:\ProgramData\chocolatey\lib\kubernetes-cli\tools\kubernetes-client-windows-amd64.tar.gz to C:\ProgramData\chocolatey\lib\kubernetes-cli\tools...
C:\ProgramData\chocolatey\lib\kubernetes-cli\tools
Extracting 64-bit C:\ProgramData\chocolatey\lib\kubernetes-cli\tools\kubernetes-client-windows-amd64.tar to C:\ProgramData\chocolatey\lib\kubernetes-cli\tools...
C:\ProgramData\chocolatey\lib\kubernetes-cli\tools
 ShimGen has successfully created a shim for kubectl-convert.exe
 ShimGen has successfully created a shim for kubectl.exe
 The install of kubernetes-cli was successful.
  Deployed to 'C:\ProgramData\chocolatey\lib\kubernetes-cli\tools'

Chocolatey installed 1/1 packages.
 See the log for details (C:\ProgramData\chocolatey\logs\chocolatey.log).

PS C:\Users\amadmin>

```

| Validate Post Installation:- |
| --------- |

```
PS C:\Users\amadmin> kubectl version --client
Client Version: v1.33.0
Kustomize Version: v5.6.0
PS C:\Users\amadmin>
```

II. __Install kubelogin on Windows.__

| Reference Link:  |
| --------- |


```

```

| Kubelogin ERROR Logs:- |
| --------- |

```
```


III. __Install Helm on Windows.__

| Reference Link: https://community.chocolatey.org/packages/kubernetes-helm |
| --------- |

| Kubectl Installation Logs:- |
| --------- |

```
PS C:\Users\amadmin> choco install kubernetes-helm
Chocolatey v2.4.3
Installing the following packages:
kubernetes-helm
By installing, you accept licenses for the packages.
Downloading package from source 'https://community.chocolatey.org/api/v2/'
Progress: Downloading kubernetes-helm 3.17.3... 100%

kubernetes-helm v3.17.3 [Approved]
kubernetes-helm package files install completed. Performing other installation steps.
The package kubernetes-helm wants to run 'chocolateyInstall.ps1'.
Note: If you don't run this script, the installation will fail.
Note: To confirm automatically next time, use '-y' or consider:
choco feature enable -n allowGlobalConfirmation
Do you want to run the script?([Y]es/[A]ll - yes to all/[N]o/[P]rint): A

Downloading kubernetes-helm 64 bit
  from 'https://get.helm.sh/helm-v3.17.3-windows-amd64.zip'
Progress: 100% - Completed download of C:\Users\amadmin\AppData\Local\Temp\2\chocolatey\kubernetes-helm\3.17.3\helm-v3.17.3-windows-amd64.zip (17.09 MB).
Download of helm-v3.17.3-windows-amd64.zip (17.09 MB) completed.
Hashes match.
Extracting C:\Users\amadmin\AppData\Local\Temp\2\chocolatey\kubernetes-helm\3.17.3\helm-v3.17.3-windows-amd64.zip to C:\ProgramData\chocolatey\lib\kubernetes-helm\tools...
C:\ProgramData\chocolatey\lib\kubernetes-helm\tools
 ShimGen has successfully created a shim for helm.exe
 The install of kubernetes-helm was successful.
  Deployed to 'C:\ProgramData\chocolatey\lib\kubernetes-helm\tools'

Chocolatey installed 1/1 packages.
 See the log for details (C:\ProgramData\chocolatey\logs\chocolatey.log).
PS C:\Users\amadmin>
PS C:\Users\amadmin>

```

| Validate Post Installation:- |
| --------- |

```
PS C:\Users\amadmin> helm version
version.BuildInfo{Version:"v3.17.3", GitCommit:"e4da49785aa6e6ee2b86efd5dd9e43400318262b", GitTreeState:"clean", GoVersion:"go1.23.7"}
PS C:\Users\amadmin>
```

Step 1: __Install Crossplane into your Kubernetes Cluster:-__

kubectl create namespace am-crossplane
```
PS C:\Users\amadmin> kubectl create namespace am-crossplane
namespace/am-crossplane created
PS C:\Users\amadmin>
```
kubectl get namespace
```
PS C:\Users\amadmin> kubectl get namespace
NAME              STATUS   AGE
am-crossplane     Active   18s
default           Active   3h15m
kube-node-lease   Active   3h15m
kube-public       Active   3h15m
kube-system       Active   3h15m
PS C:\Users\amadmin>
```

helm repo add crossplane-stable https://charts.crossplane.io/stable
```
PS C:\Users\amadmin> helm repo add crossplane-stable https://charts.crossplane.io/stable
"crossplane-stable" has been added to your repositories
PS C:\Users\amadmin>
```

helm repo update
```
PS C:\Users\amadmin> helm repo update
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "crossplane-stable" chart repository
Update Complete. ⎈Happy Helming!⎈
PS C:\Users\amadmin>
```

helm install crossplane crossplane-stable/crossplane --namespace am-crossplane
```
PS C:\Users\amadmin> helm install crossplane crossplane-stable/crossplane --namespace am-crossplane
NAME: crossplane
LAST DEPLOYED: Thu May  8 09:19:30 2025
NAMESPACE: am-crossplane
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Release: crossplane

Chart Name: crossplane
Chart Description: Crossplane is an open source Kubernetes add-on that enables platform teams to assemble infrastructure from multiple vendors, and expose higher level self-service APIs for application teams to consume.
Chart Version: 1.19.1
Chart Application Version: 1.19.1

Kube Version: v1.31.7
PS C:\Users\amadmin>
```

kubectl get pods -n am-crossplane
```
PS C:\Users\amadmin> kubectl get pods -n am-crossplane
NAME                                       READY   STATUS    RESTARTS   AGE
crossplane-66f8c4f6f8-7nkzt                1/1     Running   0          47s
crossplane-rbac-manager-564687c9dd-7qlns   1/1     Running   0          47s
PS C:\Users\amadmin>
```

kubectl get deployments -n am-crossplane
```
PS C:\Users\amadmin> kubectl get deployments -n am-crossplane
NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
crossplane                1/1     1            1           4m17s
crossplane-rbac-manager   1/1     1            1           4m17s
PS C:\Users\amadmin>
PS C:\Users\amadmin>
```

Step 2: __Install the Azure Provider:-__

__The Crossplane Provider installs the Kubernetes Custom Resource Definitions (CRDs) representing Azure Networking services. These CRDs allow you to create Azure resources directly inside Kubernetes.__

kubectl get providers
```
PS C:\Users\amadmin> kubectl get providers
No resources found
PS C:\Users\amadmin>
```

kubectl apply -f provider.yaml
```
PS C:\Users\amadmin> cd .\Desktop\
PS C:\Users\amadmin\Desktop> cd .\Crossplane\
PS C:\Users\amadmin\Desktop\Crossplane>
PS C:\Users\amadmin\Desktop\Crossplane> ls


    Directory: C:\Users\amadmin\Desktop\Crossplane


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          5/8/2025   9:33 AM            179 provider.yaml


PS C:\Users\amadmin\Desktop\Crossplane>
PS C:\Users\amadmin\Desktop\Crossplane>
PS C:\Users\amadmin\Desktop\Crossplane> kubectl apply -f provider.yaml
provider.pkg.crossplane.io/provider-azure-network created
PS C:\Users\amadmin\Desktop\Crossplane>
```

kubectl get providers
```
PS C:\Users\amadmin\Desktop\Crossplane> kubectl get providers
NAME                                       INSTALLED   HEALTHY   PACKAGE                                                                AGE
crossplane-contrib-provider-family-azure   True        True      xpkg.crossplane.io/crossplane-contrib/provider-family-azure:v1.11.2    32s
provider-azure-network                     True        True      xpkg.crossplane.io/crossplane-contrib/provider-azure-network:v1.11.2   37s
PS C:\Users\amadmin\Desktop\Crossplane>
```

Step 3: __Create an Azure Service Principal:-__

az ad sp create-for-rbac --sdk-auth --role Owner --scopes /subscriptions/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
PS C:\Users\amadmin\Desktop\Crossplane> az ad sp create-for-rbac --sdk-auth --role Owner --scopes /subscriptions/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
Option '--sdk-auth' has been deprecated and will be removed in a future release.
Creating 'Owner' role assignment under scope '/subscriptions/0e5fbaff-a521-4b8a-88a9-6b02feb20a59'
The output includes credentials that you must protect. Be sure that you do not include these credentials in your code or check the credentials into your source control. For more information, see https://aka.ms/azadsp-cli
{
  "clientId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "clientSecret": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "subscriptionId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "tenantId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
PS C:\Users\amadmin\Desktop\Crossplane>
```

🔥 Important Note: __Save your Azure JSON output as "azure-credentials.json".__










| 05: Deploying Azure resources using Crossplane:- |
| --------- |
