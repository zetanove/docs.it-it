---
title: "Procedura: esplorare dati in Windows Form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "CurrencyManager (classe), esplorazione di dati in Windows Form"
  - "cursori, origini dati"
  - "dati [Windows Form], esplorazione"
  - "origini dati, Windows Form"
  - "Windows Form, esplorazione"
ms.assetid: 97360f7b-b181-4084-966a-4c62518f735b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: esplorare dati in Windows Form
Il modo più semplice di spostarsi tra i record di un'origine dati in un'applicazione Windows consiste nell'associare un componente <xref:System.Windows.Forms.BindingSource> all'origine dati e poi nell'associare i controlli alla classe <xref:System.Windows.Forms.BindingSource>.  In seguito sarà possibile applicare il metodo di navigazione incorporato alla classe <xref:System.Windows.Forms.BindingSource>, ad esempio <xref:System.Windows.Forms.BindingSource.MoveNext%2A>, <xref:System.Windows.Forms.BindingSource.MoveLast%2A>, <xref:System.Windows.Forms.BindingSource.MovePrevious%2A> e <xref:System.Windows.Forms.BindingSource.MoveFirst%2A>.  Con questi metodi vengono adattate in maniera appropriata le proprietà <xref:System.Windows.Forms.BindingSource.Position%2A> e <xref:System.Windows.Forms.BindingSource.Current%2A> della classe <xref:System.Windows.Forms.BindingSource>.  È inoltre possibile trovare un elemento e impostarlo come elemento corrente impostando la proprietà <xref:System.Windows.Forms.BindingSource.Position%2A>.  
  
### Per incrementare la posizione in un'origine dati  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.BindingSource.Position%2A> della classe <xref:System.Windows.Forms.BindingSource> per i dati associati sulla posizione del record su cui spostarsi.  Nell'esempio riportato di seguito viene illustrato l'utilizzo del metodo <xref:System.Windows.Forms.BindingSource.MoveNext%2A> della classe <xref:System.Windows.Forms.BindingSource> per incrementare la proprietà <xref:System.Windows.Forms.BindingSource.Position%2A> quando si fa clic su `nextButton`.  La classe <xref:System.Windows.Forms.BindingSource> è associata alla tabella `Customers` di un dataset `Northwind`.  
  
    > [!NOTE]
    >  Se la proprietà <xref:System.Windows.Forms.BindingSource.Position%2A> viene impostata su un valore oltre il primo o l'ultimo record non viene generato alcun errore, perché [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] non consente di impostare la posizione su un valore non incluso nelle associazioni dell'elenco.  Se è importante che l'applicazione sia in grado di rilevare se è stato oltrepassato il primo o l'ultimo record, includere una logica per verificare se viene superato il numero degli elementi di dati.  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.NavigatingData#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#4)]  
  
### Per verificare se è stato superato il primo o l'ultimo elemento  
  
1.  Creare un gestore eventi per l'evento <xref:System.Windows.Forms.BindingSource.PositionChanged>.  Nel gestore eventi è possibile verificare se i valori della posizione proposta hanno superato il numero effettivo degli elementi di dati.  
  
     Nell'esempio che segue viene illustrato come verificare se è stato raggiunto l'ultimo elemento di dati.  Se ci si trova sull'ultimo elemento, il pulsante **Avanti** del form verrà disabilitato.  
  
    > [!NOTE]
    >  Se si modifica l'elenco in cui ci si sposta nel codice, sarà necessario riattivare il pulsante **Avanti** in modo che gli utenti possano spostarsi all'interno di tutto il nuovo elenco.  Inoltre, l'evento <xref:System.Windows.Forms.BindingSource.PositionChanged> per la specifica classe <xref:System.Windows.Forms.BindingSource> che si sta utilizzando deve essere associato al relativo metodo di gestione degli eventi.  Di seguito viene riportato un esempio di metodo per la gestione dell'evento <xref:System.Windows.Forms.BindingSource.PositionChanged>:  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.NavigatingData#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#3)]  
  
### Per trovare un elemento e impostarlo come elemento corrente  
  
1.  Trovare il record che si desidera impostare come elemento corrente.  A tale scopo, utilizzare il metodo <xref:System.Windows.Forms.BindingSource.Find%2A> della classe <xref:System.Windows.Forms.BindingSource> se l'origine dati implementa l'interfaccia <xref:System.ComponentModel.IBindingList>.  Tra le origini dati di esempio che implementano l'interfaccia <xref:System.ComponentModel.IBindingList> sono annoverate <xref:System.ComponentModel.BindingList%601> e <xref:System.Data.DataView>.  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.NavigatingData#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#2)]  
  
## Vedere anche  
 [Origini dati supportate da Windows Form](../../../docs/framework/winforms/data-sources-supported-by-windows-forms.md)   
 [Notifica delle modifiche nell'associazione dati dei Windows Form](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [Associazione dati e Windows Form](../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)