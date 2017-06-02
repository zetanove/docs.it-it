---
title: "Enumerazione di istanze di SQL Server (ADO.NET) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# Enumerazione di istanze di SQL Server (ADO.NET)
Con [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] alle applicazioni è consentito trovare istanze di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] all'interno della rete corrente.  Mediante la classe <xref:System.Data.Sql.SqlDataSourceEnumerator> queste informazioni vengono esposte allo sviluppatore dell'applicazione che in tal modo dispone di una <xref:System.Data.DataTable> contenente dati relativi a tutti i server visibili.  Nella tabella restituita è incluso un elenco di istanze di server disponibili in rete che corrisponde all'elenco fornito quando un utente tenta di creare una nuova connessione ed espande l'elenco a discesa contenente tutti i server disponibili nella finestra di dialogo **Proprietà connessione**.  I risultati visualizzati non sono sempre completi.  
  
> [!NOTE]
>  Come nel caso della maggior parte dei servizi Windows, è consigliabile eseguire il servizio Visualizzatore SQL con meno privilegi possibile.  Per altre informazioni sul servizio Visualizzatore SQL e su come gestirne il comportamento, vedere la documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
## Recupero di un'istanza di enumeratore  
 Per recuperare la tabella che contiene le informazioni sulle istanze di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] disponibili, è innanzitutto necessario recuperare un enumeratore usando la proprietà condivisa\/statica <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A>:  
  
```vb  
Dim instance As System.Data.Sql.SqlDataSourceEnumerator = _  
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
 Dopo aver recuperato l'istanza statica, è possibile chiamare il metodo <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A>, che restituisce un tipo <xref:System.Data.DataTable> contenente informazioni sui server disponibili:  
  
```vb  
Dim dataTable As System.Data.DataTable = instance.GetDataSources()  
```  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
 La tabella restituita dalla chiamata al metodo contiene le seguenti colonne, tutte contenenti valori `string`:  
  
|Colonna|Descrizione|  
|-------------|-----------------|  
|**NomeServer**|Nome del server.|  
|**InstanceName**|Nome dell'istanza del server.  Resta vuoto se il server è in esecuzione come istanza predefinita.|  
|**IsClustered**|Indica se il server è parte di un cluster.|  
|**Versione**|Versione del server.  Ad esempio:<br /><br /> -   9.00.x \([!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)]\)<br />-   10.0.xx \([!INCLUDE[ssKatmai](../../../../../includes/sskatmai-md.md)]\)<br />-   10.50.x \([!INCLUDE[ssKilimanjaro](../../../../../includes/sskilimanjaro-md.md)]\)<br />-   11.0.xx \([!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2012\)|  
  
## Limitazioni delle enumerazioni  
 È possibile elencare o non elencare tutti i server disponibili.  L'elenco può variare in base a fattori come i timeout e il traffico di rete.  Pertanto l'elenco può risultare diverso durante due chiamate consecutive.  Verranno elencati solo i server nella stessa rete.  Normalmente i pacchetti di broadcast non passeranno dai router. Per questo motivo è possibile che l'utente non visualizzi un server elencato, ma tale server resterà stabile durante le chiamate.  
  
 Per i server elencati potrebbero essere disponibili anche informazioni aggiuntive quali `IsClustered` e la versione,  a seconda del metodo con cui si è ottenuto l'elenco.  I server elencati tramite il servizio Visualizzatore di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] presenteranno maggiori dettagli rispetto a quelli rilevati tramite l'infrastruttura Windows, che consente di elencare solo i nomi.  
  
> [!NOTE]
>  L'enumerazione di server è disponibile solo in caso di attendibilità totale.  Gli assembly eseguiti in un ambiente di attendibilità parziale non saranno in grado di usare la funzionalità, anche se dispongono dell'autorizzazione CAS \(Code Access Security, Sicurezza dall'accesso di codice\) <xref:System.Data.SqlClient.SqlClientPermission>.  
  
 In [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)], invece, vengono fornite informazioni per <xref:System.Data.Sql.SqlDataSourceEnumerator> tramite l'uso di un servizio Windows esterno denominato Visualizzatore SQL.  Questo servizio è abilitato per impostazione predefinita, ma gli amministratori possono disattivarlo o disabilitarlo per rendere l'istanza del server invisibile a questa classe.  
  
## Esempio  
 L'applicazione console riportata di seguito consente di recuperare informazioni su tutte le istanze di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] visibili e di visualizzarle nella finestra della console.  
  
```vb  
Imports System.Data.Sql  
  
Module Module1  
  Sub Main()  
    ' Retrieve the enumerator instance and then the data.  
    Dim instance As SqlDataSourceEnumerator = _  
     SqlDataSourceEnumerator.Instance  
    Dim table As System.Data.DataTable = instance.GetDataSources()  
  
    ' Display the contents of the table.  
    DisplayData(table)  
  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Sub  
  
  Private Sub DisplayData(ByVal table As DataTable)  
    For Each row As DataRow In table.Rows  
      For Each col As DataColumn In table.Columns  
        Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
      Next  
      Console.WriteLine("============================")  
    Next  
  End Sub  
End Module  
```  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## Vedere anche  
 [SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)