---
title: "Problemi noti in SqlClient per Entity Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 48fe4912-4d0f-46b6-be96-3a42c54780f6
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Problemi noti in SqlClient per Entity Framework
Questa sezione descrive i problemi noti relativi al provider di dati .NET Framework per SQL Server.  
  
## Spazi finali nelle funzioni di stringa  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] ignora gli spazi finali nei valori stringa.  Il passaggio degli spazi finali nella stringa può pertanto generare risultati imprevedibili e persino errori.  
  
 Se sono necessari spazi finali nella stringa, è consigliabile aggiungere uno spazio vuoto alla fine per evitare che [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] tagli la stringa.  Se gli spazi finali non sono richiesti, devono essere tagliati prima di essere passati alla pipeline della query.  
  
## Funzione RIGHT  
 Se viene passato un valore non `null` come primo argomento e 0 come secondo argomento a `RIGHT(nvarchar(max)`, 0`)` o `RIGHT(varchar(max)`, 0`)`, verrà restituito un valore `NULL` anziché una stringa `empty`.  
  
## Operatori CROSS e OUTER APPLY  
 Gli operatori CROSS e OUTER APPLY sono stati introdotti in [!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)].  In alcuni casi, è possibile che la pipeline della query produca un'istruzione Transact\-SQL contenente gli operatori CROSS APPLY e\/o OUTER APPLY.  Poiché tali operatori non sono supportati da alcuni provider di back\-end, incluse le versioni di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)], non è consentita l'esecuzione di query con tali provider.  
  
 Gli elementi seguenti rappresentano alcuni scenari tipici che potrebbero produrre operatori CROSS APPLY e\/o OUTER APPLY nella query di output:  
  
-   Una subquery correlata con paging.  
  
-   Un oggetto `AnyElement` su una sottoquery correlata o su una raccolta prodotta dalla navigazione.  
  
-   Query LINQ che usano metodi di raggruppamento che accettano un selettore elemento.  
  
-   Una query in cui è specificato in modo esplicito un operatore CROSS APPLY o OUTER APPLY.  
  
-   Una query che presenta un costrutto DEREF su un costrutto REF.  
  
## Operatore SKIP  
 Se si usa [!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)], l'uso di SKIP con ORDER BY su colonne non chiave potrebbe restituire risultati non corretti.  Se la colonna non chiave include dati duplicati, potrebbe venire ignorato un numero di righe maggiore di quello specificato.  Questo comportamento è dovuto alla modalità di conversione di SKIP per [!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)].  Nella query seguente potrebbero ad esempio essere ignorate più di cinque righe se `E.NonKeyColumn` include valori duplicati:  
  
```  
SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L  
```  
  
## Utilizzo della versione di SQL Server corretta  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] usa la query [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] basata sulla versione di SQL Server specificata nell'attributo `ProviderManifestToken` dell'elemento Schema nel file del modello di archiviazione \(.ssdl\).  Tale versione potrebbe differire dalla versione effettiva di SQL Server a cui si è connessi.  Se, ad esempio, si usa SQL Server 2005, ma l'attributo `ProviderManifestToken` è impostato su 2008, la query [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] generata potrebbe non essere eseguita nel server. Una query che usa ad esempio i nuovi tipi datetime introdotti in SQL Server 2008 non verrà eseguita nelle versioni precedenti di SQL Server.  Se si usa SQL Server 2005, ma l'attributo `ProviderManifestToken` è impostato su 2000, la query [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] generata potrebbe essere meno ottimizzata o potrebbe essere visualizzata un'eccezione che indica che la query non è supportata.  Per altre informazioni, vedere la sezione relativa agli operatori CROSS e OUTER APPLY riportata prima in questo argomento.  
  
 Determinati comportamenti del database dipendono dal livello di compatibilità impostato per il database.  Se l'attributo `ProviderManifestToken` è impostato su 2005 e si usa la versione 2005 di SQL Server, ma il livello di compatibilità di un database è impostato su "80" \(SQL Server 2000\), il codice [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] generato avrà come destinazione SQL Server 2005, ma potrebbe non essere eseguito nel modo previsto a causa dell'impostazione del livello di compatibilità.  Se, ad esempio, un nome di colonna nell'elenco ORDER BY corrisponde a un nome di colonna nel selettore, può verificarsi la perdita delle informazioni sugli ordini.  
  
## Query annidate nella proiezione  
 Le query annidate in una clausola di proiezione potrebbero essere tradotte in query di un prodotto cartesiano sul server.  Su alcuni server di back\-end, tra cui Server SLQ, questo può provocare l'aumento delle dimensioni della tabella TempDB,  con una conseguente riduzione della prestazione del server.  
  
 Di seguito è riportato un esempio di query annidata in una clausola di proiezione:  
  
```  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## Valori Identity GUID generati dal server  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] supporta valori di identità del tipo GUID generati dal server, ma il provider deve supportare la restituzione del valore di identità generato dal server dopo l'inserimento di una riga.  A partire da [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2005, è possibile restituire il tipo GUID generato dal server in un database [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] tramite la [clausola OUTPUT](http://go.microsoft.com/fwlink/?LinkId=169400.)  
  
## Vedere anche  
 [SqlClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-the-entity-framework.md)   
 [Problemi noti e considerazioni relativi a LINQ to Entities](../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)