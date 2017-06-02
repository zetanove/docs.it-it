---
title: "Procedura: ordinare e filtrare i dati ADO.NET con il componente BindingSource Windows Form | Microsoft Docs"
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
  - "ADO.NET [Windows Form]"
  - "BindingSource (componente) [Windows Form], ordinamento e applicazione di filtri ai dati"
  - "dati [Windows Form], applicazione di filtri"
  - "dati [Windows Form], ordinamento"
  - "ordinamento dei dati, ADO.NET"
  - "filtro [Windows Form], ADO.NET"
  - "ordinamento dei dati"
ms.assetid: 6c206daf-d706-4602-9dbe-435343052063
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: ordinare e filtrare i dati ADO.NET con il componente BindingSource Windows Form
È possibile esporre la funzionalità di ordinamento e filtraggio del controllo <xref:System.Windows.Forms.BindingSource> mediante le proprietà <xref:System.Windows.Forms.BindingSource.Sort%2A> e <xref:System.Windows.Forms.BindingSource.Filter%2A>.  È possibile applicare l'ordinamento semplice quando l'origine dati sottostante è un'interfaccia <xref:System.ComponentModel.IBindingList> e applicare il filtro e l'ordinamento avanzato quando l'origine dati è un'interfaccia <xref:System.ComponentModel.IBindingListView>.  La proprietà <xref:System.Windows.Forms.BindingSource.Sort%2A> richiede una sintassi [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] standard, ovvero una stringa che rappresenta il nome di una colonna di dati nell'origine dati seguito da `ASC` o `DESC` per indicare se l'ordine dell'elenco deve essere crescente o decrescente.  È possibile impostare un ordinamento avanzato o a più colonne separando ogni colonna con un separatore virgola.  La proprietà <xref:System.Windows.Forms.BindingSource.Filter%2A> accetta un'espressione stringa.  
  
> [!NOTE]
>  L'archiviazione delle informazioni riservate, ad esempio la password, nella stringa di connessione può avere implicazioni sulla sicurezza dell'applicazione.  L'autenticazione di Windows, detta anche sicurezza integrata, consente di controllare l'accesso a un database in modo più sicuro.  Per ulteriori informazioni, vedere [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
### Per filtrare i dati con il BindingSource  
  
-   Impostare la proprietà <xref:System.Windows.Forms.BindingSource.Filter%2A> sull'espressione desiderata.  
  
     Nell'esempio di codice riportato di seguito l'espressione è un nome di colonna seguito dal valore desiderato per la colonna.  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#11)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#11)]  
  
### Per ordinare i dati con il BindingSource  
  
1.  Impostare la proprietà <xref:System.Windows.Forms.BindingSource.Sort%2A> sul nome di colonna desiderato seguito da `ASC` o `DESC` per indicare l'ordine crescente o decrescente.  
  
2.  Separare le colonne multiple con una virgola.  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#12)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#12)]  
  
## Esempio  
 Nell'esempio di codice riportato di seguito vengono caricati i dati della tabella Customers del database di esempio Northwind in un controllo <xref:System.Windows.Forms.DataGridView> e quindi vengono filtrati e ordinati i dati visualizzati.  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#1)]  
  
## Compilazione del codice  
 Per eseguire l'esempio, incollare il codice in un form contenente un <xref:System.Windows.Forms.BindingSource> denominato `BindingSource1` e un <xref:System.Windows.Forms.DataGridView> denominato `dataGridView1`.  Gestire l'evento <xref:System.Windows.Forms.Form.Load> per il form e chiamare `InitializeSortedFilteredBindingSource` nel metodo per la gestione eventi Load.  
  
## Vedere anche  
 <xref:System.Windows.Forms.BindingSource.Sort%2A>   
 <xref:System.Windows.Forms.BindingSource.Filter%2A>   
 [Procedura: installare database di esempio](../Topic/How%20to:%20Install%20Sample%20Databases.md)   
 [Il componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component.md)