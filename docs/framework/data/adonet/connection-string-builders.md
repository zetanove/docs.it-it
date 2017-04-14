---
title: "Compilatori di stringhe di connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Compilatori di stringhe di connessione
Nelle versioni precedenti di [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] il controllo in fase di compilazione delle stringhe di connessione con valori di stringhe concatenate non veniva eseguito, quindi in fase di esecuzione una parola chiave non corretta avrebbe generato un'eccezione <xref:System.ArgumentException>.  Poiché ogni provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] supporta una sintassi diversa per le parole chiave delle stringhe di connessione, la costruzione manuale di stringhe di connessione valide risulta difficile.  Per risolvere questo problema, in [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 2.0 sono stati introdotti nuovi generatori di stringhe di connessione per ogni provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  Ogni provider di dati include una classe di generatori di stringhe di connessione fortemente tipizzata che eredita da <xref:System.Data.Common.DbConnectionStringBuilder>.  Nella tabella seguente sono elencati i provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] e le classi di compilatori di stringhe di connessione associate.  
  
|Provider|Classe ConnectionStringBuilder|  
|--------------|------------------------------------|  
|<xref:System.Data.SqlClient>|<xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.OleDb>|<xref:System.Data.OleDb.OleDbConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.Odbc>|<xref:System.Data.Odbc.OdbcConnectionStringBuilder?displayProperty=fullName>|  
|<xref:System.Data.OracleClient>|<xref:System.Data.OracleClient.OracleConnectionStringBuilder?displayProperty=fullName>|  
  
## Attacchi injection alle stringhe di connessione  
 Un attacco injection alle stringhe di connessione può verificarsi quando si usa la concatenazione dinamica di stringhe per compilare stringhe di connessione basate sull'input dell'utente.  Se la stringa non viene convalidata e il testo o i caratteri dannosi non vengono convertiti in caratteri di escape, un utente non autorizzato potrebbe accedere a dati sensibili o ad altre risorse del server.  Ad esempio, un utente non autorizzato potrebbe eseguire un attacco specificando un punto e virgola e aggiungendo un altro valore.  La stringa di connessione viene analizzata tramite un algoritmo basato sul principio che l'ultima occorrenza ha la priorità, pertanto l'input dannoso viene sostituito a un valore lecito.  
  
 Le classi di generatori di stringhe di connessione sono progettate per eliminare la necessità di basarsi su congetture e proteggersi da errori di sintassi e vulnerabilità della sicurezza.  Forniscono metodi e proprietà che corrispondono alle coppie chiave\/valore note consentite da ogni provider di dati.  Ogni classe mantiene una raccolta fissa di sinonimi e può essere convertita da un sinonimo al nome di chiave noto.  Vengono eseguiti controlli per rilevare coppie chiave\/valore valide e le coppie non valide generano un'eccezione.  Inoltre, i valori inseriti vengono gestiti in modo sicuro.  
  
 Nell'esempio seguente viene illustrata la modalità con cui <xref:System.Data.SqlClient.SqlConnectionStringBuilder> gestisce un valore aggiuntivo inserito per l'impostazione `Initial Catalog`.  
  
```vb  
Dim builder As New System.Data.SqlClient.SqlConnectionStringBuilder  
builder("Data Source") = "(local)"  
builder("Integrated Security") = True  
builder("Initial Catalog") = "AdventureWorks;NewValue=Bad"  
Console.WriteLine(builder.ConnectionString)  
```  
  
```csharp  
System.Data.SqlClient.SqlConnectionStringBuilder builder =  
  new System.Data.SqlClient.SqlConnectionStringBuilder();  
builder["Data Source"] = "(local)";  
builder["integrated Security"] = true;  
builder["Initial Catalog"] = "AdventureWorks;NewValue=Bad";  
Console.WriteLine(builder.ConnectionString);  
```  
  
 Dall'output si rileva che <xref:System.Data.SqlClient.SqlConnectionStringBuilder> ha gestito correttamente questa situazione convertendo in caratteri di escape il valore aggiuntivo in virgolette doppie anziché aggiungerlo alla stringa di connessione come nuova coppia chiave\/valore.  
  
```  
data source=(local);Integrated Security=True;  
initial catalog="AdventureWorks;NewValue=Bad"  
```  
  
## Compilazione di stringhe di connessione da file di configurazione  
 Se determinati elementi di una stringa di connessione sono noti in anticipo, possono essere archiviati in un file di configurazione e recuperati in fase di esecuzione per costruire una stringa di connessione completa.  Ad esempio, è possibile che il nome del database sia noto in anticipo, ma non il nome del server.  Oppure è possibile che si desideri che un utente specifichi un nome utente e una password in fase di esecuzione senza avere la possibilità di inserire altri valori nella stringa di connessione.  
  
 Uno dei costruttori di overload per un generatore di stringhe di connessione accetta <xref:System.String> come argomento, consentendo di specificare una stringa di connessione parziale che può essere quindi completata dall'input dell'utente.  La stringa di connessione parziale può essere archiviata in un file di configurazione e recuperata in fase di esecuzione.  
  
> [!NOTE]
>  Lo spazio dei nomi <xref:System.Configuration> consente l'accesso a livello di codice ai file di configurazione che usano <xref:System.Web.Configuration.WebConfigurationManager> per le applicazioni Web e <xref:System.Configuration.ConfigurationManager> per le applicazioni Windows.  Per altre informazioni sull'utilizzo di stringhe di connessione e file di configurazione, vedere [Stringhe di connessione e file di configurazione](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md).  
  
### Esempio  
 In questo esempio vengono illustrati il recupero di una stringa di connessione da un file di configurazione e il relativo completamento tramite l'impostazione delle proprietà <xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A>, <xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A> e <xref:System.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> di <xref:System.Data.SqlClient.SqlConnectionStringBuilder>.  Il file di configurazione viene definito come segue.  
  
```  
<connectionStrings>  
  <clear/>  
  <add name="partialConnectString"   
    connectionString="Initial Catalog=Northwind;"  
    providerName="System.Data.SqlClient" />  
</connectionStrings>  
```  
  
> [!NOTE]
>  È necessario impostare un riferimento a `System.Configuration.dll` nel progetto affinché il codice venga eseguito.  
  
 [!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/CS/source.cs#1)]
 [!code-vb[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlConnectionStringBuilder.UserNamePwd/VB/source.vb#1)]  
  
## Vedere anche  
 [Stringhe di connessione](../../../../docs/framework/data/adonet/connection-strings.md)   
 [Privacy e sicurezza dei dati](../../../../docs/framework/data/adonet/privacy-and-data-security.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)