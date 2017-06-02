---
title: "Elemento &lt;messageSenderAuthentication&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d979dfc-a6f9-42ec-96d5-7fbc13a48118
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Elemento &lt;messageSenderAuthentication&gt;
Specifica opzioni di autenticazione per i mittenti di messaggi peer\-to\-peer.  
  
 Per altre informazioni sulla programmazione peer\-to\-peer, vedere [Rete peer\-to\-peer](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
## Sintassi  
  
```  
  
<messageSenderAuthentication  
customCertificateValidatorType= "namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode = "ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
revocationMode="NoCheck/Online/Offline"  
trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|customCertificateValidatorType|Un tipo e un assembly usati per convalidare un tipo personalizzato.  Questo attributo deve essere impostato quando `certificateValidationMode` è impostato su `Custom`.|  
|certificateValidationMode|Specifica una delle tre modalità usate per convalidare credenziali.  Se impostato su `Custom`, è necessario fornire anche un `customCertificateValidator`.|  
|revocationMode|Una delle modalità usate per verificare un elenco dei certificati revocati.|  
|trustedStoreLocation|Uno di due percorsi dell'archivio di sistema: `LocalMachine` o `CurrentUser`.  Questo valore viene usato quando viene negoziato un certificato del servizio con il client.  La convalida viene eseguita in base all'archivio **Persone attendibili** nel percorso dell'archivio specificato.|  
  
## Attributo customCertificateValidatorType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|String|Parametro facoltativo.  Specifica il nome e l'assembly del tipo e altri dati usati per trovare il tipo.  Come minimo, sono necessari uno spazio dei nomi e un nome del tipo.  Le informazioni facoltative comprendono il nome dell'assembly, il numero di versione, impostazioni cultura e token della chiave pubblica.|  
  
## Attributo certificateValidationMode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|Parametro facoltativo.  Uno dei valori seguenti: `None`, `PeerTrust`, `ChainTrust`, `PeerOrChainTrust`, `Custom`.  Il valore predefinito è `ChainTrust`.  Il valore predefinito è `ChainTrust`.<br /><br /> Per altre informazioni, vedere [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## Attributo revocationMode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|Uno dei valori seguenti: `NoCheck`, `Online`, `Offline`.  Il valore predefinito è `Online`.<br /><br /> Per altre informazioni, vedere [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## Attributo trustedStoreLocation  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|Uno dei valori seguenti: `LocalMachine` o `CurrentUser`.  Il valore predefinito è `CurrentUser`.  Se l'applicazione client viene eseguita con un account di sistema, il certificato è generalmente situato in `LocalMachine`.  Se l'applicazione client viene eseguita con un account utente, il certificato è generalmente situato in `CurrentUser`.  Il valore predefinito è `CurrentUser`.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-clientcredentials-element.md)|Specifica una credenziale usata per l'autenticazione del client con un servizio peer.|  
  
## Note  
 Se è stata scelta l'autenticazione dei messaggi, sarà necessario configurare questo elemento.  Per i canali di output, ogni messaggio viene firmato usando il certificato fornito da [\<certificato\>](../../../../../docs/framework/configure-apps/file-schema/wcf/certificate-element.md).  Prima che vengano recapitati all'applicazione, tutti i messaggi vengono controllati a fronte delle credenziali del messaggio usando la convalida specificata dall'attributo `customCertificateValidatorType` di questo elemento.  La convalida può accettare o rifiutare la credenziale.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene impostata la modalità di convalida del mittente del messaggio su `PeerOrChainTrust`.  
  
```  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <peer>  
      <certificate findValue="www.contoso.com"   
                   storeLocation="LocalMachine"  
                   x509FindType="FindByIssuerName" />  
        <messageSenderAuthentication   
          certificateValidationMode="PeerOrChainTrust" />  
       <messageSenderAuthentication certificateValidationMode="None" />  
    </peer>  
   </clientCredentials>  
  </behavior>  
 </endpointBehaviors>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>   
 <xref:System.ServiceModel.Security.PeerCredential.MessageSenderAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.MessageSenderAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Rete peer\-to\-peer](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/it-it/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/it-it/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [Protezione di applicazioni del canale peer](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)