---
title: "&lt;certificateReference&gt; per &lt;identity&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac359c65-c22d-42d2-97de-db53b77cebdb
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;certificateReference&gt; per &lt;identity&gt;
Specifica le impostazioni per la convalida del certificato X.509.  Un client [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] protetto che si connette a un endpoint con questa identità verifica che le attestazioni presentate dal server contengano l'attestazione di identità usata per costruire tale identità.  
  
## Sintassi  
  
```  
  
<certificateReference   
        findValue="String"   
    isChainIncluded="Boolean"  
    storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"storeName="  
  
    storeLocation="LocalMachine/CurrentUser"  
  
X509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"  
</certificateReference>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|findValue|Specifica il valore da cercare nell'archivio certificati X.509.  Il tipo contenuto in questo attributo deve soddisfare i requisiti del valore `X509FindType` specificato.  Il valore predefinito è una stringa vuota.|  
|isChainIncluded|Valore booleano che specifica se la convalida viene eseguita usando una catena di certificati.|  
|storeLocation|Specifica il percorso dell'archivio certificati che il client può usare per convalidare il certificato del server.<br /><br /> Di seguito vengono elencati i valori validi:<br /><br /> -   LocalMachine: l'archivio certificati assegnato al computer locale.<br />-   CurrentUser: l'archivio certificati assegnato all'utente corrente.<br /><br /> Il valore predefinito è LocalMachine.<br /><br /> L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.StoreLocation>.|  
|storeName|Specifica il nome dell'archivio certificati X.509 da aprire.<br /><br /> Di seguito vengono elencati i valori validi:<br /><br /> -   AddressBook: archivio certificati per altri utenti.<br />-   AuthRoot: archivio certificati per autorità di certificazione di terze parti.<br />-   CertificateAuthority: archivio certificati per autorità di certificazione intermedie.<br />-   Disallowed: archivio certificati per certificati revocati.<br />-   My: archivio certificati per certificati personali.<br />-   Root: archivio certificati per autorità di certificazione radice attendibili.<br />-   TrustedPeople: archivio certificati per utenti e risorse direttamente attendibili.<br />-   TrustedPublisher: archivio certificati per autori direttamente attendibili.<br /><br /> Il valore predefinito è My.<br /><br /> L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.StoreName>.|  
|X509FindType|Specifica il tipo di ricerca di certificati X.509 da eseguire.  Il tipo contenuto nell'attributo `findValue` deve soddisfare i requisiti del valore X509FindType specificato.<br /><br /> Di seguito vengono elencati i valori validi:<br /><br /> -   FindByThumbPrint<br />-   FindBySubjectName<br />-   FindBySubjectDistinguishedName<br />-   FindByIssuerName<br />-   FindByIssuerDistinguishedName<br />-   FindBySerialNumber<br />-   FindByTimeValid<br />-   FindByTimeNotYetValid<br />-   FindByTemplateName<br />-   FindByApplicationPolicy<br />-   FindByCertificatePolicy<br />-   FindByExtension<br />-   FindByKeyUsage<br />-   FindBySubjectKeyIdentifier<br /><br /> L'impostazione predefinita è FindBySubjectDistinguishedName.<br /><br /> L'attributo è di tipo <xref:System.Security.Cryptography.X509Certificates.X509FindType>.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<identità\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Specifica le impostazioni che attivano l'autenticazione di un endpoint presso gli altri endpoint con cui scambia messaggi.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.CertificateReferenceElement>   
 <xref:System.ServiceModel.Configuration.IdentityElement>   
 <xref:System.ServiceModel.EndpointAddress>   
 <xref:System.ServiceModel.EndpointAddress.Identity%2A>