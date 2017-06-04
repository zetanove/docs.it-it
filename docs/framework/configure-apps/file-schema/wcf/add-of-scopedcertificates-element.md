---
title: "Elemento &lt;add&gt; di &lt;scopedCertificates&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e21c1ef8-d6d6-4bca-ac5a-6fbf4bd77412
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Elemento &lt;add&gt; di &lt;scopedCertificates&gt;
Aggiunge un certificato X.509 alla raccolta di certificati con ambito.  
  
## Sintassi  
  
```  
  
<add findValue="String"  
          storeLocation="CurrentUser/LocalMachine"  
          storeName=" CurrentUser/LocalMachine"  
          targetUri="string"  
         x509Type="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"   
/>   
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|targetUri|Stringa.  Specifica l'URI del servizio associato al certificato.|  
|findValue|Stringa.  Valore da cercare.|  
|x509FindType|Enumerazione.  Uno dei campi certificato in cui cercare.|  
|storeLocation|Enumerazione.  Uno di due percorsi dell'archivio in cui cercare.|  
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
|[\<certificatiConAmbito\>](../../../../../docs/framework/configure-apps/file-schema/wcf/scopedcertificates-element.md)|Rappresenta una raccolta di certificati X.509 fornita da servizi specifici \(con ambito\) per l'autenticazione.|  
  
## Note  
 Questo elemento consente al client di configurare un certificato del servizio da usare in base all'URL del servizio con cui comunica.  Questa soluzione è particolarmente utile negli scenari di token pubblicati in cui un client comunica con più servizi \(il servizio finale e i servizi token di sicurezza intermedi\).  Per le associazioni che usano sistemi di sicurezza dei messaggi basati sui certificati, questo certificato viene usato per crittografare i messaggi inviati al servizio ed è previsto che venga usato dal servizio per firmare le risposte al client.  
  
 Se per un'associazione è necessario un certificato per il servizio e non vengono individuati certificati specifici per l'URL del servizio in ScopedCertificates, verrà usato il certificato predefinito.  
  
 Per altre informazioni, vedere la sezione relativa a "Scoped Certificates" di [Procedura: creare un client federato](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md).  
  
## Esempio  
 Nell'esempio seguente un certificato X.509 viene aggiunto alla raccolta.  
  
```  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <serviceCertificate>  
     <scopedCertificates>  
      <add targetUri="http://www.contoso.com"   
       findValue="www.Contoso.com"   
       storeLocation="LocalMachine"  
       storeName="Root"   
       x509FindType="FindByIssuerName" />  
     </scopedCertificates>  
    </serviceCertificate>  
   </clientCredentials>  
  </behavior>  
 </endpointBehaviors>  
</behaviors>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement.ScopedCertificates%2A>   
 <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElementCollection>   
 <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElement>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>   
 [Procedura: creare un client federato](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)