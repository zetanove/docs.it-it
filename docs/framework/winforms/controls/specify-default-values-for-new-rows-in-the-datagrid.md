---
title: "Procedura: specificare i valori predefiniti per le nuove righe nel controllo DataGridView di Windows Form | Microsoft Docs"
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
  - "griglie dei dati, valori predefiniti delle nuove righe"
  - "DataGridView (controllo) [Windows Form], immissione di dati"
  - "DataGridView (controllo) [Windows Form], valori predefiniti delle nuove righe"
  - "righe, specifica di valori predefiniti"
ms.assetid: 8d127963-d9f8-4e4e-9f7f-beb66688f1f2
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: specificare i valori predefiniti per le nuove righe nel controllo DataGridView di Windows Form
È possibile semplificare l'immissione dei dati facendo in modo che l'applicazione inserisca dei valori predefiniti nelle nuove righe aggiunte.  Mediante la classe <xref:System.Windows.Forms.DataGridView> è possibile inserire i valori predefiniti utilizzando l'evento <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded>,  che viene generato quando l'utente aggiunge una riga per immettere nuovi record.  Nel codice che gestisce questo evento è possibile popolare determinate celle con i valori desiderati.  
  
 Nell'esempio di codice riportato di seguito viene illustrato come specificare i valori predefiniti per le nuove righe utilizzando l'evento <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded>.  
  
## Esempio  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#120)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#120)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un controllo <xref:System.Windows.Forms.DataGridView> denominato`dataGridView1`.  
  
-   Una funzione `NewCustomerId` per la generazione di valori `CustomerID` univoci.  
  
-   Riferimenti agli assembly <xref:System?displayProperty=fullName> e <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=fullName>   
 [Immissione di dati nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [Utilizzo della riga per i nuovi record del controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)