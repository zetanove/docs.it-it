---
title: "Considerazioni su LINQ (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, LINQ"
  - "esecuzione di query sul servizio dati [WCF Data Services]"
  - "WCF Data Services, l'esecuzione di query"
ms.assetid: cc4ec9e9-348f-42a6-a78e-1cd40e370656
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Considerazioni su LINQ (WCF Data Services)
In questo argomento vengono fornite informazioni sulla modalità con cui le query LINQ vengono composte ed eseguite quando si usa il client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] e sulle limitazioni dell'utilizzo di LINQ per eseguire una query su un servizio dati che implementa [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]creazione e l'esecuzione di query su un [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]-basato su servizio dati, vedere [query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
## <a name="composing-linq-queries"></a>Composizione di query LINQ  
 LINQ consente di comporre query per una raccolta di oggetti che implementa <xref:System.Collections.Generic.IEnumerable%601>. Entrambi i **Aggiungi riferimento al servizio** nella finestra di dialogo [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] e lo strumento DataSvcUtil.exe vengono utilizzati per generare la rappresentazione di un [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] servizio come classe contenitore di entità che eredita da <xref:System.Data.Services.Client.DataServiceContext>, nonché gli oggetti che rappresentano le entità restituite nei feed. Questi strumenti generano anche le proprietà per la classe contenitore di entità delle raccolte esposte come feed dal servizio. Ognuna di queste proprietà della classe che incapsula il servizio dati restituisce un <xref:System.Data.Services.Client.DataServiceQuery%601>. Poiché il <xref:System.Data.Services.Client.DataServiceQuery%601> implementa il <xref:System.Linq.IQueryable%601> interfaccia definita da LINQ, è possibile comporre una query LINQ per i feed esposti dal servizio dati che vengono convertiti dalla libreria client in una richiesta di query URI che viene inviato al servizio dati in esecuzione.  
  
> [!IMPORTANT]
>  La sintassi LINQ consente di esprimere un set di query più ampio di quello consentito dalla sintassi URI usata dai servizi dati [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]. Oggetto <xref:System.NotSupportedException> viene generato quando la query non può essere mappata a un URI nel servizio dati di destinazione. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]il [metodi LINQ non supportati](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md#unsupportedMethods) in questo argomento.  
  
 Nell'esempio seguente viene riportata una query LINQ che restituisce `Orders` con un costo di spedizione maggiore di&30; dollari e ordina i risultati in base alla data di spedizione, partendo da quella più recente:  
  
  [Astoria NorthwindClient #AddQueryOptionsLinqSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#AddQueryOptionsLinqSpecific)]  
  
 Questa query LINQ viene convertita nella query seguente URI che viene eseguita su basato su Northwind [Guida introduttiva](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md) servizio dati:  
  
```  
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30  
```  
  
 Per ulteriori informazioni generali su LINQ, vedere [LINQ (Language-Integrated Query)](../Topic/LINQ%20\(Language-Integrated%20Query\).md).  
  
 LINQ consente di comporre query tramite la sintassi di query dichiarativa specifica della lingua, mostrata nell'esempio precedente, e un set di metodi di query noti come operatori di query standard. Una query equivalente a quella dell'esempio precedente può essere composta solo tramite la sintassi basata sul metodo, come indicato nell'esempio seguente:  
  
  [Astoria NorthwindClient #AddQueryOptionsLinqExpressionSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#AddQueryOptionsLinqExpressionSpecific)]  
  
 Il client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è in grado di convertire entrambi tipi di query composte in un URI di query ed è possibile estendere una query LINQ aggiungendo i metodi di query a un'espressione di query. Quando si compongono query LINQ aggiungendo la sintassi del metodo a un'espressione di query o un <xref:System.Data.Services.Client.DataServiceQuery%601>, le operazioni vengono aggiunte all'URI della query nell'ordine in cui vengono chiamati. Questo è equivalente alla chiamata di <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> per aggiungere ogni opzione di query all'URI della query.  
  
## <a name="executing-linq-queries"></a>Esecuzione di query LINQ  
 LINQ determinati metodi di query, ad esempio <xref:System.Linq.Enumerable.First%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29> o <xref:System.Linq.Enumerable.Single%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>, quando aggiunto alla query, la query da eseguire. Una query viene eseguita anche quando i risultati vengono enumerati in modo implicito, ad esempio durante un ciclo `foreach` o quando la query è assegnata a una raccolta `List`. Per ulteriori informazioni, vedere [query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
 Il client esegue una query LINQ in due parti. Ogni qualvolta possibile, le espressioni LINQ di una query vengono prima valutate sul client e quindi viene generata una query basata sull'URI che viene inviata al servizio dati per la valutazione rispetto ai dati del servizio. Per ulteriori informazioni, vedere la sezione [Server esecuzione del Client e](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md#executingQueries) in [query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
 Quando non è possibile convertire una query LINQ in un URI di query conforme a [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)], viene generata un'eccezione quando viene tentata l'esecuzione. Per ulteriori informazioni, vedere [query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
## <a name="linq-query-examples"></a>Esempi di query LINQ  
 Negli esempi delle sezioni seguenti vengono illustrati i tipi di query LINQ che possono essere eseguiti su un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)].  
  
<a name="filtering"></a>   
### <a name="filtering"></a>Filtro  
 Negli esempi di query LINQ in questa sezione vengono filtrati i dati nel feed restituito dal servizio.  
  
 Negli esempi seguenti vengono illustrate query equivalenti che filtrano le entità `Orders` restituite in modo che vengano restituiti solo gli ordini con un costo di spedizione maggiore di $30:  
  
-   Utilizzo della sintassi di query LINQ:  
  
      [Astoria NorthwindClient #LinqWhereClauseSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqWhereClauseSpecific)]  
  
-   Utilizzo dei metodi di query LINQ:  
  
      [Astoria NorthwindClient #LinqWhereMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqWhereMethodSpecific)]  
  
-   Opzione `$filter` della stringa di query:  
  
      [Astoria NorthwindClient #ExplicitQueryWhereMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#ExplicitQueryWhereMethodSpecific)]  
  
 Tutti gli esempi precedenti vengono convertiti nell'URI di query: `http://localhost:12345/northwind.svc/Orders()?$filter=Freight gt 30M`.  
  
<a name="sorting"></a>   
### <a name="sorting"></a>Ordinamento  
 Negli esempi seguenti vengono illustrate query equivalenti che ordinano i dati restituiti in base al nome dell'azienda e al codice postale, in ordine decrescente:  
  
-   Utilizzo della sintassi di query LINQ:  
  
      [Astoria NorthwindClient #LinqOrderByClauseSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqOrderByClauseSpecific)]  
  
-   Utilizzo dei metodi di query LINQ:  
  
      [Astoria NorthwindClient #LinqOrderByMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqOrderByMethodSpecific)]  
  
-   Opzione `$orderby` della stringa di query:  
  
      [Astoria NorthwindClient #ExplicitQueryOrderByMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#ExplicitQueryOrderByMethodSpecific)]  
  
 Tutti gli esempi precedenti vengono convertiti nell'URI di query: `http://localhost:12345/northwind.svc/Customers()?$orderby=CompanyName,PostalCode desc`.  
  
<a name="projection"></a>   
### <a name="projection"></a>Proiezione  
 Negli esempi seguenti vengono illustrate query equivalenti che ordinano i dati restituiti dal progetto nel tipo `CustomerAddress` più ristretto:  
  
-   Utilizzo della sintassi di query LINQ:  
  
      [Astoria NorthwindClient #LinqSelectClauseSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqSelectClauseSpecific)]  
  
-   Utilizzo dei metodi di query LINQ:  
  
      [Astoria NorthwindClient #LinqSelectMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqSelectMethodSpecific)]  
  
> [!NOTE]
>  Il `$select` opzione query non può essere aggiunta a un URI di query tramite il <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> metodo. Si consiglia di utilizzare LINQ <xref:System.Linq.Enumerable.Select%2A> metodo per generare il client di `$select` opzione nell'URI della richiesta di query.\</TSource, TResult>  
  
 Entrambi gli esempi precedenti vengono convertiti nell'URI di query: `"http://localhost:12345/northwind.svc/Customers()?$filter=Country eq 'GerGerm'&$select=CustomerID,Address,City,Region,PostalCode,Country"`.  
  
<a name="paging"></a>   
### <a name="client-paging"></a>Paging del client  
 Negli esempi seguenti vengono illustrate query equivalenti che richiedono una pagina delle entità ordinate che include 25 ordini, ignorando i primi 50 ordini:  
  
-   Applicazione di metodi di query a una query LINQ:  
  
      [Astoria NorthwindClient #LinqSkipTakeMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqSkipTakeMethodSpecific)]  
  
-   Opzioni `$skip` e `$top` della stringa di query dell'URI:  
  
      [Astoria NorthwindClient #ExplicitQuerySkipTakeMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#ExplicitQuerySkipTakeMethodSpecific)]  
  
 Entrambi gli esempi precedenti vengono convertiti nell'URI di query: `http://localhost:12345/northwind.svc/Orders()?$orderby=OrderDate desc&$skip=50&$top=25`.  
  
<a name="expand"></a>   
### <a name="expand"></a>Espandi  
 Quando si esegue una query su un servizio dati [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)], è possibile richiedere che le entità relative all'entità di destinazione della query siano incluse nel feed restituito. Il <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> metodo viene chiamato sul <xref:System.Data.Services.Client.DataServiceQuery%601> per il set di entità indirizzato dalla query LINQ, con l'entità correlata impostare nome fornito come il `path` parametro. Per ulteriori informazioni, vedere [il caricamento di contenuto posticipato](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md).  
  
 Gli esempi seguenti illustrano modi equivalenti per usare il <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A> metodo in una query:  
  
-   Nella sintassi della query LINQ:  
  
      [Astoria NorthwindClient #LinqQueryExpandSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqQueryExpandSpecific)]  
  
-   Con i metodi di query LINQ:  
  
      [Astoria NorthwindClient #LinqQueryExpandMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqQueryExpandMethodSpecific)]  
  
 Entrambi gli esempi precedenti vengono convertiti nell'URI di query: `http://localhost:12345/northwind.svc/Orders()?$filter=CustomerID eq 'ALFKI'&$expand=Order_Details`.  
  
<a name="unsupportedMethods"></a>   
## <a name="unsupported-linq-methods"></a>Metodi LINQ non supportati  
 Nella tabella seguente sono riportate le classi dei metodi LINQ non supportati che non possono essere incluse in una query eseguita su un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]:  
  
|Tipo di operazione|Metodo non supportato|  
|--------------------|------------------------|  
|Operatori Set|Tutti gli operatori set non sono supportati con un <xref:System.Data.Services.Client.DataServiceQuery%601>, che include quanto segue:<br /><br /> -   <xref:System.Linq.Enumerable.All%2A><br />-   <xref:System.Linq.Enumerable.Any%2A><br />-   <xref:System.Linq.Enumerable.Concat%2A><br />-   <xref:System.Linq.Enumerable.DefaultIfEmpty%2A><br />-   <xref:System.Linq.Enumerable.Distinct%2A><br />-   <xref:System.Linq.Enumerable.Except%2A><br />-   <xref:System.Linq.Enumerable.Intersect%2A><br />-   <xref:System.Linq.Enumerable.Union%2A><br />-   <xref:System.Linq.Enumerable.Zip%2A>\</TFirst, TSecond, TResult>|  
|Operatori di ordinamento|Gli operatori di ordinamento seguenti che richiedono <xref:System.Collections.Generic.IComparer%601> non sono supportati con un <xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> </TSource, TKey> </TSource, TKey><br />-   <xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> \</TSource, TKey> \</TSource, TKey><br />-   <xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> </TSource, TKey> </TSource, TKey><br />-   <xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> \</TSource, TKey> \</TSource, TKey>|  
|Operatori di proiezione e di filtro|I seguenti operatori di proiezione e filtro che accettano un argomento posizionale non sono supportati con un <xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%2CSystem.Collections.Generic.IEqualityComparer%7B%60%602%7D%29> </TOuter, TInner, TResult> </TInner, TKey> </TOuter, TKey> </TOuter, TInner, TKey, TResult><br />-   <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2C%60%601%7D%29> </TSource, Int32, TResult> </TSource, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29> </TSource, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29> </TSource, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29> \</TSource, TCollection, TResult> \</TSource, TCollection, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29> </TSource, TCollection, TResult> </TSource, TCollection, TResult><br />-   <xref:System.Linq.Enumerable.Where%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Boolean%7D%29> \</TSource, Int32, Boolean>|  
|Operatori di raggruppamento|Tutti gli operatori di raggruppamento non sono supportati con un <xref:System.Data.Services.Client.DataServiceQuery%601>, inclusi i seguenti:<br /><br /> -   <xref:System.Linq.Enumerable.GroupBy%2A>\</TSource, TKey><br />-   <xref:System.Linq.Enumerable.GroupJoin%2A>\</TOuter, TInner, TKey, TResult><br /><br /> È necessario eseguire le operazioni di raggruppamento sul client.|  
|Operatori di aggregazione|Tutte le operazioni di aggregazione non sono supportate con un <xref:System.Data.Services.Client.DataServiceQuery%601>, inclusi i seguenti:<br /><br /> -   <xref:System.Linq.Enumerable.Aggregate%2A><br />-   <xref:System.Linq.Enumerable.Average%2A><br />-   <xref:System.Linq.Enumerable.Count%2A><br />-   <xref:System.Linq.Enumerable.LongCount%2A><br />-   <xref:System.Linq.Enumerable.Max%2A><br />-   <xref:System.Linq.Enumerable.Min%2A><br />-   <xref:System.Linq.Enumerable.Sum%2A><br /><br /> Le operazioni di aggregazione devono essere eseguite sul client o devono essere incapsulate da un'operazione del servizio.|  
|Operatori di paging|Gli operatori di paging seguenti non sono supportati con un <xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.ElementAt%2A><br />-   <xref:System.Linq.Enumerable.Last%2A><br />-   <xref:System.Linq.Enumerable.LastOrDefault%2A><br />-   <xref:System.Linq.Enumerable.SkipWhile%2A><br />-   <xref:System.Linq.Enumerable.TakeWhile%2A> **Nota:** operatori di spostamento che vengono eseguiti in una sequenza vuota restituiscono null.|  
|Altri operatori|Le operazioni seguenti non sono supportati altri operatori con un <xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> 1.  <xref:System.Linq.Enumerable.Empty%2A><br />2.  <xref:System.Linq.Enumerable.Range%2A><br />3.  <xref:System.Linq.Enumerable.Repeat%2A><br />4.  <xref:System.Linq.Enumerable.ToDictionary%2A></TSource, TKey><br />5.  <xref:System.Linq.Enumerable.ToLookup%2A>\</TSource, TKey>|  
  
<a name="supportedExpressions"></a>   
## <a name="supported-expression-functions"></a>Funzioni di espressione non supportate  
 Le proprietà e i metodi Common Language Runtime (CLR) riportati di seguito sono supportati perché possono essere convertiti in un'espressione di query per l'inclusione nell'URI della richiesta a un servizio [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]:  
  
|<xref:System.String> membro|Funzione [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supportata|  
|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.String.Concat%28System.String%2CSystem.String%29>|`string concat(string p0, string p1)`|  
|<xref:System.String.Contains%28System.String%29>|`bool substringof(string p0, string p1)`|  
|<xref:System.String.EndsWith%28System.String%29>|`bool endswith(string p0, string p1)`|  
|<xref:System.String.IndexOf%28System.String%2CSystem.Int32%29>|`int indexof(string p0, string p1)`|  
|<xref:System.String.Length>|`int length(string p0)`|  
|<xref:System.String.Replace%28System.String%2CSystem.String%29>|`string replace(string p0, string find, string replace)`|  
|<xref:System.String.Substring%28System.Int32%29>|`string substring(string p0, int pos)`|  
|<xref:System.String.Substring%28System.Int32%2CSystem.Int32%29>|`string substring(string p0, int pos, int length)`|  
|<xref:System.String.ToLower>|`string tolower(string p0)`|  
|<xref:System.String.ToUpper>|`string toupper(string p0)`|  
|<xref:System.String.Trim>|`string trim(string p0)`|  
  
|<xref:System.DateTime> membro<sup>1</sup>|Funzione [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supportata|  
|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.DateTime.Day>|`int day(DateTime p0)`|  
|<xref:System.DateTime.Hour>|`int hour(DateTime p0)`|  
|<xref:System.DateTime.Minute>|`int minute(DateTime p0)`|  
|<xref:System.DateTime.Month>|`int month(DateTime p0)`|  
|<xref:System.DateTime.Second>|`int second(DateTime p0)`|  
|<xref:System.DateTime.Year>|`int year(DateTime p0)`|  
  
 <sup>1</sup>l'equivalente proprietà data e ora di <xref:Microsoft.VisualBasic.DateAndTime?displayProperty=fullName>, così come il <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> metodo in Visual Basic sono inoltre supportati.  
  
|<xref:System.Math> membro|Funzione [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supportata|  
|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Math.Ceiling%28System.Decimal%29>|`decimal ceiling(decimal p0)`|  
|<xref:System.Math.Ceiling%28System.Double%29>|`double ceiling(double p0)`|  
|<xref:System.Math.Floor%28System.Decimal%29>|`decimal floor(decimal p0)`|  
|<xref:System.Math.Floor%28System.Double%29>|`double floor(double p0)`|  
|<xref:System.Math.Round%28System.Decimal%29>|`decimal round(decimal p0)`|  
|<xref:System.Math.Round%28System.Double%29>|`double round(double p0)`|  
  
|<xref:> System.Linq.Expressions.Expression?qualifyHint=False&autoUpgrade=True membro|Funzione [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] supportata|  
|---------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Linq.Expressions.Expression.TypeIs%28System.Linq.Expressions.Expression%2CSystem.Type%29>|`bool isof(type p0)`|  
  
 È possibile che il client sia anche in grado di valutare funzioni CLR aggiuntive sul client. Oggetto <xref:System.NotSupportedException> viene generato per qualsiasi espressione che non può essere valutata sul client e non può essere convertito in un URI di richiesta valido per la valutazione sul server.  
  
## <a name="see-also"></a>Vedere anche  
 [Query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)   
 [Proiezioni di query](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md)   
 [Materializzazione degli oggetti](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)   
 [OData: Convenzioni URI](http://go.microsoft.com/fwlink/?LinkID=185564)