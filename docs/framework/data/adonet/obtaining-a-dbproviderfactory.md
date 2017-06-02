---
title: "Recupero di un oggetto DbProviderFactory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a16e4a4d-6a5b-45db-8635-19570e4572ae
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Recupero di un oggetto DbProviderFactory
Il processo di recupero di un oggetto <xref:System.Data.Common.DbProviderFactory> implica il passaggio delle informazioni su un provider di dati alla classe <xref:System.Data.Common.DbProviderFactories>.  Sulla base di queste informazioni, il metodo <xref:System.Data.Common.DbProviderFactories.GetFactory%2A> crea una factory del provider fortemente tipizzata.  Ad esempio, per creare un oggetto <xref:System.Data.SqlClient.SqlClientFactory>, è possibile passare a `GetFactory` una stringa contenente il nome del provider specificato come "System.Data.SqlClient".  L'altro overload di `GetFactory` accetta un oggetto <xref:System.Data.DataRow>.  Dopo aver creato la factory del provider, è quindi possibile usarne i metodi per creare altri oggetti.  I metodi di un oggetto `SqlClientFactory` includono <xref:System.Data.SqlClient.SqlClientFactory.CreateConnection%2A>, <xref:System.Data.SqlClient.SqlClientFactory.CreateCommand%2A>e <xref:System.Data.SqlClient.SqlClientFactory.CreateDataAdapter%2A>.  
  
> [!NOTE]
>  Anche le classi <xref:System.Data.OracleClient.OracleClientFactory>, <xref:System.Data.Odbc.OdbcFactory> e <xref:System.Data.OleDb.OleDbFactory> di .NET Framework forniscono funzionalità analoghe.  
  
## Registrazione in DbProviderFactories  
 Ogni provider di dati .NET Framework che supporta una classe basata su factory registra le informazioni di configurazione nella sezione **DbProviderFactories** del file **machine.config** del computer locale.  Nel frammento di file di configurazione seguente sono illustrati la sintassi e il formato di <xref:System.Data.SqlClient>.  
  
```  
<system.data>  
  <DbProviderFactories>  
    <add name="SqlClient Data Provider"  
     invariant="System.Data.SqlClient"   
     description=".Net Framework Data Provider for SqlServer"   
     type="System.Data.SqlClient.SqlClientFactory, System.Data,   
     Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
    />  
  </DbProviderFactories>  
</system.data>  
```  
  
 L'attributo **invariant** identifica il provider di dati sottostante.  La sintassi di denominazione in tre parti viene inoltre usata durante la creazione di una nuova factory e per l'identificazione del provider in un file di configurazione dell'applicazione in modo da consentire il recupero del nome del provider, unitamente alla stringa di connessione associata, in fase di esecuzione.  
  
## Recupero di informazioni sul provider  
 È possibile recuperare informazioni su tutti i provider di dati installati nel computer locale usando il metodo <xref:System.Data.Common.DbProviderFactories.GetFactoryClasses%2A>.  Tale metodo restituisce un oggetto <xref:System.Data.DataTable> denominato **DbProviderFactories** che contiene le colonne descritte nella tabella seguente.  
  
|Ordinale colonna|Nome colonna|Output esempio|Descrizione|  
|----------------------|------------------|--------------------|-----------------|  
|0|**Nome**|Provider di dati SqlClient|Nome leggibile del provider di dati|  
|1|**Descrizione**|Provider di dati .NET Framework per SQL Server|Descrizione leggibile del provider di dati|  
|2|**InvariantName**|`System.Data.SqlClient`|Nome da usare a livello di codice per fare riferimento al provider di dati|  
|3|**AssemblyQualifiedName**|System.Data.SqlClient.SqlClientFactory, System.Data, Version\=2.0.0.0, Culture\=neutral, PublicKeyToken\=b77a5c561934e089|Nome completo della classe factory, che contiene informazioni sufficienti per creare un'istanza dell'oggetto|  
  
 È possibile usare un oggetto `DataTable` per consentire a un utente di selezionare un oggetto <xref:System.Data.DataRow> in fase di esecuzione.  È quindi possibile passare l'oggetto `DataRow` selezionato al metodo <xref:System.Data.Common.DbProviderFactories.GetFactory%2A> per creare un oggetto <xref:System.Data.Common.DbProviderFactory> fortemente tipizzato.  È possibile passare un oggetto <xref:System.Data.DataRow> selezionato al metodo `GetFactory` per creare l'oggetto `DbProviderFactory` desiderato.  
  
## Visualizzazione dell'elenco delle classi del factory di provider installate  
 In questo esempio viene illustrato l'uso del metodo <xref:System.Data.Common.DbProviderFactories.GetFactoryClasses%2A> per restituire un oggetto <xref:System.Data.DataTable> che contiene informazioni sui provider installati.  Il codice consente di scorrere le singole righe dell'oggetto `DataTable`, visualizzando le informazioni su ogni provider installato nella finestra della console.  
  
 [!code-csharp[DataWorks DbProviderFactories#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories/VB/source.vb#1)]  
  
## Utilizzo dei file di configurazione dell'archiviazione per archiviare le informazioni sulla factory  
 Il modello di progettazione usato per la gestione delle factory prevede l'archiviazione delle informazioni relative al provider e alla stringa di connessione in un file di configurazione dell'applicazione, ad esempio **app.config** per un'applicazione Windows e **web.config** per un'applicazione ASP.NET.  
  
 Nel frammento del file di configurazione seguente viene illustrato come salvare due stringhe di connessione denominate rispettivamente "NorthwindSQL" per una connessione al database Northwind in SQL Server e "NorthwindAccess" per una connessione al database Northwind in Access\/Jet.  Per l'attributo **providerName** viene usato il nome **invariant**.  
  
```  
<configuration>  
  <connectionStrings>  
    <clear/>  
    <add name="NorthwindSQL"   
     providerName="System.Data.SqlClient"   
     connectionString=  
     "Data Source=MSSQL1;Initial Catalog=Northwind;Integrated Security=true"  
    />  
  
    <add name="NorthwindAccess"   
     providerName="System.Data.OleDb"   
     connectionString=  
     "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Data\Northwind.mdb;"  
    />  
  </connectionStrings>  
</configuration>  
```  
  
### Recupero di una stringa di connessione dal nome del provider  
 Per creare una factory del provider, è necessario fornire una stringa di connessione oltre al nome del provider.  In questo esempio viene illustrato come recuperare una stringa di connessione da un file di configurazione dell'applicazione passando il nome del provider nel formato invariant "*System.Data.ProviderName*".  Il codice consente di scorrere gli elementi di <xref:System.Configuration.ConnectionStringSettingsCollection>.  In caso di esito positivo, restituisce <xref:System.Configuration.ConnectionStringSettings.ProviderName%2A>; in caso contrario, restituisce `null` \(`Nothing` in Visual Basic\).  Se per un provider sono disponibili più stringhe, viene restituita la prima stringa trovata.  Per altre informazioni e per esempi relativi al recupero delle stringhe di connessione dai file di configurazione, vedere [Stringhe di connessione e file di configurazione](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md).  
  
> [!NOTE]
>  Per consentire l'esecuzione del codice, è necessario un riferimento a `System.Configuration.dll`.  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/VB/source.vb#1)]  
  
## Creazione di oggetti DbProviderFactory e DbConnection  
 In questo esempio viene illustrato come creare oggetti <xref:System.Data.Common.DbProviderFactory> e <xref:System.Data.Common.DbConnection> passando ad essi il nome del provider in formato "*System.Data.ProviderName*" e una stringa di connessione.  In caso di esito positivo, viene restituito un oggetto `DbConnection`; in caso di errore, viene restituito `null` \(`Nothing` in Visual Basic\).  
  
 Il codice ottiene l'oggetto `DbProviderFactory` mediante una chiamata a <xref:System.Data.Common.DbProviderFactories.GetFactory%2A>.  Il metodo <xref:System.Data.Common.DbProviderFactory.CreateConnection%2A> crea quindi l'oggetto <xref:System.Data.Common.DbConnection> e la proprietà <xref:System.Data.Common.DbConnection.ConnectionString%2A> viene impostata sulla stringa di connessione.  
  
 [!code-csharp[DataWorks DbProviderFactories.GetFactory#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.GetFactory/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.GetFactory#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.GetFactory/VB/source.vb#1)]  
  
## Vedere anche  
 [DbProviderFactory](../../../../docs/framework/data/adonet/dbproviderfactories.md)   
 [Stringhe di connessione](../../../../docs/framework/data/adonet/connection-strings.md)   
 [Using the Configuration Classes](../Topic/Using%20the%20Configuration%20Classes.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)