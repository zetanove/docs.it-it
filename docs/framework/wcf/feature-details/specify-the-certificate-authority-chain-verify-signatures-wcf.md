---
title: "Procedura: specificare la catena di certificati di autorit&#224; di certificazione utilizzata per verificare le firme (WCF) | Microsoft Docs"
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
  - "certificati [WCF], indicazione della catena di certificati di autorità di certificazione"
  - "certificati [WCF], verifica di firme"
ms.assetid: 7c719355-aa41-4567-80d0-5115a8cf73fd
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: specificare la catena di certificati di autorit&#224; di certificazione utilizzata per verificare le firme (WCF)
Per impostazione predefinita, quando riceve un messaggio SOAP firmato mediante un certificato X.509, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] verifica che quest'ultimo sia stato emesso da un autorità di certificazione attendibile.A tale scopo viene eseguita una ricerca in un archivio certificati per determinare se il certificato di tale autorità di certificazione è stato riconosciuto come attendibile.Affinché [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sia in grado di svolgere questa ricerca, è necessario che la catena di certificati dell'autorità di certificazione sia installata nell'archivio certificati corretto.  
  
### Per installare una catena di certificati dell'autorità di certificazione  
  
-   Per ogni autorità di certificazione che rilascia certificati X.509 che un destinatario di messaggi SOAP intende ritenere attendibile, installare la catena di certificati dell'autorità di certificazione nell'archivio certificati configurato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] come origine dei certificati X.509.  
  
     Ad esempio, se un destinatario di messaggi SOAP intende ritenere attendibili i certificati X.509 rilasciati da Microsoft, è necessario installare la catena di certificati dell'autorità di certificazione di Microsoft nell'archivio certificati in cui [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ricerca i certificati X.509.L'archivio certificati nel quale [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] esegue la ricerca dei certificati X.509 può essere specificato in codice o in configurazione.La specifica in codice può ad esempio essere eseguita tramite il metodo <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>. Esistono inoltre vari modi per eseguire la specifica in configurazione, fra cui mediante l'utilizzo dell'[\<certificatoServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md).  
  
     Poiché Windows offre un set incorporato di catene di certificati predefinite di autorità di certificazione attendibili, è possibile che non sia necessario installare la catena di certificati per tutte le autorità di certificazione.  
  
    1.  Esportare la catena di certificati dell'autorità di certificazione.  
  
         La modalità utilizzata per eseguire questa operazione varia a seconda dell'autorità di certificazione.Se l'autorità di certificazione esegue Servizi certificati Microsoft, selezionare **Scarica un certificato CA, la catena di certificati o l'elenco di revoche di certificati**, quindi **Esegui download certificato CA**.  
  
    2.  Importare la catena di certificati dell'autorità di certificazione.  
  
         In Microsoft Management Console \(MMC\), aprire lo snap\-in Certificati.Per l'archivio certificati da cui [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] recupera i certificati X.509, selezionare la cartella **Autorità di certificazione** **radice attendibili**.Nella cartella **Autorità di certificazione radice attendibili**, fare clic con il pulsante destro del mouse sulla cartella **Certificati**, scegliere **Tutte le attività** e quindi fare clic su **Importa**.Indicare il file esportato nel primo passaggio.  
  
         [!INCLUDE[crabout](../../../../includes/crabout-md.md)] sull'utilizzo dello snap\-in Certificati di MMC, vedere [Procedura: visualizzare certificati con lo snap\-in MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).  
  
## Vedere anche  
 [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)