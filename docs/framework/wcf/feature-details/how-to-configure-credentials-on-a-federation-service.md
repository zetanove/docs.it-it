---
title: "Procedura: configurare le credenziali in un servizio federativo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "federazione"
  - "WCF, federazione"
ms.assetid: 149ab165-0ef3-490a-83a9-4322a07bd98a
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Procedura: configurare le credenziali in un servizio federativo
In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], la creazione di un servizio federativo è costituito dalle procedure principali seguenti:  
  
1.  Configurazione di un oggetto <xref:System.ServiceModel.WSFederationHttpBinding> o di un'associazione personalizzata simile.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] creazione di un'associazione appropriata, vedere [Procedura: creare una classe WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md).  
  
2.  Configurazione della classe <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>, che controlla come vengono autenticati i token emessi presentati al servizio.  
  
 In questo argomento vengono fornite informazioni dettagliate sul secondo passaggio.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] funzionamento di un servizio federativo, vedere [Federazione](../../../../docs/framework/wcf/feature-details/federation.md).  
  
### Per impostare le proprietà di IssuedTokenServiceCredential nel codice  
  
1.  Utilizzare la proprietà <xref:System.ServiceModel.Description.ServiceCredentials.IssuedTokenAuthentication%2A> della classe <xref:System.ServiceModel.Description.ServiceCredentials> per restituire un riferimento a un'istanza di <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>.L'accesso alla proprietà viene eseguito dalla proprietà <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> della classe <xref:System.ServiceModel.ServiceHostBase>.  
  
2.  Se devono essere autenticati token autocertificati, ad esempio schede [!INCLUDE[infocard](../../../../includes/infocard-md.md)], impostare la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowUntrustedRsaIssuers%2A> su `true`.Il valore predefinito è `false`.  
  
3.  Popolare la raccolta restituita dalla proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A> con istanze della classe <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>.Ogni istanza rappresenta un emittente da cui il servizio autenticherà i token.  
  
    > [!NOTE]
    >  A differenza della raccolta lato client restituita dalla proprietà <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>, la raccolta dei certificati noti non è una raccolta con chiave.Il servizio accetta i token emessi dai certificati specificati indipendentemente dall'indirizzo del client che ha inviato il messaggio contenente il token emesso \(salvo gli ulteriori limiti descritti più avanti in questo argomento\).  
  
4.  Impostare la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> su uno dei valori dell'enumerazione <xref:System.ServiceModel.Security.X509CertificateValidationMode>.Questa operazione può essere eseguita solo nel codice.L'impostazione predefinita è <xref:System.IdentityModel.Selectors.X509CertificateValidator.ChainTrust%2A>.  
  
5.  Se la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> viene impostata su <xref:System.ServiceModel.Security.X509CertificateValidationMode>, assegnare un'istanza della classe <xref:System.IdentityModel.Selectors.X509CertificateValidator> personalizzata alla proprietà <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CustomCertificateValidator%2A>.  
  
6.  Se la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> viene impostata su `ChainTrust` o su `PeerOrChainTrust`, impostare la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.RevocationMode%2A> su un valore appropriato ottenuto dall'enumerazione <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>.Si noti che la modalità di revoca non viene utilizzata nelle modalità di convalida `PeerTrust` e `Custom`.  
  
7.  Se necessario, assegnare un'istanza di una classe <xref:System.IdentityModel.Tokens.SamlSerializer> personalizzata alla proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.SamlSerializer%2A>.Per l'analisi delle asserzioni SAML personalizzate, ad esempio, è necessario un serializzatore SAML \(Security Assertions Markup Language\).  
  
### Per impostare le proprietà di IssuedTokenServiceCredential nella configurazione  
  
1.  Creare un elemento `<issuedTokenAuthentication>`\< `come figlio di un elemento serviceCredentials`\>.  
  
2.  Impostare l'attributo `allowUntrustedRsaIssuers` dell'elemento `<issuedTokenAuthentication>` su `true` in caso di autenticazione di un token autocertificato, ad esempio una scheda [!INCLUDE[infocard](../../../../includes/infocard-md.md)].  
  
3.  Creare un elemento `<knownCertificates>``<issuedTokenAuthentication> come figlio dell'elemento` .  
  
4.  Creare zero o più elementi `<add>``<knownCertificates> come figli dell'elemento` `storeLocation` `e specificare come individuare il certificato utilizzando gli attributi storeName``, x509FindType``, findValue` e .  
  
5.  Se necessario, impostare l'attributo `samlSerializer` dell'elemento \<`issuedTokenAuthentication`\> sul nome del tipo della classe <xref:System.IdentityModel.Tokens.SamlSerializer> personalizzata.  
  
## Esempio  
 Nell'esempio seguente vengono impostate le proprietà di <xref:System.ServiceModel.Security.IssuedTokenServiceCredential> nel codice.  
  
 [!code-csharp[C_FederatedService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_federatedservice/cs/source.cs#2)]
 [!code-vb[C_FederatedService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_federatedservice/vb/source.vb#2)]  
  
 Affinché un servizio federativo autentichi un client, per il token emesso devono essere osservate le condizioni seguenti:  
  
-   Quando la firma digitale del token emesso utilizza un identificatore della chiave di sicurezza RSA, la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.AllowUntrustedRsaIssuers%2A> deve essere `true`.  
  
-   Quando la firma del token emesso utilizza un numero di serie dell'emittente X.509, un identificatore della chiave del soggetto X.509 o un identificatore di sicurezza dell'identificazione personale X.509, il token emesso deve essere firmato da un certificato nella raccolta restituita dalla proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A> della classe <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>.  
  
-   Quando il token emesso viene firmato utilizzando un certificato X.509, il certificato deve eseguire la convalida secondo la semantica specificata dal valore della proprietà <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A>, indipendentemente dal fatto che il certificato sia stato inviato al componente come <xref:System.IdentityModel.Tokens.X509RawDataKeyIdentifierClause> oppure ottenuto dalla proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.KnownCertificates%2A>.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sulla convalida dei certificati X.509, vedere [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
 Ad esempio, impostando la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A> su <xref:System.ServiceModel.Security.X509CertificateValidationMode>, verrebbe autenticato un token emesso il cui certificato di firma si trova nell'archivio certificati `TrustedPeople`.In tal caso, impostare la proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.TrustedStoreLocation%2A> su <xref:System.Security.Cryptography.X509Certificates.StoreLocation> o su <xref:System.Security.Cryptography.X509Certificates.StoreLocation>.È possibile selezionare altre modalità, tra cui <xref:System.ServiceModel.Security.X509CertificateValidationMode>.Quando si seleziona `Custom`, è necessario assegnare un'istanza della classe <xref:System.IdentityModel.Selectors.X509CertificateValidator> alla proprietà <xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CustomCertificateValidator%2A>.Con il validator personalizzato è possibile convalidare i certificati mediante qualsiasi criterio.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: creare un servizio che usa un validator del certificato personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md).  
  
## Vedere anche  
 [Federazione](../../../../docs/framework/wcf/feature-details/federation.md)   
 [Federazione e attendibilità](../../../../docs/framework/wcf/feature-details/federation-and-trust.md)   
 [Esempio di federazione](../../../../docs/framework/wcf/samples/federation-sample.md)   
 [Procedura: disattivare sessioni protette in un'associazione WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)   
 [Procedura: creare una classe WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)   
 [Procedura: creare un client federato](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)   
 [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Modalità di autenticazione di SecurityBindingElement](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)