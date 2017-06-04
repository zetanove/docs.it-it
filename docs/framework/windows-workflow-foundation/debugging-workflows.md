---
title: "Esecuzione del debug dei flussi di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b23b4814-ebb1-4c51-b7a9-469f4da7a96d
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Esecuzione del debug dei flussi di lavoro
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] offre diverse opzioni per eseguire il debug dei flussi di lavoro in esecuzione dall'ambiente di sviluppo.  Il debug dei flussi di lavoro può essere eseguito nell'utilità di progettazione, in XAML e nel codice.  
  
## Debug nell'utilità di progettazione del flusso di lavoro  
 Nelle attività dell'utilità di progettazione del flusso di lavoro è possibile impostare punti di interruzione evidenziando l'attività e premendo **F9** oppure usando il menu di scelta rapida dell'attività.  L'esecuzione del flusso di lavoro si interrompe quindi quando l'host del flusso di lavoro viene eseguito in modalità di debug.  Nella schermata seguente l'esecuzione del flusso di lavoro viene sospesa in un punto di interruzione.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Debug dei flussi di lavoro mediante Progettazione flussi di lavoro](../Topic/Debugging%20Workflows%20with%20the%20Workflow%20Designer.md).  
  
## Debug in XAML  
 Se un flusso di lavoro viene sospeso in un punto di interruzione nella finestra di progettazione, il flusso di lavoro può essere sottoposto a debug anche in XAML.  Per visualizzare il punto di esecuzione in XAML, selezionare **Visualizzazione XAML** nell'utilità di progettazione del flusso di lavoro quando l'esecuzione del flusso di lavoro viene sospesa.  Il debug può essere nuovamente avviato dalla finestra di progettazione riaprendo il flusso di lavoro nella finestra da Esplora soluzioni.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Procedura: debug di XML mediante Progettazione flussi di lavoro](../Topic/How%20to:%20Debug%20XAML%20with%20the%20Workflow%20Designer.md).  
  
## Debug nel codice  
 I punti di interruzione del codice possono essere usati nello stesso modo in [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] e in altre applicazioni imperative.  Fare clic sul margine sinistro del riquadro del codice per creare un punto di interruzione del codice o premere **F9** per posizionare un punto di interruzione in corrispondenza del percorso del cursore.  
  
## Connessione a un processo del flusso di lavoro  
 Il debug del flusso di lavoro è supportato anche usando l'infrastruttura di Visual Studio per la connessione a un processo.  In questo modo, l'autore del flusso di lavoro può eseguire il debug di un flusso di lavoro in esecuzione in un ambiente host diverso, ad esempio Internet Information Services \(IIS\) 7.0.  
  
## Debug remoto  
 Il debug remoto di [!INCLUDE[wf](../../../includes/wf-md.md)] funziona nello stesso modo del debug remoto per altri componenti [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)].  Per informazioni sul debug remoto, vedere [Procedura: attivare il debug remoto](http://go.microsoft.com/fwlink/?LinkId=196257).  
  
> [!NOTE]
>  Se l'applicazione flusso di lavoro è destinata all'architettura x86 ed è contenuta in un computer che esegue un sistema operativo a 64 bit, il debug remoto non funzionerà a meno che [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] sia installato nel computer remoto o la destinazione dell'applicazione flusso di lavoro è stata modificata in **Qualsiasi CPU**.  
  
## Estensione del servizio di debug del flusso di lavoro  
 Il servizio del debugger del flusso di lavoro è ora pubblico e può essere usato per creare applicazioni personalizzate quali monitoraggio, simulazione e debug in una finestra di progettazione riallocata.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] l'argomento <xref:System.Activities.Presentation.Debug.DebuggerService>.