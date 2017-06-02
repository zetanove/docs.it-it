---
title: "REF CURSOR Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# REF CURSOR Oracle
Il provider di dati .NET Framework per Oracle supporta il tipo di dati **REF CURSOR** Oracle.  Quando si usa il provider di dati per usare il tipo di dati REF CURSOR Oracle, considerare i seguenti comportamenti.  
  
> [!NOTE]
>  Alcuni comportamenti si differenziano da quelli del provider Microsoft OLE DB per Oracle \(MSDAORA\).  
  
-   Per motivi di prestazioni, il provider di dati per Oracle non associa automaticamente il tipo di dati **REF CURSOR**, come MSDAORA, a meno che non vengano specificati in modo esplicito.  
  
-   Il provider di dati non supporta alcuna sequenza di escape ODBC, incluso il carattere di escape {resultset} usato per specificare i parametri REF CURSOR.  
  
-   Per eseguire una stored procedure che restituisce un tipo di dati REF CURSOR, è necessario definire i parametri nel tipo <xref:System.Data.OracleClient.OracleParameterCollection> con un tipo <xref:System.Data.OracleClient.OracleType> di **Cursor** e un tipo <xref:System.Data.OracleClient.OracleParameter.Direction%2A> di **Output**.  Il provider di dati supporta l'associazione dei REF CURSOR solo come parametri di output.  I REF CURSOR come parametri di input non sono supportati.  
  
-   Il recupero di un tipo <xref:System.Data.OracleClient.OracleDataReader> dal valore del parametro non è supportato.  I valori sono di tipo <xref:System.DBNull> dopo l'esecuzione del comando.  
  
-   L'unico valore di enumerazione di **CommandBehavior** utilizzabile con il tipo di dati REF CURSOR, ad esempio quando si chiama il metodo <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>, è **CloseConnection**. Tutti gli altri vengono ignorati.  
  
-   L'ordine dei REF CURSOR in **OracleDataReader** dipende dall'ordine dei parametri in **OracleParameterCollection**.  La proprietà <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A> viene ignorata.  
  
-   Il tipo di dati PL\/SQL **TABLE** non è supportato.  I REF CURSOR, tuttavia, sono più efficaci.  Se è necessario usare un tipo di dati **TABLE**, usare il provider di dati OLE DB .NET con MSDAORA.  
  
## In questa sezione  
 [Esempi di REF CURSOR](../../../../docs/framework/data/adonet/ref-cursor-examples.md)  
 Vengono presentati tre esempi che illustrano l'uso del tipo di dati REF CURSOR.  
  
 [Parametri REF CURSOR in OracleDataReader](../../../../docs/framework/data/adonet/ref-cursor-parameters-in-an-oracledatareader.md)  
 Viene illustrato come eseguire una stored procedure PL\/SQL che restituisce un parametro REF CURSOR e legge il valore come **OracleDataReader**.  
  
 [Recupero di dati da più REF CURSOR mediante un OracleDataReader](../../../../docs/framework/data/adonet/retrieving-data-from-multiple-ref-cursors.md)  
 Viene illustrato come eseguire una stored procedure PL\/SQL che restituisce due parametri REF CURSOR e legge i valori come **OracleDataReader**.  
  
 [Compilazione di un dataset mediante uno o più oggetti REF CURSOR](../../../../docs/framework/data/adonet/filling-a-dataset-using-one-or-more-ref-cursors.md)  
 Viene illustrato come eseguire una stored procedure PL\/SQL che restituisce due parametri REF CURSOR e la compilazione di un tipo <xref:System.Data.DataSet> con le righe restituite.  
  
## Vedere anche  
 [Oracle e ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)