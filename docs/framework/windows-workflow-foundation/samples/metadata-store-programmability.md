---
title: "Programmabilit&#224; dell&#39;archivio di metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5b613661-f3f9-4e07-8e88-28c9ea2fd8f8
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Programmabilit&#224; dell&#39;archivio di metadati
L'archivio di metadati è una funzionalità di [!INCLUDE[wfd1](../../../../includes/wfd1-md.md)] che consente l'associazione di metadati arbitrari, nel formato di attributi CLR, ai tipi in fase di esecuzione.In questo modo è possibile un accoppiamento libero tra i componenti runtime e le controparti in fase di progettazione e la possibilità di modificare i componenti della fase di progettazione senza incidere sul runtime.In questo esempio viene illustrato come programmare in base all'archivio di metadati applicando attributi a un tipo in fase di esecuzione, ovvero l'origine che non può essere controllata.Secondo la terminologia utilizzata in genere, un'applicazione host registra i metadati per un set di tipi.  
  
 All'interno dell'output, è possibile notare un attributo aggiuntivo imprevisto <xref:System.Runtime.InteropServices.GUIDAttribute>.Viene aggiunto in caso di utilizzo dell'API dei metadati e non ha alcun impatto sull'esecuzione dell'esempio.  
  
 In questo esempio viene illustrato quanto segue:  
  
## Dimostrazione  
  
-   Inserimento di attributi tramite l'API dell'archivio di metadati.  
  
-   Utilizzo di un meccanismo di callback per rinviare la registrazione di metadati.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione ProgrammingMetadataStore.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\MetadataStore`  
  
## Vedere anche