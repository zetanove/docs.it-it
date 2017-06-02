---
title: "Procedura: distribuire un&#39;applicazione di integrazione COM+ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e5a0510-db3c-4988-a09c-696285836650
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Procedura: distribuire un&#39;applicazione di integrazione COM+
Dopo aver scritto un'applicazione di integrazione COM\+, è possibile distribuirla ad altri computer.In questo argomento viene illustrato come trasferire un'applicazione di integrazione COM\+ da un computer a un altro.  
  
### Trasferimento di un'applicazione di integrazione COM\+ ospitata  
  
1.  Assicurarsi che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sia installato su entrambi i computer.  
  
2.  Esportare l'applicazione dal computer A.  
  
3.  Importare l'applicazione nel computer B.  
  
4.  Impostare la directory principale dell'applicazione.Per convenzione, è %PROGRAMFILES%\/ComPlus Applications\/{AppGUID}.  
  
5.  Copiare i file Application.config e Application.manifest dalla directory principale dell'applicazione del computer A nella directory principale dell'applicazione del computer B.  
  
6.  Modificare gli indirizzi endpoint del servizio nel file Application.config nel computer B per identificare il computer appropriato.Cambiare, ad esempio, http:\/\/machineA\/MyService in http:\/\/machineB\/MyService.  
  
### Trasferimento di un'applicazione di integrazione ospitata da Web  
  
1.  Assicurarsi che [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sia installato su entrambi i computer.  
  
2.  Esportare l'applicazione dal computer A.  
  
3.  Importare l'applicazione nel computer B.  
  
4.  Creare una radice virtuale di IIS nel computer B.  
  
5.  Copiare il file con estensione svc \(componentName.svc\) e il file Web.config dalla radice virtuale nel computer A nella radice virtuale appena creata nel computer B.  
  
## Vedere anche  
 [Panoramica sull'integrazione con applicazioni COM\+](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications-overview.md)   
 [Procedura: configurare le impostazioni del servizio COM\+](../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)   
 [Procedura: utilizzare lo strumento di configurazione del modello di servizi di COM\+](../../../../docs/framework/wcf/feature-details/how-to-use-the-com-service-model-configuration-tool.md)