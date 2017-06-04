---
title: "Federazione e token emessi | Microsoft Docs"
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
  - "federazione [WCF], token emessi"
  - "token emessi [WCF]"
  - "WCF, federazione"
ms.assetid: 4c31ee7d-a820-4067-8b84-a83049021bb6
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Federazione e token emessi
Con [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è possibile creare client che comunicano in modo protetto con servizi che implementano le specifiche di WS\-Federation e WS\-Trust.Le specifiche utilizzano XML, SOAP e Web Services Description Language \(WSDL\) per fornire meccanismi che consentano l'autenticazione e l'autorizzazione in diverse aree di attendibilità.  
  
## In questa sezione  
 [Federazione](../../../../docs/framework/wcf/feature-details/federation.md)  
 Fornisce una panoramica della federazione.  
  
 [Federazione e attendibilità](../../../../docs/framework/wcf/feature-details/federation-and-trust.md)  
 Elenca i problemi di progettazione da tenere in considerazione durante la creazione di servizi o di client federati.  
  
 [Procedura: creare un client federato](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)  
 Descrive le nozioni fondamentali sulla creazione di un client federato con [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [Procedura: configurare le credenziali in un servizio federativo](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)  
 Descrive i passaggi necessari per la creazione di un servizio federato.  
  
 [Procedura: creare una classe WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-create-a-wsfederationhttpbinding.md)  
 Descrive come configurare client e servizi che utilizzano `WSFederationHttpBinding`.  
  
 [Procedura: creare un servizio token di sicurezza](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-token-service.md)  
 Descrive i passaggi necessari per la creazione di un servizio token di sicurezza.  
  
 [Attestazioni e token SAML \(Security Assertions Markup Language\)](../../../../docs/framework/wcf/feature-details/saml-tokens-and-claims.md)  
 Descrive i token Security Assertions Markup Language \(SAML\) che sono flessibili e consentono di creare tipi di attestazione dettagliati.  
  
 [Procedura: configurare un emittente locale](../../../../docs/framework/wcf/feature-details/how-to-configure-a-local-issuer.md)  
 Descrive come creare un emittente locale di token di sicurezza.  
  
 [Procedura: disattivare sessioni protette in un'associazione WSFederationHttpBinding](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 Descrive come disattivare sessioni protette in `WSFederationHttpBinding`.La disattivazione di sessioni protette è necessaria in caso di creazione di una Web farm che richiede una sessione per ogni client.  
  
## Riferimenti  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>  
  
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>  
  
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenProvider>  
  
 <xref:System.ServiceModel.WSFederationHttpBinding>  
  
## Vedere anche  
 [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)   
 [Token personalizzati](../../../../docs/framework/wcf/extending/custom-tokens.md)   
 [Sicurezza e protezione](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)