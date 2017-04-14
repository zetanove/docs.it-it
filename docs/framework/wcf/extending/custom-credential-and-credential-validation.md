---
title: "Credenziale personalizzata e convalida della credenziale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "convalida di credenziali [WCF]"
  - "credenziali [WCF]"
  - "credenziali [WCF], personalizzati"
  - "credenziali [WCF], convalida"
  - "credenziali personalizzate [WCF]"
ms.assetid: da831bec-e281-4d44-b343-437b5eef688e
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Credenziale personalizzata e convalida della credenziale
La protezione in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] si basa sullo scambio di credenziali tra servizi e client.  La maggior parte degli scenari di sicurezza può essere soddisfatta usando tipi di credenziali comuni, ad esempio Windows \(Kerberos\), nome utente e password e certificati.  Tuttavia, se è necessario un nuovo tipo di credenziale, negli argomenti di questa sezione viene illustrato come gestire e convalidare nuovi tipi.  
  
## In questa sezione  
 [Procedura: creare un servizio che usa un validator del certificato personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)  
 Viene illustrato come personalizzare la convalida [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ereditando dalla classe <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  
  
 [Procedura: creare credenziali client e del servizio personalizzate](../../../../docs/framework/wcf/extending/walkthrough-creating-custom-client-and-service-credentials.md)  
 Viene illustrato come estendere le classi <xref:System.ServiceModel.Description.ClientCredentials> e <xref:System.ServiceModel.Description.ServiceCredentials> per accogliere nuovi tipi di credenziali.  Si tratta del primo di una serie di argomenti sulla creazione di tipi di credenziali personalizzati.  
  
 [Procedura: creare un provider di token di sicurezza personalizzati](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-provider.md)  
 Viene illustrato come creare un provider di token di sicurezza per gestire nuovi tipi di credenziali e restituire nuovi token per la credenziale.  Si tratta del secondo argomento della serie.  
  
 [Procedura: creare un autenticatore del token di sicurezza personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-security-token-authenticator.md)  
 Viene illustrato come creare un autenticatore personalizzato per autenticare un nuovo tipo di credenziale.  Si tratta del terzo argomento della serie.  
  
## Riferimenti  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
 <xref:System.IdentityModel.Selectors.X509CertificateValidator>  
  
 <xref:System.ServiceModel.Description.ClientCredentials>  
  
 <xref:System.ServiceModel.Description.ServiceCredentials>  
  
## Sezioni correlate  
 [Autenticazione](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)  
  
 [Federazione e token emessi](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)  
  
 [Autorizzazione](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
  
## Vedere anche  
 [Sicurezza](../../../../docs/framework/wcf/feature-details/security.md)