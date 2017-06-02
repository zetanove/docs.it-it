---
title: "Procedura: bloccare le colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione | Microsoft Docs"
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
  - "colonne [Windows Form], blocco"
  - "dati [Windows Form], visualizzazione"
  - "DataGridView (controllo) [Windows Form], blocco di colonna"
  - "Windows Form, colonne"
ms.assetid: 87412dd2-478f-4751-af87-dafc591fc215
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: bloccare le colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione
Talvolta potrebbe risultare necessario fare di frequente riferimento a una singola colonna o a un gruppo di colonne visualizzate in un controllo <xref:System.Windows.Forms.DataGridView> di Windows Form.  Ad esempio, quando si visualizza una tabella delle informazioni utente contenente molte colonne, è utile rendere sempre visibile il nome utente e attivare lo scorrimento delle altre colonne fuori dall'area visibile.  
  
 A tale scopo, è possibile bloccare le colonne nel controllo.  Quando si blocca una colonna, vengono bloccate anche tutte le colonne presenti a sinistra o, per gli script delle lingue da destra a sinistra, a destra.  Le colonne bloccate restano ferme mentre è possibile scorrere tutte le altre colonne.  Se il riordinamento delle colonne è attivato, le colonne bloccate vengono considerate come un gruppo separato dalle colonne non bloccate.  Gli utenti possono riposizionare le colonne in entrambi i gruppi, ma non possono spostare una colonna da un gruppo all'altro.  
  
 Nella seguente procedura è richiesto un progetto **Applicazione Windows** con un form contenente un controllo <xref:System.Windows.Forms.DataGridView>.  Per informazioni sull'impostazione di tali progetti, vedere [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa) e [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md).  
  
> [!NOTE]
>  È possibile che le finestre di dialogo e i comandi di menu visualizzati siano diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/esporta impostazioni** dal menu **Strumenti**.  Per ulteriori informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### Per bloccare una colonna utilizzando la finestra di progettazione  
  
1.  Scegliere il glifo dello smart tag \(![Glifo Smart Tag](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView> e quindi selezionare **Modifica colonne**.  
  
2.  Selezionare una colonna dall'elenco **Colonne selezionate**.  
  
3.  Nella griglia **Proprietà colonne** impostare la proprietà <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A> su `true`.  
  
    > [!NOTE]
    >  È inoltre possibile bloccare una colonna quando viene aggiunta selezionando la casella **Bloccato** nella finestra di dialogo **Aggiungi colonna**.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=fullName>   
 [Procedura: aggiungere e rimuovere colonne nel controllo DataGridView di Windows Form utilizzando Progettazione Windows Form](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md)   
 [Procedura: abilitare il riordinamento delle colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione](../../../../docs/framework/winforms/controls/enable-column-reordering-in-the-datagrid-using-the-designer.md)   
 [How to: Display Right\-to\-Left Text in Windows Forms for Globalization](http://msdn.microsoft.com/it-it/f0663385-2354-4c65-8676-706422283b14)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/it-it/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [Procedura: aggiungere controlli a un Windows Form](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)