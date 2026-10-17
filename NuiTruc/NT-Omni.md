# System Context

```mermaid
flowchart LR
  NTAdmin --> NTOmni
  TenantUser --> NTOmni
  EndCustomer --> TenantApp[Tenant App </br> Phone, Zalo, Web,...]
  TenantApp --> |"chat, call, upload"| NTOmni
  NTOmni --> ExternalLLM[External LLM Providers]
  NTOmni --> PaymentGW[Payment Gateways]
  NTOmni --> TenantCRM[Tenant CRM/ERP]
  NTOmni --> Channels["Channels: Zalo, Facebook, SIP, Web"]
```
