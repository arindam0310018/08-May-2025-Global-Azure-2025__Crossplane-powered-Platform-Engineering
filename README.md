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


| 05: Deploying Azure resources using Crossplane:- |
| --------- |
