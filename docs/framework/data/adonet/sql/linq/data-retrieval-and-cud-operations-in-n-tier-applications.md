---
title: "Recupero dei dati e operazioni CUD in applicazioni a pi&#249; livelli (LINQ to SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3133d53-83ed-4a4d-af8b-82edcf3831db
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Recupero dei dati e operazioni CUD in applicazioni a pi&#249; livelli (LINQ to SQL)
Quando si serializzano oggetti entità, ad esempio Customers o Orders, in un client di una rete, tali entità vengono disconnesse dal relativo contesto dati.  Il contesto dati non rileva più le modifiche o le associazioni con gli altri oggetti,  il che non rappresenta un problema se i client leggono solo i dati.  È inoltre relativamente semplice consentire ai client di aggiungere nuove righe in un database.  Tuttavia, se l'applicazione richiede che i client siano in grado di aggiornare o eliminare i dati, sarà necessario associare le entità a un nuovo contesto dati prima di chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=fullName>.  Inoltre, se si usa un controllo della concorrenza ottimistica con i valori originali, sarà necessario anche un modo per fornire al database l'entità originale e l'entità come modificata.  I metodi `Attach` vengono forniti per consentire l'inserimento delle entità in un nuovo contesto dati dopo essere stati disconnessi.  
  
 Anche se si serializzano gli oggetti proxy anziché le entità [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], sarà comunque necessario costruire un'entità nel livello di accesso ai dati \(DAL\) e associarla a un nuovo oggetto <xref:System.Data.Linq.DataContext?displayProperty=fullName>, in modo da inviare i dati al database.  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non è importante il modo in cui le entità vengono serializzate.  Per altre informazioni sull'utilizzo della [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] e degli strumenti SQLMetal per generare le classi serializzabili mediante Windows Communication Foundation \(WCF\), vedere [Procedura: creare entità serializzabili](../../../../../../docs/framework/data/adonet/sql/linq/how-to-make-entities-serializable.md).  
  
> [!NOTE]
>  Chiamare i metodi `Attach` solo sulle entità nuove o deserializzate.  L'unico modo per disconnettere un'entità dal contesto dati originali è serializzarla.  Se si tenta di associare un'entità disconnessa a un nuovo contesto dati e tale entità dispone ancora di caricatori posticipati dal contesto dati precedente, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] verrà generata un'eccezione.  Un'entità con caricatori posticipati da due contesti dati diversi può causare risultati imprevisti quando si eseguono le operazioni di inserimento, aggiornamento ed eliminazione su tale entità.  Per altre informazioni sui caricatori posticipati, vedere [Caricamento rinviato e immediato](../../../../../../docs/framework/data/adonet/sql/linq/deferred-versus-immediate-loading.md).  
  
## Recupero dei dati  
  
### Chiamata al metodo client  
 Negli esempi seguenti viene illustrata una chiamata al metodo di esempio nel DAL da un client Windows Form.  In questo esempio il DAL viene implementato come libreria dei servizi Windows:  
  
```vb  
Private Function GetProdsByCat_Click(ByVal sender As Object, ByVal e _  
    As EventArgs)  
  
    ' Create the WCF client proxy.  
    Dim proxy As New NorthwindServiceReference.Service1Client  
  
    ' Call the method on the service.  
    Dim products As NorthwindServiceReference.Product() = _  
        proxy.GetProductsByCategory(1)  
  
    ' If the database uses original values for concurrency checks,  
    ' the client needs to store them and pass them back to the  
    ' middle tier along with the new values when updating data.  
  
    For Each v As NorthwindClient1.NorthwindServiceReference.Product _  
        In products  
        ' Persist to a List(Of Product) declared at class scope.  
        ' Additional change-tracking logic is the responsibility  
        ' of the presentation tier and/or middle tier.  
        originalProducts.Add(v)  
    Next  
  
    ' (Not shown) Bind the products list to a control  
    ' and/or perform whatever processing is necessary.  
End Function  
```  
  
```csharp  
private void GetProdsByCat_Click(object sender, EventArgs e)  
{  
    // Create the WCF client proxy.  
    NorthwindServiceReference.Service1Client proxy =   
    new NorthwindClient.NorthwindServiceReference.Service1Client();  
  
    // Call the method on the service.  
    NorthwindServiceReference.Product[] products =   
    proxy.GetProductsByCategory(1);  
  
    // If the database uses original values for concurrency checks,   
    // the client needs to store them and pass them back to the   
    // middle tier along with the new values when updating data.  
    foreach (var v in products)  
    {  
        // Persist to a list<Product> declared at class scope.  
        // Additional change-tracking logic is the responsibility  
        // of the presentation tier and/or middle tier.  
        originalProducts.Add(v);  
    }  
  
    // (Not shown) Bind the products list to a control  
    // and/or perform whatever processing is necessary.  
    }  
```  
  
### Implementazione del livello intermedio  
 Nell'esempio seguente viene illustrata un'implementazione del metodo di interfaccia nel livello intermedio.  Di seguito sono riportati i due punti principali da tenere presente:  
  
-   L'oggetto <xref:System.Data.Linq.DataContext> viene dichiarato nell'ambito del metodo.  
  
-   Il metodo restituisce una raccolta <xref:System.Collections.IEnumerable> dei risultati effettivi.  Il serializzatore eseguirà la query per restituire i risultati a livello di client\/presentazione.  Per accedere localmente ai risultati della query nel livello intermedio, è possibile forzare l'esecuzione chiamando `ToList` o `ToArray` sulla variabile della query.  È quindi possibile restituire tale elenco o matrice come oggetto `IEnumerable`.  
  
```vb  
Public Function GetProductsByCategory(ByVal categoryID As Integer) _  
    As IEnumerable(Of Product)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    Dim productQuery = _  
    From prod In db.Products _  
    Where prod.CategoryID = categoryID _  
    Select prod  
  
    Return productQuery.AsEnumerable()  
  
End Function  
```  
  
```csharp  
public IEnumerable<Product> GetProductsByCategory(int categoryID)  
{  
    NorthwindClasses1DataContext db =   
    new NorthwindClasses1DataContext(connectionString);  
  
    IEnumerable<Product> productQuery =  
    from prod in db.Products  
    where prod.CategoryID == categoryID  
    select prod;  
  
    return productQuery.AsEnumerable();   
}  
```  
  
 Un'istanza di un contesto dati deve avere una durata di una "unità di lavoro." In un ambiente a regime di controllo libero \("loosely\-coupled"\) un'unità di lavoro è tipicamente piccola, forse una transazione ottimistica, inclusa una singola chiamata a `SubmitChanges`.  Pertanto, il contesto dati viene creato ed eliminato nell'ambito del metodo.  Se l'unità di lavoro include chiamate alla logica delle regole business, è preferibile in genere mantenere l'istanza `DataContext` per l'intera operazione.  In ogni caso, le istanze `DataContext` non devono essere conservate per lunghi periodi di tempo con un numero arbitrario di transazioni.  
  
 Questo metodo restituirà oggetti Product ma non la raccolta di oggetti Order\_Detail associati a ogni oggetto Product.  Usare l'oggetto <xref:System.Data.Linq.DataLoadOptions> per modificare questo comportamento predefinito.  Per altre informazioni, vedere [Procedura: controllare la quantità di dati correlati da recuperare](../../../../../../docs/framework/data/adonet/sql/linq/how-to-control-how-much-related-data-is-retrieved.md).  
  
## Inserimento di dati  
 Per inserire un nuovo oggetto, il livello di presentazione chiama il metodo desiderato sull'interfaccia del livello intermedio e passa il nuovo oggetto da inserire.  In alcuni casi, può essere più efficiente per il client passare solo alcuni valori e far costruire al livello intermedio l'oggetto completo.  
  
### Implementazione del livello intermedio  
 Nel livello intermedio viene creato un nuovo oggetto <xref:System.Data.Linq.DataContext>, l'oggetto viene associato all'oggetto <xref:System.Data.Linq.DataContext> usando il metodo <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> e l'oggetto viene inserito quando viene chiamato il metodo <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  Le eccezioni, i callback e le condizioni di errore possono essere gestiti analogamente a qualsiasi altro scenario del servizio Web.  
  
```vb  
' No call to Attach is necessary for inserts.  
Public Sub InsertOrder(ByVal o As Order)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    db.Orders.InsertOnSubmit(o)  
  
    ' Exception handling not shown.  
    db.SubmitChanges()  
  
End Sub  
```  
  
```csharp  
// No call to Attach is necessary for inserts.  
    public void InsertOrder(Order o)  
    {  
        NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
        db.Orders.InsertOnSubmit(o);  
  
        // Exception handling not shown.  
        db.SubmitChanges();  
    }  
```  
  
## Eliminazione di dati  
 Per eliminare un oggetto esistente dal database, il livello di presentazione chiama il metodo desiderato sull'interfaccia del livello intermedio e passa la copia che include i valori originali dell'oggetto da eliminare.  
  
 Le operazioni di eliminazione implicano i controlli di concorrenza ottimistica e l'oggetto da eliminare deve prima essere associato al nuovo contesto dati.  In questo esempio il parametro `Boolean` è impostato su `false` per indicare che l'oggetto non ha un timestamp \(RowVersion\).  Se la tabella di database genera timestamp per ogni record, i controlli di concorrenza sono molto più semplici, sopratutto per il client.  È necessario solo passare l'oggetto originale o modificato e impostare il parametro `Boolean` su `true`.  In ogni caso, nel livello intermedio è in genere necessario rilevare l'eccezione <xref:System.Data.Linq.ChangeConflictException>.  Per altre informazioni su come gestire i conflitti di concorrenza ottimistica, vedere [Cenni preliminari sulla concorrenza ottimistica](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md).  
  
 Quando si eliminano le entità che hanno vincoli di chiave esterna nelle tabelle associate, è necessario prima eliminare tutti gli oggetti nelle raccolte <xref:System.Data.Linq.EntitySet%601>.  
  
```vb  
' Attach is necessary for deletes.  
Public Sub DeleteOrder(ByVal order As Order)  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
  
    db.Orders.Attach(order, False)  
    ' This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order)  
  
    Try  
        ' ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict)  
  
    Catch ex As ChangeConflictException  
        ' Get conflict information, and take actions  
        ' that are appropriate for your application.  
        ' See MSDN Article "How to: Manage Change  
        ' Conflicts (LINQ to SQL).  
  
    End Try  
End Sub  
```  
  
```csharp  
// Attach is necessary for deletes.  
public void DeleteOrder(Order order)  
{  
    NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
  
    db.Orders.Attach(order, false);  
    // This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order);  
    try  
    {  
        // ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict);  
    }  
    catch (ChangeConflictException e)  
    {  
       // Get conflict information, and take actions  
       // that are appropriate for your application.  
       // See MSDN Article How to: Manage Change Conflicts (LINQ to SQL).  
    }  
}  
```  
  
## Aggiornamento di dati  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sono supportati gli aggiornamenti di questi scenari relativi alla concorrenza ottimistica:  
  
-   Concorrenza ottimistica basata sui timestamp o i numeri RowVersion.  
  
-   Concorrenza ottimistica basata sui valori originali di un subset di proprietà dell'entità.  
  
-   Concorrenza ottimistica basata sulle entità complete originali o modificate.  
  
 È inoltre possibile eseguire aggiornamenti o eliminazioni su un'entità con le relative relazioni, ad esempio un oggetto Customer e una raccolta degli oggetti Order associati.  Quando nel client si effettuano modifiche a un grafico di oggetti entità e alle relative raccolte figlio \(`EntitySet`\) e i controlli di concorrenza ottimistica richiedono i valori originali, il client deve fornire tali valori originali per ogni entità e oggetto <xref:System.Data.Linq.EntitySet%601>.  Per consentire ai client di effettuare un set di aggiornamenti, eliminazioni e inserimenti correlati in una sola chiamata al metodo, è necessario fornire al client un modo per indicare il tipo di operazione da eseguire su ogni entità.  Nel livello intermedio chiamare quindi il metodo <xref:System.Data.Linq.ITable.Attach%2A> adatto e quindi <xref:System.Data.Linq.ITable.InsertOnSubmit%2A>, <xref:System.Data.Linq.ITable.DeleteAllOnSubmit%2A> o <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> \(senza `Attach` per gli inserimenti\) per ogni entità prima di chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  Non recuperare i dati dal database per ottenere i valori originali prima dell'esecuzione degli aggiornamenti.  
  
 Per altre informazioni sulla concorrenza ottimistica, vedere [Cenni preliminari sulla concorrenza ottimistica](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md).  Per informazioni dettagliate su come risolvere i conflitti di modifiche di concorrenza ottimistica, vedere [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md).  
  
 Negli esempi seguenti vengono illustrati tutti gli scenari:  
  
### Concorrenza ottimistica con timestamp  
  
```vb  
' Assume that "customer" has been sent by client.  
' Attach with "true" to say this is a modified entity  
' and it can be checked for optimistic concurrency  
' because it has a column that is marked with the  
' "RowVersion" attribute.  
  
db.Customers.Attach(customer, True)  
  
Try  
    ' Optional: Specify a ConflictMode value  
    ' in call to SubmitChanges.  
    db.SubmitChanges()  
Catch ex As ChangeConflictException  
    ' Handle conflict based on options provided.  
    ' See MSDN article "How to: Manage Change  
    ' Conflicts (LINQ to SQL)".  
End Try  
```  
  
```csharp  
// Assume that "customer" has been sent by client.  
// Attach with "true" to say this is a modified entity  
// and it can be checked for optimistic concurrency because  
//  it has a column that is marked with "RowVersion" attribute  
db.Customers.Attach(customer, true)  
try  
{  
    // Optional: Specify a ConflictMode value  
    // in call to SubmitChanges.  
    db.SubmitChanges();  
}  
catch(ChangeConflictException e)  
{  
    // Handle conflict based on options provided  
    // See MSDN article How to: Manage Change Conflicts (LINQ to SQL).  
}  
```  
  
### Con un subset di valori originali  
 In questo approccio il client restituisce l'oggetto serializzato completo, insieme ai valori da modificare.  
  
```vb  
Public Sub UpdateProductInventory(ByVal p As Product, ByVal _  
    unitsInStock As Short?, ByVal unitsOnOrder As Short?)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        ' p is the original unmodified product  
        ' that was obtained from the database.  
        ' The client kept a copy and returns it now.  
        db.Products.Attach(p, False)  
  
        ' Now that the original values are in the data context,  
        ' apply the changes.  
        p.UnitsInStock = unitsInStock  
        p.UnitsOnOrder = unitsOnOrder  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle conflict based on options provided.  
            ' See MSDN article "How to: Manage Change Conflicts  
            ' (LINQ to SQL)".  
        End Try  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInventory(Product p, short? unitsInStock, short? unitsOnOrder)  
{  
    using (NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString))  
    {  
        // p is the original unmodified product  
        // that was obtained from the database.  
        // The client kept a copy and returns it now.  
        db.Products.Attach(p, false);  
  
        // Now that the original values are in the data context, apply the changes.  
        p.UnitsInStock = unitsInStock;  
        p.UnitsOnOrder = unitsOnOrder;  
        try  
        {  
             // Optional: Specify a ConflictMode value  
             // in call to SubmitChanges.  
             db.SubmitChanges();  
        }  
        catch (ChangeConflictException e)  
        {  
            // Handle conflict based on provided options.  
            // See MSDN article How to: Manage Change Conflicts  
            // (LINQ to SQL).  
        }  
    }  
}  
```  
  
### Con entità complete  
  
```vb  
Public Sub UpdateProductInfo(ByVal newProd As Product, ByVal _  
    originalProd As Product)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        db.Products.Attach(newProd, originalProd)  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle potential change conflicgt in whatever way  
            ' is appropriate for your application.  
            ' For more information, see the MSDN article  
            ' "How to: Manage Change Conflicts (LINQ to  
            ' SQL)".  
        End Try  
  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInfo(Product newProd, Product originalProd)  
{  
     using (NorthwindClasses1DataContext db = new  
        NorthwindClasses1DataContext(connectionString))  
     {  
         db.Products.Attach(newProd, originalProd);  
         try  
         {  
               // Optional: Specify a ConflictMode value  
               // in call to SubmitChanges.  
               db.SubmitChanges();  
         }  
        catch (ChangeConflictException e)  
        {  
            // Handle potential change conflict in whatever way  
            // is appropriate for your application.  
            // For more information, see the MSDN article  
            // How to: Manage Change Conflicts (LINQ to SQL)/  
        }   
    }  
}  
```  
  
 Per aggiornare una raccolta, chiamare <xref:System.Data.Linq.ITable.AttachAll%2A> anziché `Attach`.  
  
### Membri dell'entità previsti  
 Come indicato in precedenza, è necessario impostare solo alcuni membri dell'oggetto entità prima di chiamare i metodi `Attach`.  I membri dell'entità da impostare devono soddisfare i criteri seguenti:  
  
-   Devono essere parte dell'identità dell'entità.  
  
-   Devono poter essere modificati.  
  
-   Devono essere un timestamp o avere l'attributo <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> impostato su un valore diverso da `Never`.  
  
 Se una tabella usa un timestamp o un numero di versione per un controllo della concorrenza ottimistica, è necessario impostare tali membri prima di chiamare <xref:System.Data.Linq.ITable.Attach%2A>.  Un membro è dedicato al controllo della concorrenza ottimistica quando la proprietà <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> è impostata su true nell'attributo Column.  Tutti gli aggiornamenti necessari vengono inviati solo se i valori del numero di versione o del timestamp sono gli stessi di quelli presenti nel database.  
  
 Un membro viene usato anche nel controllo della concorrenza ottimistica purché la proprietà del membro <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> non sia impostata su `Never`.  Il valore predefinito è `Always` se non viene specificato un altro valore.  
  
 Se uno di questi membri necessari risulta mancante, viene generata un'eccezione <xref:System.Data.Linq.ChangeConflictException> durante l'operazione <xref:System.Data.Linq.DataContext.SubmitChanges%2A> \("Riga non trovata o modificata"\).  
  
### Stato  
 Dopo aver associato un oggetto entità all'istanza <xref:System.Data.Linq.DataContext>, lo stato dell'oggetto diventa `PossiblyModified`.  Sono disponibili tre modalità per forzare un oggetto associato in modo da essere considerato `Modified`.  
  
1.  Associarlo come non modificato e quindi modificare direttamente i campi.  
  
2.  Associarlo con l'overload <xref:System.Data.Linq.Table%601.Attach%2A> che accetta le istanze dell'oggetto originale e corrente.  In questo modo alla funzionalità di ricerca delle modifiche vengono forniti i valori vecchi e nuovi per rilevare automaticamente i campi modificati.  
  
3.  Associarlo con l'overload <xref:System.Data.Linq.Table%601.Attach%2A> che accetta un secondo parametro booleano \(impostato su true\).  In questo modo la funzionalità di ricerca delle modifiche considererà l'oggetto modificato senza dover richiedere i valori originali.  In questo approccio l'oggetto deve avere un campo di versione\/timestamp.  
  
 Per altre informazioni, vedere [Stati degli oggetti e rilevamento delle modifiche](../../../../../../docs/framework/data/adonet/sql/linq/object-states-and-change-tracking.md).  
  
 Se un oggetto entità è già presente nella Cache ID con la stessa identità dell'oggetto associato, viene generata un'eccezione <xref:System.Data.Linq.DuplicateKeyException>.  
  
 Quando si associa un set di oggetti `IEnumerable`, viene generata un'eccezione <xref:System.Data.Linq.DuplicateKeyException> se è presente una chiave già esistente.  Gli oggetti rimanenti non verranno associati.  
  
## Vedere anche  
 [Applicazioni a più livelli e remote con LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)   
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)