<div align="center">

<!-- BANNER ANIMADO -->
<img src="https://raw.githubusercontent.com/alexandreglima-web/cloud-security-portfolio/main/assets/banner.svg" alt="Alexandre Lima — DevOps Engineer" width="100%"/>

# Alexandre Lima
### Azure DevOps Engineer | AKS | IaC Bicep | Microsoft 365 | Intune MDM/MAM | Entra ID | Governança & FinOps

![Azure](https://img.shields.io/badge/Microsoft_Azure-Expert-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![AKS](https://img.shields.io/badge/AKS-Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![DevOps](https://img.shields.io/badge/Azure_DevOps-CI%2FCD-0078D4?style=for-the-badge&logo=azuredevops&logoColor=white)
![M365](https://img.shields.io/badge/Microsoft_365-Intune_MDM-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

</div>

---

## 🧑‍💻 Sobre

Profissional com **+20 anos em engenharia de infraestrutura enterprise**, especializado em operação, automação e segurança de clusters Kubernetes no Azure (AKS). Experiência em pipelines CI/CD via Azure DevOps (YAML multi-stage), IaC com Bicep e Terraform, e observabilidade com Log Analytics KQL. Histórico de operação de ambientes com **200+ workloads** em topologia Hub-Spoke, integração híbrida FortiGate VPN BGP, e governança via Azure Policy, RBAC e PIM. Atuação em M365 com administração de **1.600+ usuários** via Microsoft Intune, Entra ID e Graph API.

---

## 🛠️ Stack Técnico

```yaml
role:     Azure DevOps Engineer
company:  W4Clouds Brasil — alocado na Profarma / Rede d1000
location: Rio de Janeiro, RJ — Remoto / Híbrido

kubernetes:
  - AKS node pools System (D4s_v3) / User (D8s_v3), Cluster Autoscaler, KEDA
  - Azure CNI, subnet /22 para IPAM de pods, Network Policy Calico
  - Managed Identity AcrPull, OPA/Gatekeeper, Pod Disruption Budgets
  - Private Cluster, Private Endpoints ACR/KeyVault/Storage

cicd:
  - Azure DevOps Pipelines YAML multi-stage, environments, approvals, gates
  - Docker multi-stage build, ACR geo-replication, Content Trust
  - Rollback automático em falha de deployment gate

iac:
  - Bicep modules parametrizados por ambiente dev/hml/prd
  - Terraform provider azurerm 3.x, remote backend state locking (Blob lease)
  - PowerShell Az module — automação operacional e compliance

observabilidade:
  - Log Analytics KQL — CrashLoopBackOff, CPU node, restart count
  - Container Insights, Application Insights .NET dependency tracking

seguranca:
  - NSG deny-all-default, Azure Policy 12+ initiatives, RBAC custom roles
  - PIM JIT 8h, FortiGate NVA VPN site-to-site IKEv2/IPSec BGP AS65001/AS65000

m365_intune:
  - Entra ID Conditional Access, BitLocker AES-XTS 256 via Intune MEM
  - Graph API — auditoria automatizada de 1.600+ licenças M365 E3
  - MDM/MAM compliance policies integradas ao Conditional Access

finops:
  - Cost Management rightsizing, Reserved Instances, Power BI chargeback
  - Redução 18% custo compute via rightsizing B4ms→B2s documentado
```

---

## 🏗️ Arquitetura de Referência — Hub-Spoke AKS + FortiGate NVA

```mermaid
graph TB
    subgraph OnPrem["🏢 On-Premises — Profarma"]
        FW["🔥 FortiGate<br/>AS 65000<br/>IPSec IKEv2"]
        DC["🖥️ Domain Controller<br/>Active Directory<br/>Kerberos AES-256"]
        EP["💻 Endpoints<br/>BitLocker AES-XTS 256<br/>TPM 2.0"]
    end

    subgraph Azure["☁️ Microsoft Azure"]
        subgraph Hub["🔵 Hub VNet — 10.0.0.0/16"]
            VGW["🌐 VPN Gateway<br/>VpnGw2<br/>BGP AS 65001"]
            FGT["🔥 FortiGate NVA<br/>via UDR<br/>SSL Deep Inspection"]
        end

        subgraph Spoke1["🟢 Spoke 1 — AKS Produção"]
            AKS["⚙️ AKS Cluster<br/>Azure CNI /22<br/>Calico Network Policy"]
            ACR["📦 ACR<br/>Geo-replication<br/>Content Trust"]
            KV["🔑 Key Vault<br/>Private Endpoint"]
        end

        subgraph Spoke2["🟡 Spoke 2 — M365 / Segurança"]
            INTUNE["📱 Microsoft Intune<br/>MDM/MAM"]
            EID["🔑 Entra ID<br/>Conditional Access + PIM"]
            GRAPH["📡 Microsoft Graph API<br/>License Audit 1.600+ users"]
        end

        subgraph Observ["🔍 Observabilidade"]
            LA["📊 Log Analytics<br/>KQL Queries"]
            CI["🖥️ Container Insights"]
        end
    end

    subgraph Pipelines["⚙️ Azure DevOps"]
        PIPE["YAML multi-stage<br/>Build → Staging → Prod"]
        BICEP["IaC<br/>Bicep + Terraform"]
    end

    FW <-->|"BGP over IPSec"| VGW
    VGW --> FGT
    FGT --> Spoke1
    FGT --> Spoke2
    DC --- EP
    INTUNE --> EP
    EID --> INTUNE
    AKS --> LA
    AKS --> CI
    PIPE --> ACR
    PIPE --> AKS
    BICEP --> Spoke1

    style Hub fill:#1a3a5c,color:#fff,stroke:#0078D4
    style Spoke1 fill:#1a4a2c,color:#fff,stroke:#00a86b
    style Spoke2 fill:#4a3a1a,color:#fff,stroke:#f4c842
    style OnPrem fill:#3a1a1a,color:#fff,stroke:#ee3124
    style Observ fill:#2a1a4a,color:#fff,stroke:#7B42BC
    style Pipelines fill:#1a2a3a,color:#fff,stroke:#0078D4
```

---

## 🎬 Arquitetura em Movimento

<div align="center">
<img src="https://raw.githubusercontent.com/alexandreglima-web/cloud-security-portfolio/main/assets/architecture_animated.gif" alt="Azure Hub-Spoke Architecture" width="100%"/>
</div>

> Fluxo de tráfego: VPN BGP on-prem ↔ Azure, FortiGate NVA inspecionando tráfego East-West, AKS workloads com Network Policy Calico, Intune gerenciando endpoints via MDM.

---

## 📁 Projetos em Destaque

| Projeto | Descrição | Stack |
|---------|-----------|-------|
| CVE-2026-20833 RC4/Kerberos | Assessment C4 Level 4 e plano de remediação 5 fases para AD Kerberos | PowerShell, AD, KDCSVC |
| M365 E3 License Audit | Auditoria automatizada 1.600+ licenças via Graph API + dashboard Excel | Python, Graph API, openpyxl |
| Azure RG Activity Auditor | 90 dias de Activity Logs por Resource Group com exportação Excel colorido | Python, Azure REST API |
| AKS Hub-Spoke Deployment | Cluster AKS privado com Azure CNI /22, Calico, OPA/Gatekeeper via Bicep | Bicep, Terraform, AKS |

---

## 🏅 Badges

<div align="center">

![AKS](https://img.shields.io/badge/AKS-Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Azure DevOps](https://img.shields.io/badge/Azure_DevOps-CI%2FCD-0078D4?style=flat-square&logo=azuredevops&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Bicep](https://img.shields.io/badge/IaC-Bicep-0078D4?style=flat-square&logo=microsoftazure)
![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)
![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat-square&logo=powershell&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Intune](https://img.shields.io/badge/Intune-MDM%2FMAM-0078D4?style=flat-square&logo=microsoft)
![Graph API](https://img.shields.io/badge/Graph_API-0078D4?style=flat-square&logo=microsoft)
![FortiGate](https://img.shields.io/badge/Fortinet-FortiGate_NVA-EE3124?style=flat-square&logo=fortinet)
![Active Directory](https://img.shields.io/badge/Active_Directory-0078D4?style=flat-square&logo=microsoft)
![Log Analytics](https://img.shields.io/badge/Log_Analytics-KQL-0078D4?style=flat-square&logo=microsoftazure)
![Entra ID](https://img.shields.io/badge/Entra_ID-0078D4?style=flat-square&logo=microsoft)

</div>

