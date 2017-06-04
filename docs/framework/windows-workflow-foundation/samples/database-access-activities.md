---
title: "Attivit&#224; di accesso al database | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 174a381e-1343-46a8-a62c-7c2ae2c4f0b2
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Attivit&#224; di accesso al database
Le attività di accesso al database consentono di accedere a un database all'interno di un flusso di lavoro.Queste attività consentono l'accesso a database per recuperare o modificare informazioni e utilizzare [ADO.NET](http://go.microsoft.com/fwlink/?LinkId=166081) per accedere al database.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, visitare la pagina di download per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\DbActivities`  
  
## Attività di database  
 Nelle sezioni seguenti viene descritto in dettaglio l'elenco delle attività incluse in questo esempio.  
  
## DbUpdate  
 Esegue una query SQL che produce una modifica nel database \(inserimento, aggiornamento, eliminazione e altre modifiche\).  
  
 Questa classe esegue le relative operazioni in modo asincrono \(deriva da <xref:System.Activities.AsyncCodeActivity> e utilizza le relative funzionalità asincrone\).  
  
 È possibile configurare le informazioni di connessione impostando un nome invariante del provider \(`ProviderName`\) e la stringa di connessione \(`ConnectionString`\) o solo utilizzando un nome di configurazione della stringa di connessione \(`ConfigFileSectionName`\) dal file di configurazione dell'applicazione.  
  
 La query da eseguire viene configurata nella relativa proprietà `Sql` e i parametri vengono passati tramite la raccolta `Parameters`.  
  
 Dopo l'esecuzione di `DbUpdate`, il numero di record interessati viene restituito nella proprietà `AffectedRecords`.  
  
```  
Public class DbUpdate: AsyncCodeActivity  
{  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
  
    [DependsOn("Parameters")]  
    public OutArgument<int> AffectedRecords { get; set; }       
}  
```  
  
|||  
|-|-|  
|Argomento|Descrizione|  
|ProviderName|Nome invariante del provider ADO.NET.Se viene impostato questo argomento, è necessario impostare anche `ConnectionString`.|  
|ConnectionString|Stringa di connessione per connettersi al database.Se viene impostato questo argomento, è necessario impostare anche `ProviderName`.|  
|ConfigName|Nome della sezione del file di configurazione in cui sono archiviate le informazioni di connessione.Quando viene impostato questo argomento, `ProviderName` e `ConnectionString` non sono richiesti.|  
|CommandType|Tipo di <xref:System.Data.Common.DbCommand> da eseguire.|  
|Sql|Comando SQL da eseguire.|  
|Parameters|Raccolta di parametri della query SQL.|  
|AffectedRecords|Numero di record interessato dall'ultima operazione.|  
  
## DbQueryScalar  
 Esegue una query che recupera un singolo valore dal database.  
  
 Questa classe esegue le relative operazioni in modo asincrono \(deriva da <xref:System.Activities.AsyncCodeActivity%601> e utilizza le relative funzionalità asincrone\).  
  
 È possibile configurare le informazioni di connessione impostando un nome invariante del provider \(`ProviderName`\) e la stringa di connessione \(`ConnectionString`\) o solo utilizzando un nome di configurazione della stringa di connessione \(`ConfigFileSectionName`\) dal file di configurazione dell'applicazione.  
  
 La query da eseguire viene configurata nella relativa proprietà `Sql` e i parametri vengono passati tramite la raccolta `Parameters`.  
  
 Dopo l'esecuzione di `DbQueryScalar`, il valore scalare viene restituito nell'argomento `Result``out` \(di tipo `TResult`, definito nella classe di base <xref:System.Activities.AsyncCodeActivity%601>\).  
  
```  
public class DbQueryScalar<TResult> : AsyncCodeActivity<TResult>  
{  
    // public arguments  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
}  
```  
  
|||  
|-|-|  
|Argomento|Descrizione|  
|ProviderName|Nome invariante del provider ADO.NET.Se viene impostato questo argomento, è necessario impostare anche `ConnectionString`.|  
|ConnectionString|Stringa di connessione per connettersi al database.Se viene impostato questo argomento, è necessario impostare anche `ProviderName`.|  
|ConfigName|Nome della sezione del file di configurazione in cui sono archiviate le informazioni di connessione.Quando viene impostato questo argomento, `ProviderName` e `ConnectionString` non sono richiesti.|  
|CommandType|Tipo di <xref:System.Data.Common.DbCommand> da eseguire.|  
|Sql|Comando SQL da eseguire.|  
|Parameters|Raccolta di parametri della query SQL.|  
|Result|Valore scalare ottenuto dopo l'esecuzione della query.Questo argomento è di tipo `TResult`.|  
  
## DbQuery  
 Esegue una query che recupera un elenco di oggetti.Dopo l'esecuzione della query, viene eseguita una funzione di mapping \(può essere `TResult`\> o `TResult`\>\) <xref:System.Func%601>\<`DbDataReader`<xref:System.Activities.ActivityFunc%601>\<`DbDataReader`.Questa funzione di mapping ottiene un record in un oggetto `DbDataReader` e ne esegue il mapping all'oggetto da restituire.  
  
 È possibile configurare le informazioni di connessione impostando un nome invariante del provider \(`ProviderName`\) e la stringa di connessione \(`ConnectionString`\) o solo utilizzando un nome di configurazione della stringa di connessione \(`ConfigFileSectionName`\) dal file di configurazione dell'applicazione.  
  
 La query da eseguire viene configurata nella relativa proprietà `Sql` e i parametri vengono passati tramite la raccolta `Parameters`.  
  
 I risultati della query SQL vengono recuperati utilizzando un oggetto `DbDataReader`.L'attività scorre `DbDataReader` ed esegue il mapping delle righe in `DbDataReader` a un'istanza di `TResult`.L'utente di `DbQuery` deve fornire il codice di mapping. Questa operazione può essere effettuata in due modi: utilizzando <xref:System.Func%601>\<`DbDataReader`, `TResult`\> o <xref:System.Activities.ActivityFunc%601>\<`DbDataReader`, `TResult`\>.Nel primo caso, il mapping viene eseguito in un singolo impulso.È pertanto più veloce, ma non può essere serializzato in XAML.Nel secondo caso, il mapping viene eseguito in più impulsi.Può quindi risultare più lento, ma può essere serializzato in XAML e modificato in modo dichiarativo \(qualsiasi attività esistente può partecipare al mapping\).  
  
```  
public class DbQuery<TResult> : AsyncCodeActivity<IList<TResult>> where TResult : class  
{  
    // public arguments  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
  
    [OverloadGroup("DirectMapping")]  
    [DefaultValue(null)]  
    public Func<DbDataReader, TResult> Mapper { get; set; }  
  
    [OverloadGroup("MultiplePulseMapping")]  
    [DefaultValue(null)]  
    public ActivityFunc<DbDataReader, TResult> MapperFunc { get; set; }  
}  
```  
  
|||  
|-|-|  
|Argomento|Descrizione|  
|ProviderName|Nome invariante del provider ADO.NET.Se viene impostato questo argomento, è necessario impostare anche `ConnectionString`.|  
|ConnectionString|Stringa di connessione per connettersi al database.Se viene impostato questo argomento, è necessario impostare anche `ProviderName`.|  
|ConfigName|Nome della sezione del file di configurazione in cui sono archiviate le informazioni di connessione.Quando viene impostato questo argomento, `ProviderName` e `ConnectionString` non sono richiesti.|  
|CommandType|Tipo di <xref:System.Data.Common.DbCommand> da eseguire.|  
|Sql|Comando SQL da eseguire.|  
|Parameters|Raccolta di parametri della query SQL.|  
|Mapper|Funzione di mapping \(<xref:System.Func%601>\<`DbDataReader`, `TResult`\>\) che accetta un record nell'oggetto `DataReader` ottenuto come risultato dell'esecuzione della query e restituisce un'istanza di un oggetto di tipo `TResult` da aggiungere alla raccolta `Result`.<br /><br /> In questo caso, il mapping viene eseguito in un singolo impulso, ma non può essere modificato in modo dichiarativo tramite la finestra di progettazione.|  
|MapperFunc|Funzione di mapping \(<xref:System.Activities.ActivityFunc%601>\<`DbDataReader`, `TResult`\>\) che accetta un record nell'oggetto `DataReader` ottenuto come risultato dell'esecuzione della query e restituisce un'istanza di un oggetto di tipo `TResult` da aggiungere alla raccolta `Result`.<br /><br /> In questo caso, il mapping viene eseguito in più impulsi.Questa funzione può essere serializzata in XAML e modificata in modo dichiarativo \(qualsiasi attività esistente può partecipare al mapping\).|  
|Result|Elenco di oggetti ottenuto come risultato dell'esecuzione della query e dell'esecuzione della funzione di mapping per ogni record in `DataReader`.|  
  
## DbQueryDataSet  
 Esegue una query che restituisce un oggetto <xref:System.Data.DataSet>.Questa classe esegue le relative operazioni in modo asincrono.Deriva da <xref:System.Activities.AsyncCodeActivity>\<`TResult`\> e utilizza le relative funzionalità asincrone.  
  
 È possibile configurare le informazioni di connessione impostando un nome invariante del provider \(`ProviderName`\) e la stringa di connessione \(`ConnectionString`\) o solo utilizzando un nome di configurazione della stringa di connessione \(`ConfigFileSectionName`\) dal file di configurazione dell'applicazione.  
  
 La query da eseguire viene configurata nella relativa proprietà `Sql` e i parametri vengono passati tramite la raccolta `Parameters`.  
  
 Dopo l'esecuzione di `DbQueryDataSet`, `DataSet` viene restituito nell'argomento `Result``out` \(di tipo `TResult`, definito nella classe di base <xref:System.Activities.AsyncCodeActivity%601>\).  
  
```  
public class DbQueryDataSet : AsyncCodeActivity<DataSet>  
{  
    // public arguments  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
}  
```  
  
|||  
|-|-|  
|Argomento|Descrizione|  
|ProviderName|Nome invariante del provider ADO.NET.Se viene impostato questo argomento, è necessario impostare anche `ConnectionString`.|  
|ConnectionString|Stringa di connessione per connettersi al database.Se viene impostato questo argomento, è necessario impostare anche `ProviderName`.|  
|ConfigName|Nome della sezione del file di configurazione in cui sono archiviate le informazioni di connessione.Quando viene impostato questo argomento, `ProviderName` e `ConnectionString` non sono richiesti.|  
|CommandType|Tipo di <xref:System.Data.Common.DbCommand> da eseguire.|  
|Sql|Comando SQL da eseguire.|  
|Parameters|Raccolta di parametri della query SQL.|  
|Result|<xref:System.Data.DataSet> ottenuto dopo l'esecuzione della query.|  
  
## Configurazione delle informazioni di connessione  
 Tutte le attività DbActivities condividono gli stessi parametri di configurazione.Possono essere configurate in due modi:  
  
-   `ConnectionString + InvariantName`: impostare il nome invariante del provider ADO.NET e la stringa di connessione.  
  
    ```  
    Activity dbSelectCount = new DbQueryScalar<DateTime>()  
    {  
        ProviderName = "System.Data.SqlClient",  
        ConnectionString = @"Data Source=.\SQLExpress;  
                             Initial Catalog=DbActivitiesSample;  
                             Integrated Security=True",  
        Sql = "SELECT GetDate()"  
    };  
    ```  
  
-   `ConfigName`: impostare il nome della sezione di configurazione che contiene le informazioni di connessione.  
  
    ```  
    <connectionStrings>      
        <add name="DbActivitiesSample"  
             providerName="System.Data.SqlClient"  
             connectionString="Data Source=.\SQLExpress;Initial Catalog=DbActivitiesSample;Integrated Security=true"/>  
      </connectionStrings>  
    ```  
  
-   Nell'attività:  
  
    ```  
    Activity dbSelectCount = new DbQueryScalar<int>()  
    {                  
        ConfigName = "DbActivitiesSample",  
        Sql = "SELECT COUNT(*) FROM Roles"  
    };  
    ```  
  
## Esecuzione dell'esempio  
  
### Istruzioni per l'impostazione  
 In questo esempio viene utilizzato un database.Con l'esempio viene fornito uno script di impostazione e caricamento \(Setup.cmd\) .È necessario eseguire il file dal prompt dei comandi.  
  
 Lo script Setup.cmd richiama il file di script CreateDb.sql che contiene i comandi SQL per l'esecuzione delle operazioni seguenti:  
  
-   Crea un database denominato DbActivitiesSample.  
  
-   Crea la tabella Ruoli.  
  
-   Crea la tabella Employees.  
  
-   Inserisce tre record nella tabella Ruoli.  
  
-   Inserisce dodici record nella tabella Employees.  
  
##### Per eseguire Setup.cmd  
  
1.  Aprire un prompt dei comandi.  
  
2.  Passare alla cartella di esempio DbActivities.  
  
3.  Digitare "setup.cmd", quindi premere INVIO.  
  
    > [!NOTE]
    >  Setup.cmd tenta di installare l'esempio nell'istanza di SqlExpress del computer locale.Se si desidera installarlo in un'altra istanza del server SQL, modificare Setup.cmd specificando il nome della nuova istanza.  
  
##### Per disinstallare il database di esempio  
  
1.  Eseguire Cleanup.cmd dalla cartella di esempio in un prompt dei comandi.  
  
##### Per eseguire l’esempio  
  
1.  Aprire la soluzione in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire l'esempio senza debug, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\DbActivities`