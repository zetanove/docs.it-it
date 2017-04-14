---
title: "&lt;autenticazionePeer&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad545e6f-f06e-4549-ac92-09d758d5c636
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;autenticazionePeer&gt;
Specifica le impostazioni di autenticazione di un certificato peer usato da un nodo peer.  
  
## Sintassi  
  
```  
  
<peerAuthentication  
      customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
      certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
      revocationMode="NoCheck/Online/Offline"  
      trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`certificateValidationMode`|Enumerazione facoltativa.  Specifica una delle tre modalità usate per convalidare credenziali.  L'attributo è di tipo <xref:System.ServiceModel.Security.X509CertificateValidationMode>.  Se impostato su `Custom`, è necessario fornire anche un `customCertificateValidator`.|  
|`customCertificateValidatorType`|Stringa facoltativa.  Specifica un tipo e un assembly usati per convalidare un tipo personalizzato.  Questo attributo deve essere impostato quando `certificateValidationMode` è impostato su `Custom`.  L'attributo è di tipo <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] fornisce un validator del certificato peer predefinita che verifica il certificato peer a fronte dell'archivio Persone attendibili.  Verifica inoltre che il certificato sia concatenato a una radice valida.  È possibile implementare una convalida personalizzata per specificare un comportamento diverso e usare questo attributo per puntare alla convalida personalizzata.|  
|`revocationMode`|Enumerazione facoltativa.  Specifica la modalità di revoca dei certificati.  L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>.  Il sistema verifica che il certificato peer non sia stato revocato cercandolo nell'elenco dei certificati revocati.  Questo controllo può essere eseguito controllando in linea o in un elenco di revoche memorizzato nella cache.  È possibile disattivare il controllo di revoca impostando l'attributo su NoCheck.|  
|`trustedStoreLocation`|Enumerazione facoltativa.  Specifica il percorso dell'archivio dati attendibile in cui il certificato peer viene convalidato dal sistema di sicurezza [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].  L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.StoreLocation>.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-servicecredentials.md)|Specifica le credenziali correnti per un nodo peer.|  
  
## Note  
 L'elemento `<authentication>` corrisponde alla classe <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>.  Questo elemento specifica una convalida, che viene richiamata durante l'autenticazione tra peer adiacenti nella rete.  Quando un nuovo peer tenta di stabilire una connessione con un peer adiacente, passa la propria credenziale al peer che risponde.  Viene richiamata la convalida del risponditore per verificare la credenziale della parte remota.  Ogni volta che viene stabilita una connessione peer nella rete, entrambi i peer vengono reciprocamente autenticati, indicando che vengono richiamati validator su entrambe le parti.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.PeerCredentialElement>   
 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>   
 <xref:System.ServiceModel.Security.PeerCredential.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Rete peer\-to\-peer](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/it-it/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/it-it/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [Protezione di applicazioni del canale peer](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)