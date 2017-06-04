---
title: "&lt;emittenteLocale&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 26bdd0df-0e7d-4b9e-bbeb-f28c53769385
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;emittenteLocale&gt;
Specifica l'indirizzo e l'associazione dell'autorità emittente locale da usare per ottenere un token di sicurezza.  
  
## Sintassi  
  
```  
  
<localIssuer address="string"  
      binding="string"  
      bindingConfiguration="string" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|address|Stringa obbligatoria.  Specifica l'URI dell'emittente locale.|  
|associazione|Stringa facoltativa.  Una delle associazioni fornite dal sistema  Per un elenco, vedere [Associazioni fornite dal sistema](../../../../../docs/framework/wcf/system-provided-bindings.md).|  
|bindingConfiguration|Stringa facoltativa.  Specifica una configurazione di associazione presente nel file di configurazione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identità\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Specifica informazioni sull'identità per l'autorità emittente locale.|  
|[\<intestazioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md)|Raccolta di intestazioni di indirizzo richiesta per indirizzare correttamente l'autorità emittente locale.  È possibile usare la parola chiave `add` per aggiungere un'intestazione a questa raccolta.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<tokenEmesso\>](../../../../../docs/framework/configure-apps/file-schema/wcf/issuedtoken.md)|Specifica un token personalizzato usato per autenticare un client presso un servizio.|  
  
## Note  
 Quando si ottiene un token rilasciato da un servizio token di sicurezza \(STS, Security Token Service\), l'applicazione client deve essere configurata con l'indirizzo da usare per comunicare con il servizio token di sicurezza.  Se <xref:System.ServiceModel.WSFederationHttpBinding> non fornisce un URL per il servizio token di sicurezza o se l'indirizzo dell'emittente di un'associazione federativa è http:\/\/schemas.microsoft.com\/2005\/12\/ServiceModel\/Addressing\/Anonymous o `null`, il canale [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] del client usa il valore specificato da `address` e `binding` per comunicare con il servizio token di sicurezza e ottenere il token rilasciato.  Per altre informazioni sulla configurazione di un'autorità emittente locale, vedere [Procedura: configurare un emittente locale](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md).  
  
## Esempio  
 Nell'esempio seguente vengono impostati gli attributi `address`, `binding` e `bindingConfiguration` di un elemento `localIssuer`.  
  
```  
<system.serviceModel>  
 <behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <issuedToken cacheIssuedTokens="false"   
                 defaultKeyEntropyMode="ClientEntropy">  
     <localIssuer address="net.tcp://cohowinery/tokens"   
                  binding="netTcpBinding"  
                  bindingConfiguration="myTcpBindingConfig" />  
    </issuedToken>  
   </clientCredentials>  
  </behavior>  
  </endpointBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.IssuedTokenClientElement.LocalIssuer%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenParametersEndpointAddressElement>   
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Procedura: configurare un emittente locale](../../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)   
 [Identità del servizio e autenticazione](../../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Federazione e token emessi](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Procedura: creare un client federato](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [Federazione e token emessi](../../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)