---
title: "&lt;message&gt; di &lt;netMsmqBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6ebf0240-d7be-4493-b0fe-f00fd5989d77
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;message&gt; di &lt;netMsmqBinding&gt;
Definisce le impostazioni di sicurezza dei messaggi SOAP in questa associazione `netMsmqBinding`.  
  
## Sintassi  
  
```  
  
<netMsmqBinding>  
    <binding>  
      <security>  
         <message   
                      algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"  
            clientCredentialType="None/Windows/UserName/Certificate/CardSpace" />  
    </security>  
</netMsmqBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|algorithmSuite|Imposta la crittografia del messaggio e gli algoritmi di incapsulamento della chiave usati per ottenere la sicurezza basata su messaggi per i messaggi inviati sul trasporto MSMQ.<br /><br /> Il valore predefinito è `Aes256`.  L'attributo è di tipo <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.|  
|clientCredentialType|Specifica il tipo di credenziale da usare se l'autenticazione client viene eseguita per i messaggi inviati sul trasporto MSMQ.  Di seguito vengono elencati i valori validi:<br /><br /> -   None: consente al servizio di interagire con i client anonimi.  Né il servizio né il client richiedono una credenziale.<br />-   Windows: consente lo svolgimento degli scambi SOAP nel contesto autenticato di una credenziale di Windows.  In questo caso viene sempre eseguita l'autenticazione basata su Kerberos.<br />-   UserName: consente al servizio di richiedere che il client venga autenticato tramite una credenziale UserName.  In questo caso la credenziale deve essere specificata mediante il comportamento `clientCredentials`. **Caution:**  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] non supporta l'invio di un digest delle password, né la derivazione delle chiavi basata su password, né l'uso di tali chiavi per implementare la sicurezza dei messaggi.  Di conseguenza, quando si usano le credenziali UserName, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] richiede che lo scambio sia protetto.  Questa modalità richiede che sia specificato il certificato del servizio sul lato client mediante il comportamento `clientCredential` e `serviceCertificate`. <br /><br /> -   Certificate: consente al servizio di richiedere che il client venga autenticato tramite un certificato.  La credenziale client in questo caso deve essere specificata tramite il comportamento `clientCredentials`.  In questo caso la credenziale del servizio deve essere specificata usando il comportamento `clientCredentials` tramite la specifica di `serviceCertificate`.<br />-   CardSpace: consente al servizio di richiedere che il client venga autenticato tramite un CardSpace.  Il provisioning del certificato `serviceCertiifcate` deve essere eseguito nel comportamento `clientCredential`.<br /><br /> Il valore predefinito è `Windows`.  L'attributo è di tipo <xref:System.ServiceModel.MessageCredentialType>.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-netmsmqbinding.md)|Definisce le impostazioni di sicurezza per un'associazione.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.MessageSecurityOverMsmqElement>   
 <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement.Message%2A>   
 <xref:System.ServiceModel.NetMsmqSecurity.Message%2A>   
 <xref:System.ServiceModel.MessageSecurityOverMsmq>   
 [Code in WCF](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)