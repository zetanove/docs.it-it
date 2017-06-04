---
title: "Attivit&#224; 1: creare una nuova applicazione Windows Presentation Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 270eaeba-9492-4532-af9f-403ce5c9935b
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Attivit&#224; 1: creare una nuova applicazione Windows Presentation Foundation
In questa attività verrà creata un'applicazione [!INCLUDE[avalon1](../../../includes/avalon1-md.md)] vuota tramite il modello di Visual Studio dell'applicazione WPF e verranno aggiunti riferimenti agli assembly del flusso di lavoro di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] appropriati.  
  
### Per creare il progetto applicazione WPF  
  
1.  Aprire [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] e scegliere **Nuovo** dal menu **File**, quindi **Progetto**.  
  
2.  Nella finestra di dialogo **Nuovo progetto** selezionare **Visual C\#** o **Visual Basic** nel riquadro **Modelli installati** sul lato sinistro della casella.Se il linguaggio scelto non viene visualizzato, cercarlo in **Altri linguaggi**.  
  
3.  Selezionare **Windows** nel riquadro **Modelli installati**.  
  
4.  Nel riquadro superiore verificare che sia stato selezionato **.NET Framework 4** \(impostazione predefinita\) nell'elenco a discesa, quindi scegliere **Applicazione WPF**.  
  
5.  Impostare il nome del progetto su **HostingApplication** nella parte inferiore della finestra.  
  
6.  Impostare il nome della soluzione su **RehostingTheDesigner**.  
  
7.  Fare clic su **OK** per creare il progetto di applicazione.[!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] consente di creare un'interfaccia utente WPF di base per l'applicazione e dispone di file XAML e code\-behind appropriati.  
  
8.  Aggiungere riferimenti agli assembly **WorkflowModel**.A tale scopo, in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **HostingApplication** e scegliere **Aggiungi riferimento**.  
  
9. Nella finestra di dialogo **Aggiungi riferimento** fare clic sulla scheda **.NET**, tenendo premuto CTRL selezionare gli assembly seguenti, quindi scegliere **OK**:  
  
    -   System.Activities  
  
    -   System.Activities.Presentation  
  
    -   System.Activities.Core.Presentation  
  
10. Scegliere **OK**.  
  
11. Per informazioni su come ospitare l'area di disegno dell'utilità di progettazione del flusso di lavoro, vedere [Attività 2: ospitare l'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md).  
  
## Vedere anche  
 [Riallocazione dell'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)   
 [Attività 2: ospitare l'utilità di progettazione del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md)