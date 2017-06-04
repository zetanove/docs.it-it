---
title: "Gestione di valori null | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Gestione di valori null
Un valore null in un database relazionale viene usato quando il valore in una colonna è sconosciuto o mancante.  Un valore null non è né una stringa vuota \(per tipi di dati carattere o data\-ora\) né un valore zero \(per tipi di dati numerici\).  Nella specifica ANSI SQL\-92 si afferma che un valore null deve essere uguale per tutti i tipi di dati, in modo da gestire coerentemente tutti i valori null.  Lo spazio dei nomi <xref:System.Data.SqlTypes> offre una semantica di tipo null tramite l'implementazione dell'interfaccia <xref:System.Data.SqlTypes.INullable>.  Ciascun tipo di dati nello spazio dei nomi <xref:System.Data.SqlTypes> dispone di una proprietà `IsNull` e di un valore `Null` che può essere assegnato a un'istanza di quel tipo di dati.  
  
> [!NOTE]
>  In .NET Framework versione 2.0 è stato introdotto il supporto per i tipi nullable, che consentono ai programmatori di estendere un tipo di valore in modo da rappresentare tutti i valori del tipo sottostante.  I tipi nullable di CLR rappresentano un'istanza della struttura <xref:System.Nullable>.  Questa funzionalità risulta particolarmente utile quando i tipi di valore sono boxed e unboxed e garantisce una maggior compatibilità con i tipi di oggetto.  I tipi nullable di CLR non devono essere usati per l'archiviazione di valori null di database perché il comportamento di un valore null SQL ANSI è diverso da quello di un riferimento a `null` \(o `Nothing` in Visual Basic\).  Per gestire valori null SQL ANSI di database, usare valori null di <xref:System.Data.SqlTypes> anziché <xref:System.Nullable>.  Per altre informazioni sull'uso di tipi nullable CLR in Visual Basic, vedere [Nullable Value Types](../Topic/Nullable%20Value%20Types%20\(Visual%20Basic\).md), mentre per C\# vedere [Utilizzo dei tipi nullable](../Topic/Using%20Nullable%20Types%20\(C%23%20Programming%20Guide\).md).  
  
## Valori null e logica con tre valori  
 La concessione di valori null nelle definizioni di colonna introduce una logica con tre valori nell'applicazione.  Un confronto può restituire una delle tre condizioni indicate di seguito:  
  
-   True  
  
-   False  
  
-   Sconosciuto  
  
 Poiché il valore null è considerato come sconosciuto, due valori null confrontati tra loro non vengono considerati uguali.  In espressioni che usano operatori aritmetici, se uno degli operandi è un valore null, anche il risultato sarà null.  
  
## Valori null e SqlBoolean  
 Un confronto tra qualsiasi spazio dei nomi <xref:System.Data.SqlTypes> restituirà un tipo <xref:System.Data.SqlTypes.SqlBoolean>.  La funzione `IsNull` per ogni `SqlType` restituisce un tipo <xref:System.Data.SqlTypes.SqlBoolean> e può essere usata per controllare eventuali valori null.  Nelle seguenti tabelle reali viene mostrato come funzionano gli operatori AND, OR e NOT in presenza di un valore null.  \(T\=true, F\=false e U\=sconosciuto \[unknown\] o null.\)  
  
 ![Tabella Truth](../../../../../docs/framework/data/adonet/sql/media/truthtable-bpuedev11.png "TruthTable\_bpuedev11")  
  
### Nozioni di base sull'opzione ANSI\_NULLS  
 Lo spazio dei nomi <xref:System.Data.SqlTypes> offre la stessa semantica dell'opzione ANSI\_NULLS quando è attivata in SQL Server.  Tutti gli operatori aritmetici \(\+, \-, \*, \/, %\), gli operatori bit per bit \(~, &, &#124;\) e la maggior parte delle funzioni restituiscono Null se uno degli operandi o degli argomenti è Null, ad eccezione della proprietà `IsNull`.  
  
 Lo standard ANSI SQL\-92 non supporta *columnName* \= NULL in una clausola WHERE.  In SQL Server l'opzione ANSI\_NULLS consente di controllare sia i valori null predefiniti nel database sia la valutazione dei confronti rispetto a valori null.  Se l'opzione ANSI\_NULLS è attivata \(impostazione predefinita\), è necessario usare l'operatore IS NULL nelle espressioni quando si verifica la presenza di valori null.  Ad esempio, il confronto che segue restituisce sempre Sconosciuto quando l'opzione ANSI\_NULLS è attiva:  
  
```  
  
colname > NULL  
```  
  
 Anche il confronto con una variabile che contiene un valore null restituisce Sconosciuto:  
  
```  
  
colname > @MyVariable  
```  
  
 Usare il predicato IS NULL o IS NOT NULL per verificare la presenza di un valore null.  In tal modo si può rendere più complessa la clausola WHERE.  Ad esempio, la colonna TerritoryID nella tabella Customer di AdventureWorks consente valori null.  Se con un'istruzione SELECT si intende verificare la presenza di valori in aggiunta ad altri valori, è necessario che l'istruzione includa un predicato IS NULL:  
  
```  
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
 Se si disattiva l'opzione ANSI\_NULLS in SQL Server, è possibile creare espressioni che usano l'operatore di uguaglianza per eseguire confronti con valori null.  Tuttavia, non è possibile impedire che altre connessioni impostino opzioni null per tale connessione.  L'uso di IS NULL per verificare la presenza di valori null funziona sempre, indipendentemente dall'impostazione dell'opzione ANSI\_NULLS per una connessione.  
  
 La disattivazione dell'opzione ANSI\_NULLS non è supportata in un tipo `DataSet`, che segue sempre lo standard ANSI SQL\-92 per la gestione di valori null nello spazio dei nomi<xref:System.Data.SqlTypes>.  
  
## Assegnazione di valori null  
 I valori null sono speciali e la loro semantica di archiviazione e assegnazione differisce nei diversi sistemi di tipi e di archiviazioni.  Un tipo `Dataset` è progettato per essere usato con diversi sistemi di tipi e di archiviazioni.  
  
 Questa sezione descrive la semantica del valore null per assegnare valori null a un tipo <xref:System.Data.DataColumn> in un tipo <xref:System.Data.DataRow> nei diversi sistemi di tipi.  
  
 `DBNull.Value`  
 Questa assegnazione è valida per un oggetto `DataColumn` di qualunque tipo.  Se il tipo implementa `INullable`, `DBNull.Value` viene convertito nel valore null fortemente tipizzato appropriato.  
  
 `SqlType.Null`  
 Tutti i tipi di dati <xref:System.Data.SqlTypes> implementano `INullable`.  Se è possibile convertire il valore null fortemente tipizzato nel tipo di dati della colonna usando operatori di cast impliciti, l'assegnazione verrà eseguita.  In caso contrario, viene generata un'eccezione di cast non valido.  
  
 `null`  
 Se "null" è un valore valido per il tipo di dati `DataColumn` specificato, viene convertito nel valore `DbNull.Value` o `Null` appropriato associato al tipo `INullable` \(`SqlType.Null`\).  
  
 `derivedUdt.Null`  
 Per le colonne UDT i valori null sono sempre archiviati in base al tipo associato al `DataColumn`.  Si prenda in considerazione il caso di una colonna UDT associata a un `DataColumn` che non implementa `INullable` mentre lo fa la relativa sottoclasse.  In questo caso, se viene associato alla classe derivata, un valore null fortemente tipizzato viene archiviato come `DbNull.Value` non tipizzato, perché l'archiviazione di valori null è sempre coerente con il tipo di dati di DataColumn.  
  
> [!NOTE]
>  Attualmente la struttura `Nullable<T>` o <xref:System.Nullable> non è supportata nel `DataSet`.  
  
### Assegnazione di più colonne \(riga\)  
 Per `DataTable.Add`, `DataTable.LoadDataRow` o altre API che accettano una proprietà <xref:System.Data.DataRow.ItemArray%2A> di cui viene eseguito il mapping a una riga, viene associato "null" al valore predefinito di DataColumn.  Se un oggetto nella matrice contiene `DbNull.Value` oppure la controparte fortemente tipizzata, si applicano le stesse regole descritte in precedenza.  
  
 Per un'istanza di assegnazioni di valori null di `DataRow.["columnName"]` si applicano inoltre le regole seguenti:  
  
1.  Il valore predefinito di *default* è `DbNull.Value` per tutte le colonne ad eccezione di quelle null fortemente tipizzate, alle quali si applica il valore null fortemente tipizzato appropriato.  
  
2.  I valori null non vengono mai scritti durante la serializzazione in file XML \(come in "xsi:nil"\).  
  
3.  Tutti i valori non null, inclusi i valori predefiniti, vengono sempre scritti durante la serializzazione in file XML.  Questo caso differisce dalla semantica XSD\/XML, dove un valore null \(xsi:nil\) è esplicito e il valore predefinito è implicito \(se non è presente in XML, un parser di convalida lo può recuperare da uno schema XSD associato\).  Per un oggetto `DataTable` vale il concetto opposto: un valore null è implicito e il valore predefinito è esplicito.  
  
4.  A tutti i valori di colonna mancanti per le righe lette dall'input XML viene assegnato il valore NULL.  Alle righe create usando il metodo <xref:System.Data.DataTable.NewRow%2A> o metodi simili viene assegnato il valore predefinito di DataColumn.  
  
5.  Il metodo <xref:System.Data.DataRow.IsNull%2A> restituisce `true` sia per `DbNull.Value` che per `INullable.Null`.  
  
## Assegnazione di valori null  
 Il valore predefinito per qualsiasi istanza <xref:System.Data.SqlTypes> è null.  
  
 I valori null nell'istanza <xref:System.Data.SqlTypes> sono specifici dei tipi e non è possibile rappresentarli con un unico valore, quale `DbNull`.  Usare la proprietà `IsNull` per controllare la presenza di valori null.  
  
 È possibile assegnare valori null a un tipo <xref:System.Data.DataColumn>, come mostrato nel seguente esempio di codice.  È possibile assegnare direttamente valori null a variabili `SqlTypes` senza generare un'eccezione.  
  
### Esempio  
 Nell'esempio di codice seguente viene creato un tipo <xref:System.Data.DataTable> con due colonne definite <xref:System.Data.SqlTypes.SqlInt32> e <xref:System.Data.SqlTypes.SqlString>.  Il codice consente di aggiungere una riga di valori noti e una riga di valori, quindi di scorrere la <xref:System.Data.DataTable>, assegnando i valori alle variabili e visualizzando l'output nella finestra della console.  
  
 [!code-csharp[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/VB/source.vb#1)]  
  
 In questo esempio vengono visualizzati i seguenti risultati:  
  
```  
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## Confronto di valori null con SqlTypes e tipi CLR  
 Quando si confrontano valori null, è importante comprendere la differenza tra il modo in cui il metodo `Equals` valuta i valori null nello spazio dei nomi <xref:System.Data.SqlTypes> rispetto al modo in cui funziona con i tipi CLR.  Tutti i metodi `Equals` di <xref:System.Data.SqlTypes> usano la semantica del database per valutare valori null: se uno o entrambi i valori sono null, il confronto restituisce null.  D'altra parte, se si usa il metodo CLR `Equals` su due spazi dei nomi <xref:System.Data.SqlTypes>, verrà restituito true se entrambi gli spazi dei nomi sono null.  Questo riflette la differenza tra l'uso di un metodo di istanza come il metodo CLR `String.Equals` e l'uso del metodo statico\/condiviso `SqlString.Equals`.  
  
 Nell'esempio seguente viene illustrata la differenza di risultato tra il metodo `SqlString.Equals` e il metodo `String.Equals` quando a ciascuno vengono passate una coppia di valori null e successivamente una coppia di stringhe vuote.  
  
 [!code-csharp[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/VB/source.vb#1)]  
  
 L'output del codice è il seguente:  
  
```  
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## Vedere anche  
 [Tipi di dati SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)