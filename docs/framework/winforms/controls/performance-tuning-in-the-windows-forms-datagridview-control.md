---
title: "Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form | Microsoft Docs"
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
  - "DataGridView (controllo) [Windows Form], ottimizzazione delle prestazioni"
  - "ottimizzazione delle prestazioni, griglie dei dati"
  - "prestazioni, DataGridView (controllo)"
ms.assetid: 6ccbff28-a0ff-41e4-b601-61b31b61851d
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Ottimizzazione delle prestazioni nel controllo DataGridView Windows Form
Quando si utilizzano grandi quantità di dati, il controllo `DataGridView` può utilizzare una notevole quantità di memoria in overhead, a meno che non lo si impieghi in modo adeguato.  Nei client con memoria limitata, è possibile evitare l'overhead impedendo l'esecuzione di funzionalità che richiedono un notevole utilizzo della memoria.  È anche possibile eseguire manualmente alcune delle attività di gestione e recupero dei dati ricorrendo alla modalità virtuale per personalizzare l'utilizzo della memoria per uno scenario di questo tipo.  
  
## In questa sezione  
 [Procedure consigliate per ridimensionare il controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)  
 Viene descritto come impiegare il controllo `DataGridView` in maniera tale da evitare l'utilizzo non necessario della memoria e la riduzione delle prestazioni quando si opera con grandi quantità di dati.  
  
 [Modo virtuale nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)  
 Viene descritto come utilizzare la modalità virtuale per supportare o sostituire il meccanismo di associazione dati.  
  
 [Procedura dettagliata: implementazione della modalità virtuale nel controllo DataGridView Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)  
 Viene illustrato come implementare gestori per diversi eventi in modalità virtuale.  Viene inoltre illustrato come implementare il rollback e il commit a livello di riga per le modifiche dell'utente.  
  
 [Implementazione del modo virtuale con caricamento dati JIT nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
 Viene illustrato come caricare i dati su richiesta, operazione utile quando i dati da visualizzare sono in numero superiore rispetto alla capacità di memoria disponibile nel client.  
  
## Riferimenti  
 <xref:System.Windows.Forms.DataGridView>  
 Viene fornita la documentazione di riferimento per il controllo <xref:System.Windows.Forms.DataGridView>.  
  
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>  
 Viene fornita la documentazione di riferimento per la proprietà <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>.  
  
## Vedere anche  
 [Controllo DataGridView](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Modalità di visualizzazione dati nel controllo DataGridView di Windows Form](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)