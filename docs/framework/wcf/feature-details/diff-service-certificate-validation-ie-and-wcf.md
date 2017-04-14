---
title: "Differenze tra la convalida del certificato di servizio eseguita in Internet Explorer e in WCF | Microsoft Docs"
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
  - "certificati [WCF], convalida della certificazione di servizio"
  - "convalida della certificazione di servizio [WCF]"
ms.assetid: 9dffcab2-70a9-40f0-99fd-d3a0b296028f
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Differenze tra la convalida del certificato di servizio eseguita in Internet Explorer e in WCF
A causa della differenza del modo in cui in Internet Explorer e in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene eseguita la convalida di certificati del servizio quando viene utilizzato HTTPS, è possibile che con Internet Explorer non sia possibile accedere alla pagina della Guida o a WSDL \(Web Services Description Language\) di un servizio, nonostante un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sia in grado di inviare messaggi correttamente agli endpoint del servizio.Ciò avviene perché in Internet Explorer viene verificato se il certificato del servizio dispone degli identificatori dell'oggetto \(OID\) `ServerAuthentication` nei flag di utilizzo migliorato, mentre in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tale vincolo non viene applicato.Se Internet Explorer non è in grado di accedere alla pagina della Guida o a WSDL del servizio, utilizzare [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per accedere ai metadati del servizio.  
  
## Vedere anche  
 [Differenze di convalida del certificato tra HTTPS, SSL su TCP e protezione SOAP](../../../../docs/framework/wcf/feature-details/cert-val-diff-https-ssl-over-tcp-and-soap.md)   
 [Procedura: recuperare metadati e implementare un servizio conforme](../../../../docs/framework/wcf/feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md)