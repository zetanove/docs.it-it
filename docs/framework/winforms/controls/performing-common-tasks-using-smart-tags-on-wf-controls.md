---
title: "Procedura dettagliata: esecuzione di attivit&#224; comuni utilizzando gli smart tag nei controlli Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "azioni di progettazione"
  - "DesignerAction (modello a oggetto)"
  - "smart tag"
ms.assetid: cac337e6-00f6-4584-80f4-75728f5ea113
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura dettagliata: esecuzione di attivit&#224; comuni utilizzando gli smart tag nei controlli Windows Form
Quando si creano form e controlli per le applicazioni Windows Form, molte attività vengono eseguite ripetutamente.  Di seguito sono riportate alcune delle attività comuni:  
  
-   Aggiunta o rimozione di una scheda in un <xref:System.Windows.Forms.TabControl>.  
  
-   Ancoraggio di un controllo al controllo padre.  
  
-   Modifica dell'orientamento di un controllo <xref:System.Windows.Forms.SplitContainer>.  
  
 Per rendere lo sviluppo più rapido, molti controlli offrono gli smart tag, ossia menu sensibili al contesto che consentono di eseguire le attività comuni con un singolo gesto in fase di progettazione.  Tali attività sono chiamate *verbi di smart tag*.  
  
 Gli smart tag restano allegati all'istanza di un controllo per la sua durata nella finestra di progettazione e sono sempre disponibili.  
  
 Di seguito vengono elencate le attività illustrate nella procedura dettagliata:  
  
-   Creazione di un progetto Windows Form  
  
-   Utilizzo degli smart tag  
  
-   Attivazione e disattivazione degli smart tag  
  
 Al termine, si saranno acquisite le informazioni circa il ruolo delle importanti funzionalità di layout.  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il form.  
  
#### Per creare il progetto  
  
1.  Creare un progetto di applicazione basata su Windows chiamato "SmartTagsExample".  Per informazioni dettagliate, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Selezionare il form in **Progettazione Windows Form**.  
  
## Utilizzo degli smart tag  
 Gli smart tag sono sempre disponibili in fase di progettazione per i controlli che li prevedono.  
  
#### Per utilizzare gli smart tag  
  
1.  Trascinare un controllo <xref:System.Windows.Forms.TabControl> dalla **Casella degli strumenti** nel form.  Si noti l'icona dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) che viene visualizzata sul lato del controllo <xref:System.Windows.Forms.TabControl>.  
  
2.  Fare clic sull'icona dello smart tag.  Nel menu di scelta rapida visualizzato accanto all'icona, selezionare la voce **Aggiungi scheda**.  Si osservi che una nuova scheda viene aggiunta al controllo <xref:System.Windows.Forms.TabControl>.  
  
3.  Trascinare un controllo <xref:System.Windows.Forms.TableLayoutPanel> dalla **Casella degli strumenti** al form.  
  
4.  Fare clic sull'icona dello smart tag.  Nel menu di scelta rapida visualizzato accanto all'icona, selezionare la voce **Aggiungi colonna**.  Si osservi che una nuova colonna viene aggiunta al controllo <xref:System.Windows.Forms.TableLayoutPanel>.  
  
5.  Trascinare un controllo <xref:System.Windows.Forms.SplitContainer> dalla **Casella degli strumenti** al form.  
  
6.  Fare clic sull'icona dello smart tag.  Nel menu di scelta rapida visualizzato accanto all'icona, selezionare la voce **Orientamento separatore orizzontale**.  La barra di divisione del controllo <xref:System.Windows.Forms.SplitContainer> viene orientata orizzontalmente.  
  
## Vedere anche  
 <xref:System.Windows.Forms.TextBox>   
 <xref:System.Windows.Forms.TabControl>   
 <xref:System.Windows.Forms.SplitContainer>   
 <xref:System.ComponentModel.Design.DesignerActionList>   
 [Walkthrough: Adding Smart Tags to a Windows Forms Component](../Topic/Walkthrough:%20Adding%20Smart%20Tags%20to%20a%20Windows%20Forms%20Component.md)