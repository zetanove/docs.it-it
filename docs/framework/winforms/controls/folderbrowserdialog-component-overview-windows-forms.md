---
title: "Cenni preliminari sul componente FolderBrowserDialog (Windows Form) | Microsoft Docs"
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
  - "FolderBrowserDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "directory [Windows Form], abilitazione dell'esplorazione nelle applicazioni"
  - "FolderBrowserDialog (componente) [Windows Form], informazioni"
  - "cartelle [Windows Form], abilitazione dell'esplorazione nelle applicazioni"
ms.assetid: 796b622c-3ba9-4356-93bb-e217fc52f2c7
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Cenni preliminari sul componente FolderBrowserDialog (Windows Form)
Il componente <xref:System.Windows.Forms.FolderBrowserDialog> di Windows Form è una finestra di dialogo modale utilizzata per l'individuazione e la selezione di cartelle.  Nel componente <xref:System.Windows.Forms.FolderBrowserDialog> è inoltre possibile creare nuove cartelle.  
  
> [!NOTE]
>  Per selezionare file anziché cartelle, utilizzare il componente [OpenFileDialog](../../../../docs/framework/winforms/controls/openfiledialog-component-windows-forms.md).  
  
 Il componente <xref:System.Windows.Forms.FolderBrowserDialog> viene visualizzato in fase di esecuzione utilizzando il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>.  Impostare la proprietà <xref:System.Windows.Forms.FolderBrowserDialog.RootFolder%2A> per stabilire la cartella attiva e le eventuali sottocartelle visualizzate nella visualizzazione struttura ad albero della finestra di dialogo.  Una volta visualizzata la finestra di dialogo, è possibile utilizzare la proprietà <xref:System.Windows.Forms.FolderBrowserDialog.SelectedPath%2A> per ottenere il percorso della cartella selezionata.  
  
 Quando viene aggiunto a un form, il componente <xref:System.Windows.Forms.FolderBrowserDialog> è visualizzato nella barra delle applicazioni nella parte inferiore di Progettazione Windows Form.  
  
## Vedere anche  
 <xref:System.Windows.Forms.FolderBrowserDialog>   
 [Procedura: scegliere cartelle con il componente FolderBrowserDialog di Windows Form](../../../../docs/framework/winforms/controls/how-to-choose-folders-with-the-windows-forms-folderbrowserdialog-component.md)   
 [Componente FolderBrowserDialog](../../../../docs/framework/winforms/controls/folderbrowserdialog-component-windows-forms.md)