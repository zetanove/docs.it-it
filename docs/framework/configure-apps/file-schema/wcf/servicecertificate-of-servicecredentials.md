---
title: "&lt;serviceCertificate&gt; di &lt;serviceCredentials&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 597ae6d5-4938-4950-9f5e-b2280e816182
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;serviceCertificate&gt; di &lt;serviceCredentials&gt;
Specifica un certificato X.509 che verrà usato dai client per autenticare il servizio tramite la modalità di sicurezza dei messaggi.  
  
## Sintassi  
  
```  
  
<serviceCertificate findValue="String"   
    storeLocation="LocalMachine/CurrentUser"  
    storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
X509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`findValue`|Stringa che contiene il valore da cercare nell'archivio certificati X.509.  Il tipo contenuto in questo attributo deve soddisfare i requisiti del valore X509FindType specificato.  Il valore predefinito è una stringa vuota.|  
|`storeLocation`|Specifica il percorso dell'archivio certificati X.509 usato dal client per convalidare il certificato sul server.  Di seguito vengono elencati i valori validi:<br /><br /> -   LocalMachine: l'archivio certificati assegnato al computer locale.<br />-   CurrentUser: l'archivio certificati assegnato all'utente corrente.<br /><br /> L'impostazione predefinita è LocalMachine.|  
|`storeName`|Specifica il nome dell'archivio certificati X.509 da aprire.  Di seguito vengono elencati i valori validi:<br /><br /> -   AddressBook: archivio certificati per altri utenti.<br />-   AuthRoot: archivio certificati per autorità di certificazione di terze parti.<br />-   CertificateAuthority: archivio certificati per autorità di certificazione intermedie.<br />-   Disallowed: archivio certificati per certificati revocati.<br />-   My: archivio certificati per certificati personali.<br />-   Root: archivio certificati per autorità di certificazione radice attendibili.<br />-   TrustedPeople: archivio certificati per utenti e risorse direttamente attendibili.<br />-   TrustedPublisher: archivio certificati per autori direttamente attendibili.<br /><br /> L'impostazione predefinita è My.|  
|`X509FindType`|Definisce il tipo di ricerca X.509 da eseguire.  Di seguito vengono elencati i valori validi:<br /><br /> -   FindByThumbPrint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-   FindByIssuerName<br />-   FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-   FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-   FindByExtension<br />-   FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> Il tipo contenuto nell'attributo `findValue` deve soddisfare i requisiti del valore X509FindType specificato.<br /><br /> L'impostazione predefinita è FindBySubjectDistinguishedName.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|Specifica la credenziale da usare nell'autenticazione del servizio e le impostazioni relative alla convalida delle credenziali client.|  
  
## Note  
 Questo elemento consente di specificare il certificato X.509 usato dai client per autenticare il servizio tramite la modalità di sicurezza Messaggio.  L'identificazione personale di un certificato che viene rinnovato periodicamente viene anch'essa aggiornata periodicamente di conseguenza.  In questo caso, poiché il certificato può essere rilasciato nuovamente con lo stesso nome del soggetto, usare quest'ultimo come tipo `X509FindType`.  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] utilizzo dell'elemento, vedere [Procedura: specificare valori di credenziali client](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.X509RecipientCertificateServiceElement>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.ServiceCertificate%2A>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>   
 <xref:System.ServiceModel.Description.ServiceCredentials.ServiceCertificate%2A>   
 [Procedura: specificare valori di credenziali client](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)