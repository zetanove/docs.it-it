---
title: "&lt;certificateValidation&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c54c704-b55e-4631-88ff-4d4a5621554c
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# &lt;certificateValidation&gt;
Controlla le impostazioni che i gestori di token viene utilizzato per convalidare i certificati.  Queste impostazioni vengono ignorate se un gestore specifico è configurato con il proprio validator.  
  
## Sintassi  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <certificateValidation  
      certificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
      revocationMode="NoCheck||Offline||Online"  
      trustedStoreLocation="CurrentLocation||LocalMachine" >  
    </certificateValidation>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|certificateValidationMode|Un valore di <xref:System.ServiceModel.Security.X509CertificateValidationMode> che specifica la modalità di convalida da utilizzare per il certificato X.509.  il valore predefinito è “PeerOrChainTrust„.  Per specificare un validator personalizzato, impostare questo attributo custom e specificare il validator  utilizzando l'elemento.  Parametro facoltativo.|  
|revocationMode|Un valore di <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> che specifica la modalità di revoca da utilizzare per il certificato X.509.  il valore predefinito è “online„.  Parametro facoltativo.|  
|trustedStoreLocation|Un valore di <xref:System.Security.Cryptography.X509Certificates.StoreLocation> che specifica archivio certificati X.509.  il valore predefinito è “LocalMachine„.  Parametro facoltativo.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<certificateValidator\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/certificatevalidator.md)|Specifica un tipo personalizzato per la convalida del certificato.  Questo tipo viene utilizzato solo se l'attributo di `certificateValidationMode`  dell' elemento è custom impostata.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)|Specifica le impostazioni dell' identità del livello di servizio.|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|Fornisce la configurazione per una raccolta di gestori del token di sicurezza.|  
  
## Note  
 Un elemento di `<certificateValidation>` può essere specificato a livello del servizio nell' elemento di `<identityConfiguration>` o a livello di raccolta per la gestione del token di sicurezza nell' elemento di `<securityTokenHandlerConfiguration>` .  Impostazioni di override di raccolta di gestori di quelli specificati dal servizio.  Alcuni gestori di consentono di specificare le impostazioni di convalida del certificato nella configurazione.  Le impostazioni sui singoli gestori di eseguono l'override di quelle specificato sia a livello di servizio che la raccolta di gestori del token di sicurezza.  
  
## Esempio  
  
```  
<certificateValidation certificateValidationMode="PeerOrChainTrust"  
                       revocationMode="Online"  
                       trustedStoreLocation="LocalMachine" />  
```