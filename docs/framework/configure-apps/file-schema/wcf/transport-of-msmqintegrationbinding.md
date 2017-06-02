---
title: "&lt;transport&gt; di &lt;msmqIntegrationBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 054579e3-7fdd-47df-99ca-952706ba5c8e
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# &lt;transport&gt; di &lt;msmqIntegrationBinding&gt;
Definisce le impostazioni di sicurezza per il trasporto di integrazione di Accodamento messaggi.  
  
## Sintassi  
  
```  
  
<security>  
    <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"  
        msmqEncryptionAlgorithm="RC4Stream/AES"  
        msmqProtectionLevel="None/Sign/EncryptAndSign"  
        msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
</security>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`msmqAuthenticationMode`|Specifica come deve essere autenticato il messaggio dal trasporto MSMQ.  Se viene impostato su `None`, anche il valore dell'attributo `msmqProtectionLevel` deve essere impostato su `None`.<br /><br /> Di seguito vengono elencati i valori validi:<br /><br /> -   None: nessuna autenticazione<br />-   WindowsDomain: il meccanismo di autenticazione usa Active Directory per ottenere il certificato X.509 per il SID associato al messaggio.  Questo viene quindi usato per controllare l'ACL della coda in modo da garantire che l'utente disponga dell'autorizzazione per scrivere nella coda.<br />-   Certificate: il canale ottiene il certificato dall'archivio certificati.<br /><br /> Il valore predefinito è WindowsDomain.  L'attributo è di tipo <xref:System.ServiceModel.MsmqAuthenticationMode>.|  
|`msmqEncryptionAlgorithm`|Specifica l'algoritmo da usare per la crittografia del messaggio in transito durante il trasferimento dei messaggi tra i gestori della coda dei messaggi.  Di seguito vengono elencati i valori validi:<br /><br /> -   RC4Stream<br />-   AES<br /><br /> Il valore predefinito è RC4Stream.  L'attributo è di tipo <xref:System.ServiceModel.MsmqEncryptionAlgorithm>.|  
|`msmqProtectionLevel`|Specifica come viene protetto il messaggio a livello del trasporto MSMQ.  La crittografia assicura l'integrità del messaggio mentre EncryptAndSign assicura sia l'integrità che il non ripudio del messaggio; ovvero, il messaggio proviene effettivamente dal mittente e il mittente è quello che dichiara di essere.<br /><br /> -   Di seguito vengono elencati i valori validi:<br />-   None: nessuna protezione.<br />-   Sign: i messaggi sono firmati.<br />-   EncryptAndSign: i messaggi sono crittografati e firmati.<br /><br /> Il valore predefinito è Sign.  L'attributo è di tipo ProtectionLevel.|  
|`msmqSecureHashAlgorithm`|-   Specifica l'algoritmo da usare nel calcolo del digest come parte delle firme.  Di seguito vengono elencati i valori validi:<br />-   MD5<br />-   SHA1<br />-   SHA256<br />-   SHA512<br /><br /> Il valore predefinito è SHA1.  L'attributo è di tipo <xref:System.ServiceModel.MsmqSecureHashAlgorithm>.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)|Definisce le impostazioni di sicurezza per un'associazione MSMQ.|  
  
## Note  
 Questo elemento incapsula le impostazioni di sicurezza per il trasporto di integrazione del servizio di accodamento di messaggi.  Le impostazioni sono le stesse per l'integrazione di accodamento messaggi e trasporti in coda.  Consente di impostare la modalità di autenticazione, l'algoritmo di crittografia, l'algoritmo hash protetto e il livello di protezione.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>   
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.MsmqIntegrationSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.MsmqTransportSecurity>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)