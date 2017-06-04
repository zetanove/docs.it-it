---
title: "Estensione della protezione | Microsoft Docs"
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
  - "sicurezza [WCF], estensione"
ms.assetid: a015a040-9fdf-4147-9ea9-f83b570be1d4
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# Estensione della protezione
Per contenere nuovi tipi di attestazione e nuovi token personalizzati, è possibile estendere l'infrastruttura di sicurezza di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Questa operazione viene descritta negli argomenti di questa sezione.  
  
## In questa sezione  
 [Security Architecture](http://msdn.microsoft.com/it-it/16593476-d36a-408d-808c-ae6fd483e28f)  
 Viene illustrata l'architettura del sistema della protezione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [Credenziale personalizzata e convalida della credenziale](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md)  
 Viene spiegato il modo in cui il modello di identità viene utilizzato durante la convalida di credenziali personalizzate.  
  
 [Token personalizzati](../../../../docs/framework/wcf/extending/custom-tokens.md)  
 I token rilasciati da un servizio token di sicurezza \(STS\) sono in genere token SAML.In questo argomento viene spiegato come creare un tipo di token personalizzato.  
  
 [Autorizzazione personalizzata](../../../../docs/framework/wcf/extending/custom-authorization.md)  
 Viene spiegato come implementare un'autorizzazione personalizzata.  
  
 [Override dell'identità di un servizio per l'autenticazione](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md)  
 Viene descritto come eseguire l'override dell'identità di un servizio per l'autenticazione.  
  
 [Procedura: creare un verificatore di identità client personalizzato](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md)  
 Viene dimostrato come convalidare l'identità di un endpoint personalizzato.  
  
 [Procedura: utilizzare certificati X.509 separati per la firma e la crittografia](../../../../docs/framework/wcf/extending/how-to-use-separate-x-509-certificates-for-signing-and-encryption.md)  
 I messaggi vengono in genere firmati e crittografati con un solo certificato.In questo argomento viene spiegato come sia possibile utilizzare due certificati, se necessario.  
  
 [Procedura: modificare il provider di crittografia per la chiave privata di un certificato X.509](../../../../docs/framework/wcf/extending/change-cryptographic-provider-x509-certificate-private-key.md)  
 Viene illustrato come modificare il provider di crittografia utilizzato per fornire la chiave privata di un certificato X.509 e come integrare il provider nel framework di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## Riferimenti  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
## Sezioni correlate  
 [Sicurezza](../../../../docs/framework/wcf/feature-details/security.md)  
  
 [Programmazione WCF di base](../../../../docs/framework/wcf/basic-wcf-programming.md)  
  
## Vedere anche  
 [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md)