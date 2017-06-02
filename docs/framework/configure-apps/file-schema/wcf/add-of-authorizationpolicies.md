---
title: "&lt;add&gt; di &lt;authorizationPolicies&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 613a03d8-4384-4556-bce2-8c23286c0bb0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;add&gt; di &lt;authorizationPolicies&gt;
Specifica i criteri di autorizzazione per la trasformazione di attestazioni.  
  
## Sintassi  
  
```  
  
<authorizationPolicies>  
   <add policyType="String" />  
</authorizationPolicies>  
```  
  
## Tipo  
 `Type`  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`policyType`|Attributo stringa obbligatorio.<br /><br /> Il modello di controllo di accesso di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] supporta il provisioning di un set di criteri di autorizzazione come tipi.  Questo attributo specifica un criterio di autorizzazione che consente la trasformazione di un set di attestazioni di input in un altro set di attestazioni.  Su questa base può essere concesso o negato il controllo di accesso.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<authorizationPolicies\>](../../../../../docs/framework/configure-apps/file-schema/wcf/authorizationpolicies.md)|Specifica una raccolta di tipi di criteri di autorizzazione.|  
  
## Note  
 Ciascun criterio di autorizzazione contiene un solo attributo `policyType` obbligatorio che è una stringa.  L'attributo specifica un criterio di autorizzazione che consente la trasformazione di un set di attestazioni di input in un altro set di attestazioni.  Su questa base può essere concesso o negato il controllo di accesso.  Per altre informazioni sul funzionamento dei criteri di autorizzazione, vedere <xref:System.IdentityModel.Policy.IAuthorizationPolicy> e [Criteri di autorizzazione](../../../../../docs/framework/wcf/samples/authorization-policy.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A>   
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>   
 <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElement>   
 <xref:System.ServiceModel.Configuration.ServiceAuthorizationElement.AuthorizationPolicies%2A>   
 <xref:System.ServiceModel.Configuration.AuthorizationPolicyTypeElementCollection>   
 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>   
 [Autorizzazione dell'accesso alle operazioni del servizio](../../../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md)   
 [Procedura: creare un gestore autorizzazioni personalizzato per un servizio](../../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)   
 [\<add\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-authorizationpolicies.md)   
 [Criteri di autorizzazione](../../../../../docs/framework/wcf/samples/authorization-policy.md)