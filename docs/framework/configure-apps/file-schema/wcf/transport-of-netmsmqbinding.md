---
title: "&lt;transport&gt; di &lt;netMsmqBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 72e1b338-39f0-4af1-a5d9-7a2fb79f6a0b
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# &lt;transport&gt; di &lt;netMsmqBinding&gt;
Definisce le impostazioni di sicurezza del trasporto.  
  
## Sintassi  
  
```  
  
<netMsmqBinding>  
    <binding>  
    <security>  
         <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"  
            msmqEncryptionAlgorithm="RC4Stream/AES"  
            msmqProtectionLevel="None/Sign/EncryptAndSign"  
            msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
    </security>  
   </binding>  
</netMsmqBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|msmqAuthenticationMode|Specifica come deve essere autenticato il messaggio dal trasporto MSMQ.  Di seguito vengono elencati i valori validi:<br /><br /> -   None: nessuna autenticazione<br />-   WindowsDomain: il meccanismo di autenticazione usa Active Directory per recuperare il certificato X.509 per l'ID di sicurezza associato al messaggio.  Questo viene quindi utilizzo per controllare l'ACL della coda in modo da garantire che l'utente disponga dell'autorizzazione per scrivere sulla coda.<br />-   Certificate: il canale recupera il certificato dall'archivio certificati.<br /><br /> Il valore predefinito è `WindowsDomain`.<br /><br /> Se questo attributo viene impostato su `None`, anche l'attributo dell'attributo `msmqProtectionLevel` deve essere impostato su `None`.  L'attributo è di tipo <xref:System.ServiceModel.MsmqAuthenticationMode>.|  
|msmqEncryptionAlgorithm|Specifica l'algoritmo da usare per la crittografia del messaggio in transito durante il trasferimento dei messaggi tra i gestori della coda dei messaggi.  Di seguito vengono elencati i valori validi:<br /><br /> -   RC4Stream<br />-   AES<br />-   Il valore predefinito è `RC4Stream`.  L'attributo è di tipo <xref:System.ServiceModel.MsmqEncryptionAlgorithm>.|  
|msmqProtectionLevel|Specifica il metodo di sicurezza dei messaggi al livello del trasporto MSMQ.  La crittografia assicura l'integrità del messaggio, mentre la firma e la crittografa assicurano l'integrità del messaggio e il non ripudio.  Ciò significa che il messaggio proviene effettivamente dal mittente e il mittente è quello indicato.  Di seguito vengono elencati i valori validi:<br /><br /> -   None: nessuna protezione.<br />-   Sign: i messaggi sono firmati.<br />-   EncryptAndSign: i messaggi sono crittografati e firmati.<br />-   Il valore predefinito è `Sign`.|  
|msmqSecureHashAlgorithm|Specifica l'algoritmo hash da usare per il calcolo del digest del messaggio.  Di seguito vengono elencati i valori validi:<br /><br /> -   MD5<br />-   SHA1<br />-   SHA256<br />-   SHA512<br /><br /> Il valore predefinito è `SHA1`.  L'attributo è di tipo <xref:System.ServiceModel.MsmqSecureHashAlgorithm>.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-netmsmqbinding.md)|Definisce le impostazioni di sicurezza del trasporto per i trasporti in coda.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>   
 <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.NetMsmqSecurity.Transport%2A>   
 <xref:System.ServiceModel.MsmqTransportSecurity>   
 [Code in WCF](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)