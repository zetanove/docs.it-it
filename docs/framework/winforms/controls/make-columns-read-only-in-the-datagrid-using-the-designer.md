---
title: "Procedura: rendere le colonne di sola lettura nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "colonne [Windows Form], sola lettura"
  - "dati [Windows Form], visualizzazione"
  - "DataGridView (controllo) [Windows Form], colonne di sola lettura"
  - "Windows Form, colonne"
ms.assetid: b4ef7a75-ab33-4ee3-b2cf-201530e454e9
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: rendere le colonne di sola lettura nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione
Per impostazione predefinita, gli utenti possono modificare il testo e i dati numerici visualizzati nel controllo <xref:System.Windows.Forms.DataGridView> di Windows Form.  Per visualizzare i dati senza permetterne la modifica, è necessario rendere le colonne con i dati di sola lettura.  Per informazioni sulla procedura per rendere l'intero controllo di sola lettura, vedere [Procedura: impedire l'aggiunta e l'eliminazione di righe nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-in-the-datagrid-using-the-designer.md).  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per rendere una colonna di sola lettura utilizzando la finestra di progettazione  
  
1.  Scegliere il glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView> e quindi selezionare **Modifica colonne**.  
  
2.  Selezionare una colonna dall'elenco **Colonne selezionate**.  
  
3.  Nella griglia **Proprietà colonne** impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A> su `true`.  
  
    > [!NOTE]
    >  È anche possibile rendere una colonna di sola lettura quando la si aggiunge, selezionando la casella di controllo **Sola lettura** nella finestra di dialogo **Aggiungi colonna**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A?displayProperty=fullName>   
 [Procedura: aggiungere e rimuovere colonne nel controllo DataGridView di Windows Form utilizzando Progettazione Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md)   
 [Procedura: impedire l'aggiunta e l'eliminazione di righe nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-in-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)