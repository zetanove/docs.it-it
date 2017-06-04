---
title: "Procedura: aggiungere colonne al controllo ListView Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "colonne [Windows Form], aggiunta a controlli ListView"
  - "ListView (controllo) [Windows Form], aggiunta di intestazioni di colonne"
ms.assetid: 5b1a8b4d-587e-479a-95c1-f9b90884f13a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: aggiungere colonne al controllo ListView Windows Form utilizzando la finestra di progettazione
Il controllo <xref:System.Windows.Forms.ListView> Windows Form nella visualizzazione **Dettagli** è in grado di visualizzare più colonne per ciascun elemento dell'elenco.  È possibile utilizzare le colonne per visualizzare più tipi di informazioni su ciascuna voce di elenco.  Relativamente a un elenco di file, ad esempio, è possibile visualizzare il nome, il tipo, le dimensioni e la data dell'ultima modifica.  Per informazioni sulla compilazione delle colonne una volta create, vedere [Procedura: visualizzare elementi secondari nelle colonne con il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md).  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.ListView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per aggiungere colonne nella finestra di progettazione  
  
1.  Nella finestra **Proprietà** impostare la proprietà <xref:System.Windows.Forms.ListView.View%2A> del controllo su <xref:System.Windows.Forms.View>.  
  
2.  Nella finestra **Proprietà**, fare clic sul pulsante con i **puntini di sospensione** \(![Schermata VisualStudioEllipsesButton](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) accanto alla proprietà <xref:System.Windows.Forms.ListView.Columns%2A>.  
  
     Verrà visualizzato l'**Editor della raccolta ColumnHeader**.  
  
3.  Utilizzare il pulsante **Aggiungi** per aggiungere nuove colonne.  È quindi possibile selezionare l'intestazione della colonna e impostarne il testo, ovvero la didascalia della colonna, l'allineamento e la larghezza.  
  
## Vedere anche  
 [Cenni preliminari sul controllo ListView](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)   
 [Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form](../../../../docs/framework/winforms/controls/how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)   
 [Procedura: visualizzare elementi secondari nelle colonne con il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)   
 [Procedura: visualizzare icone per il controllo ListView Windows Form](../../../../docs/framework/winforms/controls/how-to-display-icons-for-the-windows-forms-listview-control.md)   
 [Procedura: aggiungere informazioni personalizzate a un controllo TreeView o ListView \(Windows Form\)](../../../../docs/framework/winforms/controls/add-custom-information-to-a-treeview-or-listview-control-wf.md)