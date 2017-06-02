---
title: "Procedura: aggiungere una colonna non associata a un controllo DataGridView di Windows Form associato ai dati | Microsoft Docs"
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
  - "colonne [Windows Form], dati non associati"
  - "griglie dei dati, aggiunta di colonne non associate"
  - "DataGridView (controllo) [Windows Form], dati non associati"
ms.assetid: f7bdc4d8-ba8e-421b-ad62-82d936f01372
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: aggiungere una colonna non associata a un controllo DataGridView di Windows Form associato ai dati
I dati visualizzati nel controllo <xref:System.Windows.Forms.DataGridView> in genere provengono da un'origine dati di qualche tipo, ma è possibile visualizzare una colonna di dati di origine diversa.  Questo tipo di colonna è detto colonna non associata.  Le colonne non associate possono assumere molte forme.  Spesso vengono usate per fornire accesso ai dettagli di una riga di dati.  
  
 Nell'esempio di codice seguente viene illustrato come creare una colonna non associata di pulsanti **Dettagli** per visualizzare una tabella figlio correlata a una data riga in una tabella padre quando si implementa uno scenario Master\-Details.  Per rispondere alle selezioni dei pulsanti, implementare un gestore dell'evento <xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=fullName> che visualizzi un form contenente la tabella figlio.  
  
 Questa attività è supportata in Visual Studio.  Vedere anche [Procedura: Aggiungere e rimuovere colonne nel controllo DataGridView Windows Form usando Progettazione Windows Form](http://msdn.microsoft.com/library/dyyesckz\(v=vs.110\)).  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#010](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#010)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#010](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#010)]  
  
## Compilazione del codice  
 L'esempio presenta i requisiti seguenti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1`.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 [Visualizzazione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Modalità di visualizzazione dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)