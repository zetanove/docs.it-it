---
title: "Procedura: specificare la modalit&#224; di modifica per il controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, modalità di modifica"
  - "DataGridView (controllo) [Windows Form], modalità di modifica"
ms.assetid: 93e117e8-94c4-411b-ba31-645e475ed85c
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura: specificare la modalit&#224; di modifica per il controllo DataGridView di Windows Form
Per impostazione predefinita, gli utenti possono modificare il contenuto della casella di testo corrente del controllo <xref:System.Windows.Forms.DataGridView> digitando al suo interno o premendo F2.  Questa operazione attiva la modalità di modifica della cella se sono soddisfatte tutte le seguenti condizioni:  
  
-   L'origine dati sottostante supporta la modifica.  
  
-   Il controllo <xref:System.Windows.Forms.DataGridView> è attivato.  
  
-   Il valore della proprietà <xref:System.Windows.Forms.DataGridView.EditMode%2A> non è <xref:System.Windows.Forms.DataGridViewEditMode>.  
  
-   Le proprietà `ReadOnly` di cella, riga, colonna e controllo sono tutte impostate su `false`.  
  
 In modalità di modifica l'utente può modificare il valore della cella e premere INVIO per eseguire il commit della modifica oppure ESC per ripristinare il valore originale della cella.  
  
 È possibile configurare un controllo <xref:System.Windows.Forms.DataGridView> in modo che una cella entri in modalità di modifica non appena diventa la cella corrente.  Il comportamento dei tasti INVIO ed ESC in questo caso non cambia, ma la cella rimane in modalità di modifica anche dopo il commit o il ripristino del valore originale.  È inoltre possibile configurare il controllo in modo che le celle entrino in modalità di modifica solo quando gli utenti digitano al loro interno o premono F2.  Infine, è possibile impedire che le celle entrino in modalità di modifica tranne nel caso in cui venga chiamato il metodo <xref:System.Windows.Forms.DataGridView.BeginEdit%2A>.  
  
### Per cambiare la modalità di modifica nel controllo DataGridView  
  
-   Impostare la proprietà <xref:System.Windows.Forms.DataGridView.EditMode%2A?displayProperty=fullName> sull'enumerazione <xref:System.Windows.Forms.DataGridViewEditMode> appropriata.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#067](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#067)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#067](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#067)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System> e <xref:System.Windows.Forms>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.EditMode%2A?displayProperty=fullName>   
 [Immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)