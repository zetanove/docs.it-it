---
title: "Elemento &lt;defaultCertificate&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f1ddf364-9a00-45d3-b989-ff381c154ce6
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Elemento &lt;defaultCertificate&gt;
Specifica un certificato X.509 da usare quando un servizio o STS non ne fornisce uno tramite un protocollo di negoziazione.  
  
## Sintassi  
  
```  
  
<defaultCertificate findValue="String"   
storeLocation=" CurrentUser/LocalMachine"  
storeName="AddressBook/AuthRoot/CertificateAuthority/Disallowed/My/Root/TrustedPeople/TrustedPublisher"   
x509FindType="FindByThumbPrint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialiNumber/FindByTimeValid/FindByTimeNotYetValid/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|findValue|Stringa.  Valore da cercare.|  
|x509FindType|Enumerazione.  Uno dei campi certificato in cui cercare.|  
|storeLocation|Enumerazione.  Uno di due percorsi dell'archivio di sistema in cui cercare.|  
|storeName|Enumerazione.  Uno degli archivi di sistema in cui cercare.|  
  
## Attributo findValue  
  
|Valore|Descrizione|  
|------------|-----------------|  
|String|Il valore dipende dal campo di ricerca specificato dall'attributo X509FindType.  Ad esempio, se viene eseguita la ricerca di un'identificazione digitale, il valore deve essere una stringa di numeri esadecimali.|  
  
## Attributo x509FindType  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|I valori includono: FindByThumbprint, FindBySubjectName, FindBySubjectDistinguishedName, FindByIssuerName, FindByIssuerDistinguishedName, FindBySerialNumber, FindByTimeValid, FindByTimeNotYetValid, FindBySerialNumber, FindByTimeExpired, FindByTemplateName, FindByApplicationPolicy, FindByCertificatePolicy, FindByExtension, FindByKeyUsage, FindBySubjectKeyIdentifier.|  
  
## Attributo storeLocation  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|CurrentUser o LocalMachine.|  
  
## Attributo storeName  
  
|Valore|Descrizione|  
|------------|-----------------|  
|Enumerazione|I valori includono: AddressBook, AuthRoot, CertificateAuthority, Disallowed, My, Root, TrustedPeople e TrustedPublisher.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<certificatoServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)|Specifica un certificato da usare per l'autenticazione di un servizio presso il client.|  
  
## Note  
 Per le associazioni che usano sistemi di sicurezza dei messaggi basati sui certificati, il certificato specificato mediante questo elemento di configurazione viene usato per crittografare i messaggi inviati al servizio ed è previsto che venga usato dal servizio per firmare le risposte al client.  Può contenere un solo certificato da usare quando il servizio non specifica alcun certificato.  
  
## Esempio  
 Nell'esempio seguente viene specificato un certificato da usare per endpoint il cui URI inizia con http:\/\/www.contoso.com e un certificato da usare per tutti gli altri endpoint che non eseguono negoziazione del certificato.  
  
```  
<serviceCertificate>  
  <defaultCertificate findValue="www.contoso.com"   
                      storeLocation="LocalMachine"  
                      storeName="TrustedPeople"   
                      x509FindType="FindByIssuerDistinguishedName" />  
  <scopedCertificates>  
     <add targetUri="http://www.contoso.com"   
          findValue="www.contoso.com" storeLocation="LocalMachine"  
                  storeName="Root" x509FindType="FindByIssuerName" />  
  </scopedCertificates>  
  <authentication revocationMode="Online"   
   trustedStoreLocation="LocalMachine" />  
</serviceCertificate>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.X509DefaultServiceCertificateElement>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.DefaultCertificate%2A>   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [\<authentication\>](../../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)