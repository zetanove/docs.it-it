---
title: "Procedura: aggiungere un riferimento al servizio dati (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, configurazione"
ms.assetid: 62c6f318-3ee1-433a-b7a3-efa234c3034c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: aggiungere un riferimento al servizio dati (WCF Data Services)
È possibile usare la finestra di dialogo **Aggiungi riferimento al servizio** in Visual Studio per aggiungere un riferimento a [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)].  In questo modo è possibile accedere più facilmente a un servizio dati in un'applicazione client sviluppata in Visual Studio.  Al completamento di questa procedura, verranno generate classi di dati in base ai metadati ottenuti dal servizio dati.  Per altre informazioni, vedere [Generazione della libreria client del servizio dati](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md).  
  
### Per aggiungere un riferimento al servizio dati  
  
1.  \(Facoltativo\) Se il servizio dati non fa parte della soluzione e non è già in esecuzione, avviare il servizio dati e prendere nota dell'URI del servizio dati.  
  
2.  Fare clic con il pulsante destro del mouse sul progetto client, quindi scegliere **Aggiungi riferimento al servizio**.  
  
3.  Se il servizio dati fa parte della soluzione corrente, fare clic su **Individua**.  
  
     \-oppure\-  
  
     Nella casella di testo **Indirizzo** immettere l'URL di base del servizio dati, ad esempio `http://localhost:1234/Northwind.svc`, quindi fare clic su **Vai**.  
  
4.  Fare clic su **OK**.  
  
     Aggiunge un nuovo file di codice contenente le classi di dati usate per accedere e interagire con le risorse del servizio dati come oggetti.  
  
## Vedere anche  
 [Guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)