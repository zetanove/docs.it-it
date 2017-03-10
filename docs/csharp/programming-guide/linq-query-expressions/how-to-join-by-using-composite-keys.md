---
redirect_url: /dotnet/articles/csharp/linq/join-by-using-composite-keys
caps.handback.revision: 8
---
# Procedura: eseguire un join utilizzando una chiave composta (Guida per programmatori C#)
In questo esempio viene illustrato come eseguire operazioni di join in cui si desidera utilizzare più di una chiave per definire una corrispondenza.  Ciò è possibile utilizzando una chiave composta.  Viene creata una chiave composta come tipo anonimo o tipo denominato con i valori che si desidera confrontare.  Se la variabile di query viene passata attraverso i limiti del metodo, utilizzare un tipo denominato che esegue l'override di <xref:System.Object.Equals%2A> e <xref:System.Object.GetHashCode%2A> per la chiave.  I nomi delle proprietà e l'ordine in cui si verificano devono essere identici in ogni chiave.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare una chiave composta per eseguire un join dei dati da tre tabelle:  
  
```  
var query = from o in db.Orders  
    from p in db.Products  
    join d in db.OrderDetails   
        on new {o.OrderID, p.ProductID} equals new {d.OrderID,         d.ProductID} into details  
        from d in details  
        select new {o.OrderID, p.ProductID, d.UnitPrice};  
```  
  
 L'inferenza dei tipi nelle chiavi composte dipende dai nomi delle proprietà nelle chiavi e dall'ordine in cui si verificano.  Se le proprietà nelle sequenze di origine non contengono gli stessi nomi, è necessario assegnare nuovi nomi nelle chiavi.  Ad esempio, se nella tabella `Orders` e nella tabella `OrderDetails` vengono utilizzati nomi diversi per le colonne, è possibile creare chiavi composte assegnando nomi identici nei tipi anonimi:  
  
```  
join...on new {Name = o.CustomerName, ID = o.CustID} equals   
    new {Name = d.CustName, ID = d.CustID }  
```  
  
 Le chiavi composte possono essere utilizzate anche nella clausola `group`.  
  
## Compilazione del codice  
  
-   Per compilare ed eseguire questo codice, seguire questi passaggi:  
  
-   Aprire [Procedura dettagliata: connettersi al database Northwind](../Topic/How%20to:%20Connect%20to%20the%20Northwind%20Database.md) e seguire le istruzioni per configurare il progetto e creare la connessione di database.  Per ulteriori informazioni, vedere [Procedura: installare database di esempio](../Topic/How%20to:%20Install%20Sample%20Databases.md).  
  
-   In samples.cs creare un nuovo metodo vuoto che accetti un parametro di input di Northwind denominato db, simile agli altri metodi presenti nel file.  Incollare il codice indicato in questo esempio nel corpo del metodo.  
  
-   Modificare program.cs in modo da chiamare il nuovo metodo da `Main`.  
  
-   Premere F5 per compilare ed eseguire la query.  
  
## Vedere anche  
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Clausola join](../../../csharp/language-reference/keywords/join-clause.md)   
 [Clausola group](../../../csharp/language-reference/keywords/group-clause.md)