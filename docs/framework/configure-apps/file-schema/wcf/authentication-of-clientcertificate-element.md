---
title: "Elemento &lt;authentication&gt; di &lt;clientCertificate&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4a55eea2-1826-4026-b911-b7cc9e9c8bfe
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Elemento &lt;authentication&gt; di &lt;clientCertificate&gt;
Specifica i comportamenti di autenticazione per i certificati client utilizzati da un servizio.  
  
## Sintassi  
  
```  
  
<authentication  
customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
includeWindowsGroups="Boolean"  
mapClientCertificateToWindowsAccount="Boolean"  
revocationMode="NoCheck/Online/Offline"  
trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|customCertificateValidatorType|Stringa facoltativa.  Un tipo e un assembly usati per convalidare un tipo personalizzato.  Questo attributo deve essere impostato quando `certificateValidationMode` è impostato su `Custom`.|  
|certificateValidationMode|Enumerazione facoltativa.  Specifica una delle modalità usate per convalidare credenziali.  L'attributo è di tipo [System.Servicemodel.Security.X509CertificateValidationMode](assetId:///System.Servicemodel.Security.X509CertificateValidationMode?qualifyHint=False&amp;autoUpgrade=True).  Se impostato su `Custom`, è necessario fornire anche un `customCertificateValidator`.  Il valore predefinito è `ChainTrust`.|  
|includeWindowsGroups|Valore booleano facoltativo.  Specifica se i gruppi di Windows sono inclusi nel contesto di sicurezza.  L'impostazione di questo attributo su `true` determina un effetto sulle prestazioni in quanto comporta un'espansione completa del gruppo.  Impostare questo attributo su `false` se non è necessario stabilire l'elenco di gruppi a cui appartiene un utente.|  
|mapClientCertificateToWindowsAcccount|Proprietà di tipo Boolean.  Specifica se è possibile eseguire il mapping del client a un'identità di Windows usando il certificato.  A tal scopo è necessario che Active Directory sia attivato.|  
|revocationMode|Enumerazione facoltativa.  Una delle modalità usate per verificare un elenco dei certificati revocati.  Il valore predefinito è `Online`.  Questo valore viene ignorato quando si usa la sicurezza del trasporto HTTP.|  
|trustedStoreLocation|Enumerazione facoltativa.  Uno di due percorsi dell'archivio di sistema: `LocalMachine` o `CurrentUser`.  Questo valore viene usato quando viene negoziato un certificato del servizio con il client.  La convalida viene eseguita in base all'archivio **Persone attendibili** nel percorso dell'archivio specificato.  Il valore predefinito è `CurrentUser`.|  
  
## Attributo customCertificateValidatorType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|String|Specifica il nome e l'assembly del tipo e altri dati usati per trovare il tipo.|  
  
## Attributo certificateValidationMode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|Uno dei valori seguenti: None, PeerTrust, ChainTrust, PeerOrChainTrust, Custom.<br /><br /> Per altre informazioni, vedere [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## Attributo revocationMode  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|Uno dei valori seguenti: NoCheck, Online, Offline.  Per altre informazioni, vedere [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md).|  
  
## Attributo trustedStoreLocation  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|Uno dei valori seguenti: `LocalMachine` o `CurrentUser`.  Il valore predefinito è `CurrentUser`.  Se l'applicazione client viene eseguita con un account di sistema, il certificato è generalmente situato in `LocalMachine`.  Se l'applicazione client viene eseguita con un account utente, il certificato è generalmente situato in `CurrentUser`.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<certificatoClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcertificate-of-servicecredentials.md)|Definisce un certificato X.509 utilizzato dal client per autenticare un servizio.|  
  
## Note  
 L'elemento `<authentication>` corrisponde alla classe <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>.  Consente di personalizzare la modalità di autenticazione dei client.  A tale scopo, l'attributo `certificateValidationMode` può essere impostato su `None`, `ChainTrust`, `PeerOrChainTrust`, `PeerTrust` o `Custom`.  Per impostazione predefinita, il livello è impostato su `ChainTrust`. Tale impostazione prevede che ogni certificato appartenga a una gerarchia di certificati che termina in un'*autorità radice* situata all'inizio della catena.  Si tratta della modalità più sicura.  Il livello può inoltre essere impostato su `PeerOrChainTrust`, a indicare che sia i certificati autocertificati \(trust peer\) sia i certificati appartenenti a una catena di trust sono ritenuti attendibili.  Poiché i certificati autocertificati non devono essere acquistati da un'autorità attendibile, questo livello viene usato in fase di sviluppo e di debug dei client e dei servizi.  Quando si distribuisce un client è invece opportuno usare il livello `ChainTrust`.  
  
 Un altro livello disponibile è `Custom`.  Quando si imposta il livello `Custom` è necessario impostare anche l'attributo `customCertificateValidatorType` sull'assembly e sul tipo usati per convalidare il certificato.  Per creare un validator personalizzato è necessario ereditare una classe dalla classe astratta <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  Per altre informazioni, vedere [Procedura: creare un servizio che usa un validator del certificato personalizzato](../../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
## Esempio  
 Nel codice seguente sono specificati un certificato X.509 e un tipo di convalida personalizzato nell'elemento `<authentication>`.  
  
```  
<serviceBehaviors>  
 <behavior name="myServiceBehavior">  
  <clientCertificate>  
   <certificate   
         findValue="www.cohowinery.com"   
         storeLocation="CurrentUser"   
         storeName="TrustedPeople"  
         x509FindType="FindByIssuerName" />  
   <authentication customCertificateValidatorType="MyTypes.Coho"  
    certificateValidationMode="Custom"   
    revocationMode="Offline"  
    includeWindowsGroups="false"   
    mapClientCertificateToWindowsAccount="true" />  
  </clientCertificate>  
 </behavior>  
</serviceBehaviors>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>   
 <xref:System.ServiceModel.Security.X509CertificateValidationMode>   
 <xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.Authentication%2A>   
 <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement.Authentication%2A>   
 <xref:System.ServiceModel.Configuration.X509ClientCertificateAuthenticationElement>   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Procedura: creare un servizio che usa un validator del certificato personalizzato](../../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)