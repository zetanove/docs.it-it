---
title: "&lt;message&gt; di &lt;wsDualHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 75101744-eed8-4d61-91f4-5fc4473a21f2
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# &lt;message&gt; di &lt;wsDualHttpBinding&gt;
Definisce la sicurezza a livello di messaggio per l'[\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md).  
  
## Sintassi  
  
```  
  
<message   
      clientCredentialType="None/Windows/UserName/Certificate/CardSpace"  
     negotiateServiceCredential="Boolean"  
   algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"/>  
</message>  
```  
  
## Tipo  
 <xref:System.ServiceModel.MessageSecurityOverHttp>  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|algorithmSuite|Parametro facoltativo.  Imposta la crittografia dei messaggi e gli algoritmi di incapsulamento della chiave.  Gli algoritmi e le dimensioni della chiave sono determinati dalla classe <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.  Questi algoritmi sono associati a quelli specificati nelle specifiche del linguaggio dei criteri di sicurezza \(WS\-SecurityPolicy\).<br /><br /> Di seguito sono riportati i valori possibili.  Il valore predefinito è `Basic256`.|  
|clientCredentialType|Parametro facoltativo.  Specifica il tipo di credenziale da usare se l'autenticazione client viene eseguita usando la modalità di sicurezza `Message`.  Di seguito sono riportati i valori possibili.  Il valore predefinito è `Windows`.<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.MessageCredentialType>.|  
|negotiateServiceCredential|Parametro facoltativo.  Valore booleano che specifica se viene eseguito il provisioning della credenziale del servizio al client fuori banda o se viene ottenuta dal servizio al client tramite un processo di negoziazione.  Tale negoziazione precede lo scambio di messaggi abituale.<br /><br /> Se l'attributo `clientCredentialType` è None, UserName o Certificate, l'impostazione di questo attributo su `false` implica che il certificato del servizio sia disponibile per il client fuori banda e che il client deve specificare il certificato del servizio \(mediante [\<certificatoServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)\) nel comportamento del servizio [\<credenzialiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md).  Questa modalità è interoperabile con gli stack SOAP che implementano WS\-Trust e WS\-SecureConversation.<br /><br /> Se l'attributo `ClientCredentialType` è impostato su `Windows`, l'impostazione di questo attributo su `false` specifica l'autenticazione basata su Kerberos.  Questo significa che il client e il servizio devono fare parte dello stesso dominio Kerberos.  Questa modalità è interoperabile con gli stack SOAP che implementano il profilo del token Kerberos \(come definito in OASIS WSS TC\) e anche WS\-Trust e WS\-SecureConversation.  Quando questo attributo è `true`, si verifica una negoziazione SOAP .NET che esegue il tunneling dello scambio SPNego su messaggi SOAP.<br /><br /> Il valore predefinito è `true`.|  
  
## Attributo algorithmSuite  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Basic128|Usa crittografia Aes128, Sha1 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|Basic192|Usa crittografia Aes192, Sha1 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|Basic256|Usa crittografia Aes256, Sha1 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|Basic256Rsa15|Usa Aes256 per la crittografia del messaggio, Sha1 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
|Basic192Rsa15|Usa Aes192 per la crittografia del messaggio, Sha1 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
|TripleDes|Usa crittografia TripleDes, Sha1 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|Basic128Rsa15|Usa crittografia Aes128, Sha1 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
|TripleDesRsa15|Usa crittografia TripleDes, Sha1 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
|Basic128Sha256|Usa crittografia Aes256, Sha256 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|Basic192Sha256|Usa Aes192 per la crittografia del messaggio, Sha256 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|Basic256Sha256|Usa crittografia Aes256, Sha256 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|TripleDesSha256|Usa TripleDes per la crittografia del messaggio, Sha256 per il digest del messaggio e Rsa\-oaep\-mgf1p per l'incapsulamento della chiave.|  
|Basic128Sha256Rsa15|Usa Aes128 per la crittografia del messaggio, Sha256 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
|Basic192Sha256Rsa15|Usa Aes192 per la crittografia del messaggio, Sha256 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
|Basic256Sha256Rsa15|Usa Aes256 per la crittografia del messaggio, Sha256 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
|TripleDesSha256Rsa15|Usa TripleDes per la crittografia del messaggio, Sha256 per il digest del messaggio e Rsa15 per l'incapsulamento della chiave.|  
  
## Attributo clientCredentialType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|None|None: consente al servizio di interagire con i client anonimi.  Sul lato del servizio, indica che il servizio non richiede alcuna credenziale client.  Sul client, indica che il client non fornisce alcuna credenziale client.|  
|Windows|consente lo svolgimento degli scambi SOAP nel contesto autenticato di una credenziale di Windows.  Se l'attributo `negotiateServiceCredential` è impostato su `true`, esegue una negoziazione SSPI o Kerberos \(un standard interoperabile\).|  
|UserName|Consente al servizio di richiedere che l'autenticazione del client sia eseguita tramite una credenziale UserName.  [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] non supporta l'invio di un digest delle password, né la derivazione delle chiavi basata su password, né l'uso di tali chiavi per implementare la sicurezza dei messaggi.  Di conseguenza, quando si usano le credenziali UserName, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] richiede che il trasporto sia protetto.  Questa modalità di credenziale produce un scambio interoperabile o una negoziazione non interoperabile basata sull'attributo `negotiateServiceCredential`.|  
|Certificato|Consente al servizio di richiedere che l'autenticazione del client si basi su un certificato.  Se viene usata la modalità di sicurezza del messaggio e l'attributo `negotiateServiceCredential` è impostato su `false`, è necessario eseguire il provisioning del client tramite il certificato del servizio.|  
|IssuedToken|Specifica un token personalizzato, generalmente rilasciato da un servizio di token di sicurezza.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezza\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsdualhttpbinding.md)|Definisce le funzionalità di sicurezza di [\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md).|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.WSDualHttpSecurityElement.Message%2A>   
 <xref:System.ServiceModel.WSDualHttpSecurity.Message%2A>   
 <xref:System.ServiceModel.Configuration.MessageSecurityOverTcpElement>   
 <xref:System.ServiceModel.MessageSecurityOverHttp>   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/it-it/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<associazione\>](../../../../../docs/framework/misc/binding.md)