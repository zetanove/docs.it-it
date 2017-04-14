---
title: "Cenni preliminari sul controllo ToolBar (Windows Form) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ToolBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ToolBar (controllo) [Windows Form], informazioni sui controlli ToolBar"
  - "barre degli strumenti [Windows Form], informazioni sulle barre degli strumenti"
ms.assetid: d426b203-0216-4dbe-b834-1641e50a9c29
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Cenni preliminari sul controllo ToolBar (Windows Form)
> [!NOTE]
>  Benché il controllo <xref:System.Windows.Forms.ToolStrip> sostituisca il controllo <xref:System.Windows.Forms.ToolBar> aggiungendovi funzionalità, il controllo <xref:System.Windows.Forms.ToolBar> viene mantenuto per compatibilità con le versioni precedenti e per un eventuale utilizzo futuro.  
  
 Il controllo <xref:System.Windows.Forms.ToolBar> Windows Form viene utilizzato nei form come barra di controllo sulla quale viene visualizzata una riga di menu a discesa e pulsanti bitmap per l'attivazione dei comandi.  In tal modo, fare clic su un pulsante della barra degli strumenti equivale a scegliere un comando di menu.  È possibile configurare i pulsanti perché abbiano l'aspetto e il comportamento di pulsanti di comando, menu a discesa o separatori.  In genere, una barra degli strumenti contiene pulsanti e menu che corrispondono alle voci della struttura di menu di un'applicazione e forniscono un rapido accesso alle funzioni e ai comandi utilizzati più di frequente in un'applicazione.  
  
## Utilizzo del controllo barra degli strumenti  
 Un controllo <xref:System.Windows.Forms.ToolBar> è in genere "ancorato" alla parte superiore della finestra padre, ma può essere ancorato a qualsiasi lato della finestra.  Una barra degli strumenti può visualizzare le descrizioni dei comandi quando l'utente sposta il puntatore del mouse su uno dei pulsanti.  Una descrizione comandi è una piccola finestra popup che descrive brevemente la funzione del pulsante o del menu.  Per visualizzare le descrizioni comando è necessario impostare la proprietà <xref:System.Windows.Forms.ToolBar.ShowToolTips%2A> su `true`.  
  
> [!NOTE]
>  I controlli di determinate applicazioni sono molto simili alla barra degli strumenti, in quanto possono essere riposizionati e "ancorati" al di sopra della finestra dell'applicazione.  Il controllo ToolBar Windows Form non consente di eseguire queste operazioni.  
  
 Quando la proprietà <xref:System.Windows.Forms.ToolBar.Appearance%2A> è impostata su [Normal](frlrfSystemWindowsFormsToolBarAppearanceClassTopic), i pulsanti della barra degli strumenti appaiono sollevati e tridimensionali.  Affinché i pulsanti e la barra degli strumenti possano apparire piatti, impostare la proprietà <xref:System.Windows.Forms.ToolBar.Appearance%2A> della barra degli strumenti su <xref:System.Windows.Forms.ToolBarAppearance>.  I pulsanti assumono un aspetto tridimensionale quando il puntatore del mouse viene spostato su di essi.  I pulsanti della barra degli strumenti possono essere suddivisi in gruppi logici tramite dei separatori.  Un separatore è un pulsante della barra degli strumenti in cui la proprietà <xref:System.Windows.Forms.ToolBarButton.Style%2A> è impostata su [Separator](frlrfSystemWindowsFormsToolBarButtonStyleClassTopic).  Viene visualizzato sulla barra degli strumenti come uno spazio vuoto.  Quando per la barra degli strumenti si è impostato l'aspetto "piatto", i separatori sono visualizzati come linee anziché come spazi tra i pulsanti.  
  
 Con il controllo <xref:System.Windows.Forms.ToolBar> è possibile creare barre degli strumenti aggiungendo oggetti <xref:System.Windows.Forms.Button> a una raccolta di elementi <xref:System.Windows.Forms.ToolBar.Buttons%2A>.  Per aggiungere i pulsanti a un controllo <xref:System.Windows.Forms.ToolBar>, utilizzare l'editor della raccolta; a ciascun oggetto <xref:System.Windows.Forms.Button> dovrà essere associato testo o un'immagine, o entrambi.  L'immagine viene fornita da un componente [ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) associato.  In fase di esecuzione è possibile aggiungere o rimuovere pulsanti dall'insieme <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection> utilizzando rispettivamente i metodi <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Add%2A> e <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Remove%2A>.  Per programmare i pulsanti di un controllo <xref:System.Windows.Forms.ToolBar>, aggiungere codice agli eventi <xref:System.Windows.Forms.ToolBar.ButtonClick> del controllo <xref:System.Windows.Forms.ToolBar>, utilizzando la proprietà <xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A> della classe <xref:System.Windows.Forms.ToolBarButtonClickEventArgs> per determinare il pulsante selezionato.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ToolBar>   
 [Controllo ToolBar](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)   
 [Procedura: aggiungere pulsanti a un controllo ToolBar](../../../../docs/framework/winforms/controls/how-to-add-buttons-to-a-toolbar-control.md)   
 [Procedura: definire un'icona per un pulsante ToolBar](../../../../docs/framework/winforms/controls/how-to-define-an-icon-for-a-toolbar-button.md)   
 [Procedura: attivare eventi di menu per i pulsanti di una barra degli strumenti](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)