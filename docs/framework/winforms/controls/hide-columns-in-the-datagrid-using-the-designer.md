---
title: "Procedura: nascondere le colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "colonne [Windows Form], nascondere"
  - "dati [Windows Form], visualizzazione"
  - "DataGridView (controllo) [Windows Form], occultamento di colonna"
  - "Windows Form, colonne"
ms.assetid: a81c38e6-2527-426a-bcb1-be691403be04
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: nascondere le colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione
Talvolta potrebbe essere necessario visualizzare solo alcune delle colonne disponibili in un controllo <xref:System.Windows.Forms.DataGridView> di Windows Form.  Ad esempio, si potrebbe voler visualizzare la colonna degli stipendi degli impiegati solo per gli utenti con credenziali di gestione, nascondendola per tutti gli altri utenti.  In alternativa, si potrebbe voler associare il controllo a un'origine dati che contiene molte colonne, rendendo visibili solo alcune di esse.  In questo caso, generalmente si rimuovono le colonne non desiderate dalla visualizzazione invece di nasconderle.  Per ulteriori informazioni, vedere [Procedura: aggiungere e rimuovere colonne nel controllo DataGridView di Windows Form utilizzando Progettazione Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md).  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per nascondere una colonna utilizzando la finestra di progettazione  
  
1.  Scegliere il glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView> e quindi selezionare **Modifica colonne**.  
  
2.  Selezionare una colonna dall'elenco **Colonne selezionate**.  
  
3.  Nella griglia **Proprietà colonne** impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A> su `false`.  
  
    > [!NOTE]
    >  È possibile nascondere una colonna anche quando la si aggiunge, deselezionando la casella di controllo **Visibile** nella finestra di dialogo **Aggiungi colonna**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn.Visible%2A?displayProperty=fullName>   
 [Procedura: aggiungere e rimuovere colonne nel controllo DataGridView di Windows Form utilizzando Progettazione Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)