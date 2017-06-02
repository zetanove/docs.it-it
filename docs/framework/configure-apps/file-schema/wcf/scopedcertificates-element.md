---
title: "Elemento &lt;scopedCertificates&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7b6fc35-d4b2-4c18-98bd-83e09591f1d3
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Elemento &lt;scopedCertificates&gt;
Rappresenta una raccolta di certificati X.509 fornita da servizi specifici \(con ambito\) per l'autenticazione.  Questa raccolta è usata in genere per specificare i certificati di servizio per i servizi dei token di sicurezza in un scenario federato.  
  
## Sintassi  
  
```  
  
<scopedCertificates>  
      <add findValue="String"  
                storeLocation="CurrentUser/LocalMachine"  
                storeName=" CurrentUser/LocalMachine"  
                targetUri="string"  
            x509Type="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />   
</scopedCertificates>   
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-scopedcertificates-element.md)|Aggiunge un certificato X.509 alla raccolta di certificati con ambito.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<certificatoServizio\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)|Specifica un certificato da usare per l'autenticazione di un servizio presso il client.|  
  
## Note  
 Questa raccolta consente al client di configurare i certificati del servizio da usare in base all'URL del servizio con cui comunica.  Questa soluzione è particolarmente utile negli scenari di token pubblicati in cui un client comunica con più servizi \(il servizio finale e i servizi token di sicurezza intermedi\).  Per le associazioni che usano sistemi di sicurezza dei messaggi basati sui certificati, questo certificato viene usato per crittografare i messaggi inviati al servizio ed è previsto che venga usato dal servizio per firmare le risposte al client.  
  
 Se per un'associazione è necessario un certificato per il servizio e non vengono individuati certificati specifici per l'URL del servizio in ScopedCertificates, verrà usato il certificato predefinito.  
  
 Per altre informazioni, vedere la sezione relativa a "Scoped Certificates" di [Procedura: creare un client federato](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md).  
  
## Esempio  
 Nell'esempio seguente viene specificato un certificato di servizio che viene usato dal client per comunicare con endpoint il cui nome di dominio è http:\/\/www.contoso.com sul protocollo HTTP.  
  
```  
<serviceCertificate>  
  <scopedCertificates>  
     <add targetUri="http://www.contoso.com"   
          findValue="www.contoso.com" storeLocation="LocalMachine"  
                  storeName="Root" x509FindType="FindByIssuerName" />  
  </scopedCertificates>  
</serviceCertificate>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement.ScopedCertificates%2A>   
 <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElementCollection>   
 <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElement>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>   
 <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>   
 [Utilizzo dei certificati](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Procedura: creare un client federato](../../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [\<aggiunta\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-scopedcertificates-element.md)   
 [Protezione di client](../../../../../docs/framework/wcf/securing-clients.md)   
 [Protezione di servizi e client](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)