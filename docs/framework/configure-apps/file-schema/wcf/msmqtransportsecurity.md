---
title: "&lt;sicurezzaTrasportoMsmq&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 092e911b-ab1b-4069-a26e-6134c3299e06
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# &lt;sicurezzaTrasportoMsmq&gt;
Specifica le impostazioni di sicurezza del trasporto MSMQ di un'associazione personalizzata.  
  
## Sintassi  
  
```  
  
<msmqTransportSecurity>  
   msmqAuthenticationMode="None/Windows/Certificate"  
   msmqEncryptionAlgorithm="RC4Stream/AES"  
   msmqProtectionLevel="None/Sign/EncryptAndSign"  
   msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
</msmqTransportSecurity>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`msmqAuthenticationMode`|Specifica come deve essere autenticato il messaggio dal trasporto MSMQ.  Se viene impostato su `None`, anche il valore dell'attributo `msmqProtectionLevel` deve essere impostato su `None`.<br /><br /> Di seguito vengono elencati i valori validi:<br /><br /> -   None: nessuna autenticazione<br />-   Windows: il meccanismo di autenticazione usa Active Directory per ottenere il certificato X.509 per il SID associato al messaggio.  Questo viene quindi usato per controllare l'ACL della coda in modo da garantire che l'utente disponga dell'autorizzazione per scrivere nella coda.<br />-   Certificate: il canale ottiene il certificato dall'archivio certificati.<br /><br /> L'impostazione predefinita è Windows.  L'attributo è di tipo <xref:System.ServiceModel.MsmqAuthenticationMode>.|  
|`msmqEncryptionAlgorithm`|Specifica l'algoritmo da usare per la crittografia del messaggio in transito durante il trasferimento dei messaggi tra i gestori della coda dei messaggi.  Di seguito vengono elencati i valori validi:<br /><br /> -   RC4Stream<br />-   AES<br /><br /> Il valore predefinito è RC4Stream.  L'attributo è di tipo <xref:System.ServiceModel.MsmqEncryptionAlgorithm>.|  
|`msmqProtectionLevel`|Specifica come viene protetto il messaggio a livello del trasporto MSMQ.  La crittografia assicura l'integrità del messaggio mentre EncryptAndSign assicura sia l'integrità che il non ripudio del messaggio; ovvero, il messaggio proviene effettivamente dal mittente e il mittente è quello che dichiara di essere.  Di seguito vengono elencati i valori validi:<br /><br /> -   None: nessuna protezione.<br />-   Sign: i messaggi sono firmati.<br />-   EncryptAndSign: i messaggi sono crittografati e firmati.<br /><br /> Il valore predefinito è Sign.  L'attributo è di tipo <xref:System.Net.Security.ProtectionLevel>.|  
|`msmqSecureHashAlgorithm`|Specifica l'algoritmo da usare nel calcolo del digest come parte delle firme.  Di seguito vengono elencati i valori validi:<br /><br /> -   MD5<br />-   SHA1<br />-   SHA256<br />-   SHA512<br /><br /> Il valore predefinito è SHA1.  L'attributo è di tipo <xref:System.ServiceModel.MsmqSecureHashAlgorithm>.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<integrazioneMsmq\>](../../../../../docs/framework/configure-apps/file-schema/wcf/msmqintegration.md)|Specifica le impostazioni necessarie per l'interazione con un mittente o un destinatario del sistema di accodamento messaggi \(MSMQ\).|  
|[\<trasportoMsmq\>](../../../../../docs/framework/configure-apps/file-schema/wcf/msmqtransport.md)|Specifica le proprietà di comunicazione dell'accodamento per un servizio Windows Communication Foundation \(WCF\) che usa il protocollo MSMQ nativo.|  
  
## Note  
 Per altre informazioni sulla sicurezza di trasporto, vedere [Protezione del trasporto](../../../../../docs/framework/wcf/feature-details/transport-security.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity>   
 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Code in WCF](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [Trasporti](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [Scelta di un trasporto](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Protezione del trasporto](../../../../../docs/framework/wcf/feature-details/transport-security.md)