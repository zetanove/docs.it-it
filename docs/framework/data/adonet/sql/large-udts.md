---
title: "Tipi di grandi dimensioni definiti dall&#39;utente | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Tipi di grandi dimensioni definiti dall&#39;utente
I tipi definiti dall'utente \(UDT\) consentono agli sviluppatori di estendere il sistema di tipi scalari del server archiviando oggetti CLR \(Common Language Runtime\) in un database di SQL Server.  I tipi UDT possono contenere più elementi e presentare comportamenti diversi dai tipi di dati alias tradizionali, costituiti da un singolo tipo di dati di sistema SQL Server.  
  
> [!NOTE]
>  Per sfruttare il supporto SqlClient migliorato per i tipi UDT di grandi dimensioni, è necessario installare .NET Framework 3.5 SP1 \(o versione successiva\).  
  
 In precedenza, i tipi UDT avevano una dimensione massima di 8 kilobyte.  In SQL Server 2008 questa limitazione è stata rimossa per i tipi UDT che hanno un formato <xref:Microsoft.SqlServer.Server.Format>.  
  
 Per informazioni complete sui tipi definiti dall'utente, vedere la documentazione online di SQL Server relativa alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
1.  [Tipi CLR definiti dall'utente](http://go.microsoft.com/fwlink/?LinkId=98366)  
  
## Recupero di schemi UDT tramite GetSchema  
 Il metodo <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> di <xref:System.Data.SqlClient.SqlConnection> restituisce informazioni sullo schema del database in un oggetto <xref:System.Data.DataTable>.  Per altre informazioni, vedere [Raccolte di schemi di SQL Server](../../../../../docs/framework/data/adonet/sql-server-schema-collections.md).  
  
### Valori della colonna GetSchemaTable per i tipi UDT  
 Il metodo <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> di <xref:System.Data.SqlClient.SqlDataReader> restituisce un oggetto <xref:System.Data.DataTable> che descrive i metadati della colonna.  La tabella seguente descrive le differenze tra i metadati della colonna per i tipi UDT di grandi dimensioni tra SQL Server 2005 e SQL Server 2008.  
  
|Colonna SqlDataReader|SQL Server 2005|SQL Server 2008 e versioni successive|  
|---------------------------|---------------------|-------------------------------------------|  
|`ColumnSize`|Variabile|Variabile|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|Istanza UDT|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|Istanza UDT|  
|`ProviderType`|21 \(`SqlDbType.VarBinary`\)|29 \(`SqlDbType.Udt`\)|  
|`NonVersionedProviderType`|29 \(`SqlDbType.Udt`\)|29 \(`SqlDbType.Udt`\)|  
|`DataTypeName`|`SqlDbType.VarBinary`|Nome in tre parti specificato come *Database.SchemaName.TypeName*.|  
|`IsLong`|Variabile|Variabile|  
  
## Considerazioni su SqlDataReader  
 <xref:System.Data.SqlClient.SqlDataReader> è stato esteso a partire da SQL Server 2008 per supportare il recupero di valori UDT di grandi dimensioni.  La modalità di elaborazione dei valori UDT di grandi dimensioni da parte di [SqlDataReader](assetId:///SqlDataReader?qualifyHint=False&amp;autoUpgrade=True) dipende dalla versione di SQL Server in uso, nonché dal valore di `Type System Version` specificato nella stringa di connessione.  Per altre informazioni, vedere <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
 I seguenti metodi di <xref:System.Data.SqlClient.SqlDataReader> restituiranno <xref:System.Data.SqlTypes.SqlBinary> anziché un tipo definito dall'utente quando `Type System Version` è impostato su SQL Server 2005:  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  ``  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  ``  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
 I seguenti metodi restituiranno una matrice di `Byte[]` anziché un tipo definito dall'utente quando `Type System Version` è impostato su SQL Server 2005:  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>  ``  
  
-   <xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
 Si noti che per la versione corrente di ADO.NET non vengono eseguite conversioni.  
  
## Impostazione di SqlParameters  
 Le proprietà <xref:System.Data.SqlClient.SqlParameter> seguenti sono state estese per l'uso con i tipi UDT di grandi dimensioni.  
  
|Proprietà SqlParameter|Descrizione|  
|----------------------------|-----------------|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|Ottiene o imposta un oggetto che rappresenta il valore del parametro.  Il valore predefinito è Null.  La proprietà può essere `SqlBinary`, `Byte[]` o un oggetto gestito.|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|Ottiene o imposta un oggetto che rappresenta il valore del parametro.  Il valore predefinito è Null.  La proprietà può essere `SqlBinary`, `Byte[]` o un oggetto gestito.|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|Ottiene o imposta la dimensione del valore del parametro da risolvere.  Il valore predefinito è 0.  La proprietà può essere un integer che rappresenta la dimensione del valore del parametro.  Per i tipi UDT di grandi dimensioni, può trattarsi delle dimensioni effettive del tipo UDT oppure può essere pari a \-1 per i tipi sconosciuti.|  
  
## Esempio di recupero di dati  
 Nel frammento di codice seguente viene illustrato come recuperare i dati UDT di grandi dimensioni.  La variabile `connectionString` presuppone una connessione valida a un database di SQL Server e la variabile `commandString` presuppone un'istruzione SELECT valida con la colonna della chiave primaria elencata per prima.  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
```vb  
Using connection As New SqlConnection( _  
    connectionString, commandString)  
    connection.Open()  
    Dim command As New SqlCommand(commandString, connection)  
    Dim reader As SqlDataReader  
    reader = command.ExecuteReader  
  
    While reader.Read()  
      ' Retrieve the value of the Primary Key column.  
      Dim id As Int32 = reader.GetInt32(0)  
  
      ' Retrieve the value of the UDT.  
      Dim udt As LargeUDT = CType(reader(1), LargeUDT)  
  
     ' You can also use GetSqlValue and GetValue.  
     ' Dim udt As LargeUDT = CType(reader.GetSqlValue(1), LargeUDT)  
     ' Dim udt As LargeUDT = CType(reader.GetValue(1), LargeUDT)  
  
      ' Print values.  
      Console.WriteLine("ID={0} LargeUDT={1}", id, udt)  
    End While  
    reader.Close()  
End Using  
  
```  
  
## Vedere anche  
 [Configurazione dei parametri e tipi di dati dei parametri](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)   
 [Recupero di informazioni sullo schema di database](../../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [Mapping dei tipi di dati SQL Server](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)   
 [Dati binari e con valori di grandi dimensioni SQL Server](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)