---
title: "Controllo dell&#39;avvio automatico di Host servizio WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "WcfOptions"
ms.assetid: 6abe5d34-519b-4cef-8f02-3c0a7f125585
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Controllo dell&#39;avvio automatico di Host servizio WCF
È possibile controllare le funzionalità di avvio automatico dell'host del servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] \(WcfSvcHost.exe\) per un progetto Libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] quando si esegue il debug di un altro progetto nella stessa soluzione [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] contenente più progetti.  
  
 A tale scopo, fare clic con il pulsante destro del mouse sul progetto di servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in **Esplora soluzioni**, scegliere **Proprietà** e fare clic su scheda **Opzioni WCF**.La casella di controllo **Avvia host servizio WCF durante il debug di un altro progetto nella stessa soluzione** è selezionata per impostazione predefinita.È possibile deselezionare la casella in modo che l'host del servizio di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per questo progetto specifico non venga avviato durante il debug di un altro nella stessa soluzione.  
  
 Questo comportamento non influisce sulle funzionalità di debug con F5 o con l'opzione Aggiungi riferimento al servizio per questo progetto.  
  
 Questa opzione è disponibile per i progetti seguenti:  
  
-   Progetto Libreria di servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
-   Progetto Libreria di servizi del flusso di lavoro sequenziale.  
  
-   Progetto Libreria di servizi del flusso di lavoro di una macchina a stati.  
  
-   Progetto Libreria di servizi di diffusione.  
  
## Vedere anche  
 [Host servizio WCF \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)