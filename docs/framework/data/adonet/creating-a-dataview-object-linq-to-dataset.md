---
title: "Creazione di un oggetto DataView (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 76057508-e12d-4779-a707-06a4c2568acf
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Creazione di un oggetto DataView (LINQ to DataSet)
Per creare un oggetto <xref:System.Data.DataView> nel contesto [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], sono disponibili due modalità.  È possibile creare un oggetto <xref:System.Data.DataView> da una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] su <xref:System.Data.DataTable> oppure da un oggetto <xref:System.Data.DataTable> tipizzato o non tipizzato.  In entrambi i casi, l'oggetto <xref:System.Data.DataView> viene creato usando uno dei metodi di estensione<xref:System.Data.DataTableExtensions.AsDataView%2A>; non è possibile costruire <xref:System.Data.DataView> direttamente nel contesto  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  
  
 Dopo aver creato <xref:System.Data.DataView>, è possibile associarlo a un controllo dell'interfaccia utente in un'applicazione Windows Form o ASP.NET oppure modificare le impostazioni di filtro e ordinamento.  
  
 <xref:System.Data.DataView> costruisce un indice, offrendo un significativo incremento delle prestazioni nel caso di operazioni in cui è possibile usare l'indice, ad esempio ordinamento e filtro.  L'indice relativo a un oggetto <xref:System.Data.DataView> viene compilato sia quando si crea <xref:System.Data.DataView> che quando si modifica una qualsiasi delle informazioni relative all'ordinamento o al filtraggio.  Se si crea un oggetto <xref:System.Data.DataView> e quindi si impostano le impostazioni sull'ordinamento o il filtraggio in un secondo momento, l'indice verrà compilato almeno due volte, ovvero una volta durante la creazione di <xref:System.Data.DataView> e una seconda volta quando viene modificata una qualsiasi delle proprietà di ordinamento o filtro.  
  
 Per altre informazioni sul filtro e l'ordinamento con <xref:System.Data.DataView>, vedere [Filtro con DataView](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md) e [Ordinamento con DataView](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md).  
  
## Creazione di una DataView da una query LINQ to DataSet  
 Un oggetto <xref:System.Data.DataView> può essere creato dai risultati di una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], in cui i risultati sono una proiezione di oggetti <xref:System.Data.DataRow>.  Il nuovo oggetto <xref:System.Data.DataView> eredita le informazioni di filtro e ordinamento della query da cui è stato creato.  
  
> [!NOTE]
>  Nella maggior parte dei casi le espressioni usate per il filtro e l'ordinamento non devono presentare effetti collaterali e devono essere deterministiche.  Le espressioni non devono inoltre contenere eventuale codice che dipende da un numero impostato di esecuzioni perché è possibile che le operazioni di ordinamento e filtro vengano eseguite un numero qualsiasi di volte.  
  
 La creazione di <xref:System.Data.DataView> da una query che restituisce tipi anonimi o da query che eseguono operazioni join non è supportata.  
  
 In una query usata per creare <xref:System.Data.DataView> sono supportati solo i seguenti operatori di query:  
  
-   <xref:System.Data.EnumerableRowCollectionExtensions.Cast%2A>  
  
-   <xref:System.Data.EnumerableRowCollectionExtensions.OrderBy%2A>  
  
-   <xref:System.Data.EnumerableRowCollectionExtensions.OrderByDescending%2A>  
  
-   <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A>  
  
-   <xref:System.Data.EnumerableRowCollectionExtensions.ThenBy%2A>  
  
-   <xref:System.Data.EnumerableRowCollectionExtensions.ThenByDescending%2A>  
  
-   <xref:System.Data.EnumerableRowCollectionExtensions.Where%2A>  
  
 Si noti che quando viene creato un oggetto <xref:System.Data.DataView> da una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], il metodo <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A> deve essere il metodo finale chiamato nella query, come illustrato nell'esempio seguente, in cui viene creato un oggetto <xref:System.Data.DataView> di ordini online ordinati in base al totale dovuto:  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquery1)]
 [!code-vb[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquery1)]  
  
 È inoltre possibile usare le proprietà basate su stringa <xref:System.Data.DataView.RowFilter%2A> e <xref:System.Data.DataView.Sort%2A> per filtrare e ordinare un oggetto <xref:System.Data.DataView> creato da una query.  Si noti che in questo caso le informazioni di ordinamento e di filtro ereditate dalla query verranno cancellate.  Nell'esempio seguente viene creato un oggetto <xref:System.Data.DataView> da una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] che filtra i contatti in base ai cognomi che iniziano con 'S'.  La proprietà <xref:System.Data.DataView.Sort%2A> basata su stringa è impostata per ordinare i cognomi in ordine crescente e quindi i nomi in ordine decrescente:  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## Creazione di una DataView da una DataTable  
 Oltre che da una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], un oggetto <xref:System.Data.DataView> può essere creato da <xref:System.Data.DataTable> usando il metodo <xref:System.Data.DataTableExtensions.AsDataView%2A>.  
  
 Nell'esempio seguente viene creato un oggetto <xref:System.Data.DataView> dalla tabella SalesOrderDetail e viene impostato come origine dati di un oggetto <xref:System.Windows.Forms.BindingSource>.  L'oggetto funge da proxy per un controllo <xref:System.Windows.Forms.DataGridView>.  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromtable)]
 [!code-vb[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromtable)]  
  
 Dopo la creazione dell'oggetto <xref:System.Data.DataView> da <xref:System.Data.DataTable>, è possibile specificare le impostazioni di filtro e ordinamento.  Nell'esempio seguente viene creato un oggetto <xref:System.Data.DataView> dalla tabella Contact e la proprietà <xref:System.Data.DataView.Sort%2A> viene impostata in modo da ordinare i cognomi in ordine crescente e quindi i nomi in ordine decrescente:  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
 Se tuttavia la proprietà <xref:System.Data.DataView.RowFilter%2A> o <xref:System.Data.DataView.Sort%2A> viene impostata dopo la creazione di <xref:System.Data.DataView> da una query, si verifica un decremento delle prestazioni perché <xref:System.Data.DataView> costruisce un indice per supportare le operazioni di filtro e ordinamento.  L'impostazione della proprietà <xref:System.Data.DataView.RowFilter%2A> o <xref:System.Data.DataView.Sort%2A> provoca una ricompilazione dell'indice dei dati, aggiungendo un sovraccarico all'applicazione e riducendo le prestazioni.  Se possibile, è preferibile specificare le impostazioni di filtro e ordinamento la prima volta che viene creato l'oggetto <xref:System.Data.DataView> ed evitare di modificarle in seguito.  
  
## Vedere anche  
 [Associazione dati e LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)   
 [Filtro con DataView](../../../../docs/framework/data/adonet/filtering-with-dataview-linq-to-dataset.md)   
 [Ordinamento con DataView](../../../../docs/framework/data/adonet/sorting-with-dataview-linq-to-dataset.md)