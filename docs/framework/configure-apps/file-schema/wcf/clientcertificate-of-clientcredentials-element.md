---
title: "Elemento &lt;clientCertificate&gt; di &lt;clientCredentials&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b3fa000-3434-4142-a178-11903bdd2c5d
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Elemento &lt;clientCertificate&gt; di &lt;clientCredentials&gt;
Definisce un certificato X.509 usato dal client per autenticare un servizio.  
  
## Sintassi  
  
```  
  
<clientCertificate findValue="String"   
    storeLocation="LocalMachine/CurrentUser"  
    storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"  
X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`findValue`|Stringa che contiene il valore da cercare nell'archivio certificati X.509.  Il tipo contenuto in questo attributo deve soddisfare i requisiti del valore `X509FindType` specificato.  Il valore predefinito è una stringa vuota.|  
|`storeLocation`|Specifica il percorso del certificato X.509 usato dal client per autenticarsi presso il servizio.  Di seguito vengono elencati i valori validi:<br /><br /> -   LocalMachine: l'archivio certificati assegnato al computer locale.<br />-   CurrentUser: l'archivio certificati assegnato all'utente corrente.<br /><br /> L'impostazione predefinita è LocalMachine.  L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.StoreLocation>.|  
|`storeName`|Specifica il nome dell'archivio certificati X.509 in cui eseguire la ricerca.  Di seguito vengono elencati i valori validi:<br /><br /> -   AddressBook: archivio certificati per altri utenti.<br />-   AuthRoot: archivio certificati per autorità di certificazione di terze parti.<br />-   CertificateAuthority: archivio certificati autorità di certificazione intermedie.<br />-   Disallowed: archivio certificati per certificati revocati.<br />-   My: archivio certificati per certificati personali.<br />-   Root: archivio certificati per autorità di certificazione radice attendibili.<br />-   TrustedPeople: archivio certificati per utenti e risorse direttamente attendibili.<br />-   TrustedPublisher: archivio certificati per autori direttamente attendibili.<br /><br /> L'impostazione predefinita è My.  L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.StoreName>.|  
|X509FindType|Definisce il tipo di ricerca X.509 da eseguire.  Il tipo contenuto nell'attributo `findValue` deve soddisfare i requisiti di questo attributo.  Di seguito vengono elencati i valori validi:<br /><br /> -   FindByThumbPrint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-   FindByIssuerName<br />-   FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-   FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-   FindByExtension<br />-   FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> L'impostazione predefinita è FindBySubjectDistinguishedName.  L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.X509FindType>.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<credenzialiClient\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|Specifica le credenziali usate per autenticare il client presso un servizio.|  
  
## Note  
 Questo elemento di configurazione specifica il certificato usato per autenticare il client con questo elemento.  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [Procedura: specificare valori di credenziali client](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ClientCertificate%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.ClientCertificate%2A>   
 <xref:System.ServiceModel.Configuration.X509InitiatorCertificateServiceElement>   
 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>   
 [Comportamenti di sicurezza](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [Procedura: specificare valori di credenziali client](../../../../../docs/framework/wcf/how-to-specify-client-credential-values.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)