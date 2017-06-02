---
title: "&lt;certificate&gt; di &lt;peer&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 48b69142-c957-4305-a042-c9d0c9a55c0e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;certificate&gt; di &lt;peer&gt;
Specifica un certificato usato da un peer.  
  
## Sintassi  
  
```  
  
<certificate findValue = "String"   
storeLocation = "CurrentUser/LocalMachine"  
storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`findValue`|Stringa che contiene il valore da cercare nell'archivio certificati X.509.  Il tipo contenuto nell'attributo deve soddisfare i requisiti del valore `x509FindType` specificato.  Il valore predefinito è una stringa vuota.|  
|`storeLocation`|Specifica il percorso dell'archivio certificati X.509 usato dal client per eseguire la convalida del certificato peer.  Di seguito vengono elencati i valori validi:<br /><br /> -   LocalMachine: l'archivio certificati assegnato al computer locale.<br />-   CurrentUser: l'archivio certificati assegnato all'utente corrente.<br /><br /> L'impostazione predefinita è LocalMachine.|  
|`storeName`|Specifica il nome dell'archivio certificati X.509 da aprire.  Di seguito vengono elencati i valori validi:<br /><br /> -   AddressBook: archivio certificati per altri utenti.<br />-   AuthRoot: archivio certificati per autorità di certificazione di terze parti.<br />-   CertificateAuthority: archivio certificati autorità di certificazione intermedie.<br />-   Disallowed: archivio certificati per certificati revocati.<br />-   My: archivio certificati per certificati personali.<br />-   Root: archivio certificati per autorità di certificazione radice attendibili.<br />-   TrustedPeople: archivio certificati per utenti e risorse direttamente attendibili.<br />-   TrustedPublisher: archivio certificati per autori direttamente attendibili.<br /><br /> L'impostazione predefinita è My.|  
|`X509FindType`|Definisce il tipo di ricerca X.509 da eseguire.  Di seguito vengono elencati i valori validi:<br /><br /> -   FindByThumbPrint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-   FindByIssuerName<br />-   FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-   FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-   FindByExtension<br />-   FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> Il tipo contenuto nell'attributo `findValue` deve soddisfare i requisiti del valore `X509FindType` specificato.<br /><br /> L'impostazione predefinita è FindBySubjectDistinguishedName.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-servicecredentials.md)|Specifica le credenziali correnti per un nodo peer.|  
  
## Note  
 Questa elemento di configurazione contiene un'istanza `X509Certificate2` usata per autenticare elementi adiacenti nella rete di peer.  
  
 Per altre informazioni sulla programmazione peer\-to\-peer, vedere [Rete peer\-to\-peer](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.PeerCredentialElement>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.Certificate%2A>   
 <xref:System.ServiceModel.Configuration.X509PeerCertificateElement>   
 <xref:System.ServiceModel.Security.PeerCredential.Certificate%2A>   
 <xref:System.ServiceModel.Security.PeerCredential>   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Rete peer\-to\-peer](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/it-it/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/it-it/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [Protezione di applicazioni del canale peer](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)