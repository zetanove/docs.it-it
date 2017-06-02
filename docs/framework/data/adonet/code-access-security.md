---
title: "Sicurezza dall&#39;accesso di codice e ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 93e099eb-daa1-4f1e-b031-c1e10a996f88
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Sicurezza dall&#39;accesso di codice e ADO.NET
In .NET Framework sono incluse sia la sicurezza basata sui ruoli che la sicurezza dall'accesso di codice \(CAS, Code Access Security\), entrambe implementate usando un'infrastruttura comune fornita da CLR \(Common Language Runtime\).  In un contesto di codice non gestito la maggior parte delle applicazioni viene eseguita con le autorizzazioni dell'utente o entità di sicurezza.  Di conseguenza, quando un utente con privilegi elevati esegue software dannoso o con errori possono verificarsi danni al sistemi del computer e ai dati privati.  
  
 Al contrario, il codice gestito eseguito in .NET Framework include la sicurezza dall'accesso di codice, che viene applicata al solo codice.  L'esecuzione del codice verrà pertanto consentita in base all'origine o ad altri aspetti dell'identità del codice e non unicamente in base all'identità dell'entità di sicurezza.  In tal modo si riduce la probabilità di uso improprio del codice gestito.  
  
## Autorizzazioni di accesso al codice  
 Quando si esegue il codice, viene presentata l'evidenza restituita dal sistema di sicurezza di CLR.  In genere, tale evidenza comprende l'origine del codice, l'URL, il sito Web, l'area e le firme digitali che garantiscono l'identità dell'assembly.  
  
 CLR consente al codice di eseguire solo le operazioni che il codice è autorizzato a eseguire.  Il codice può richiedere delle autorizzazioni e tali richieste vengono eseguite in base al criterio di sicurezza impostato da un amministratore.  
  
> [!NOTE]
>  Il codice eseguito in CLR non può concedere autorizzazioni a se stesso.  Il codice può ad esempio richiedere e ottenere un numero di autorizzazioni inferiore, ma non superiore, rispetto a quello consentito da un criterio di sicurezza.  Quando si concedono autorizzazioni, iniziare senza autorizzazioni, quindi aggiungere le autorizzazioni minime per la specifica attività da eseguire.  Se invece si negano singole autorizzazioni dopo aver iniziato concedendole tutte, le applicazioni potrebbero risultare non protette e contenere problemi di sicurezza non intenzionali derivanti dalla concessione di un numero di autorizzazioni maggiore di quello necessario.  Per altre informazioni, vedere [NIB: Configuring Security Policy](http://msdn.microsoft.com/it-it/0f130bcd-1bba-4346-b231-0bcca7dab1a4) e [NIB: Security Policy Management](http://msdn.microsoft.com/it-it/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9).  
  
 Sono disponibili tre tipi di autorizzazioni di accesso al codice:  
  
-   `Code access permissions`, che derivano dalla classe <xref:System.Security.CodeAccessPermission>.  Le autorizzazioni sono necessarie per accedere a risorse protette, ad esempio file e variabili di ambiente, nonché per eseguire operazioni protette, ad esempio l'accesso a codice non gestito.  
  
-   `Identity permissions`, che rappresentano le caratteristiche identificative di un assembly.  Le autorizzazioni vengono concesse a un assembly in base a una prova, che può includere elementi quali una firma digitale o l'origine del codice.  Le autorizzazioni di identità derivano anche dalla classe base <xref:System.Security.CodeAccessPermission>.  
  
-   `Role-based security permissions`, che variano a seconda che un'entità di sicurezza disponga di un'identità specificata o sia membro di un ruolo specificato.  La classe <xref:System.Security.Permissions.PrincipalPermission> consente l'esecuzione di controlli di autorizzazione dichiarativi e imperativi sull'entità di sicurezza attiva.  
  
 Per determinare se il codice è autorizzato ad accedere a una risorsa o a eseguire un'operazione, il sistema di sicurezza del runtime attraversa lo stack di chiamate, confrontando le autorizzazioni concesse di ogni chiamante con l'autorizzazione richiesta.  Se un qualsiasi chiamante nello stack di chiamate non dispone dell'autorizzazione richiesta, viene generata un'eccezione <xref:System.Security.SecurityException> e l'accesso viene rifiutato.  
  
### Richiesta di autorizzazioni  
 Lo scopo della richiesta di autorizzazioni è informare il runtime delle autorizzazioni richieste per eseguire l'applicazione e garantire che riceva solo le autorizzazioni effettivamente necessarie.  Ad esempio, se l'applicazione deve scrivere dati sul disco locale, richiederà <xref:System.Security.Permissions.FileIOPermission>.  Se tale autorizzazione non è stata concessa, l'applicazione non riuscirà a scrivere sul disco.  Se tuttavia l'applicazione richiede `FileIOPermission` e tale autorizzazione non è stata concessa, l'applicazione genererà l'eccezione all'inizio e non verrà caricata.  
  
 In uno scenario in cui l'applicazione deve solo leggere dati dal disco, è possibile richiedere che non venga mai concessa alcuna autorizzazione di scrittura.  In caso di bug o attacco dannoso, il codice non potrà quindi danneggiare i dati su cui opera.  Per altre informazioni, vedere [NIB: Requesting Permissions](http://msdn.microsoft.com/it-it/0447c49d-8cba-45e4-862c-ff0b59bebdc2).  
  
## Sicurezza basata sui ruoli e CAS  
 L'implementazione della sicurezza basata sui ruoli e della sicurezza dall'accesso di codice \(CAS\) consente di migliorare la sicurezza complessiva dell'applicazione.  La sicurezza basata sui ruoli può essere impostata su un account di Windows o un'identità personalizzata, in modo da rendere le informazioni sull'entità di sicurezza disponibili al thread corrente.  È inoltre necessario che le applicazioni concedano l'accesso a dati o risorse in base alle credenziali fornite dall'utente.  In genere, queste applicazioni controllano il ruolo di un utente e consentono l'accesso alle risorse sulla base di tale ruolo.  
  
 La sicurezza basata sui ruoli consente a un componente di identificare gli utenti correnti e i relativi ruoli associati in fase di esecuzione.  Queste informazioni vengono quindi mappate usando un criterio CAS per determinare il set di autorizzazioni concesse in fase di esecuzione.  Per un dominio dell'applicazione specificato, l'host può modificare il criterio di sicurezza basato sui ruoli predefinito e impostare un'entità di sicurezza predefinita che rappresenta un utente e i ruoli ad esso associati.  
  
 CLR usa le autorizzazioni per implementare il proprio meccanismo di applicazione delle restrizioni sul codice gestito.  Le autorizzazioni di sicurezza basate sui ruoli offrono un meccanismo per individuare se un utente \(o l'agente che opera per conto dell'utente\) dispone di una specifica identità o è membro di un ruolo specificato.  Per altre informazioni, vedere [Security Permissions](http://msdn.microsoft.com/it-it/b03757b4-e926-4196-b738-3733ced2bda0).  
  
 A seconda del tipo di applicazione che si intende compilare, è opportuno considerare l'implementazione di autorizzazioni basate sui ruoli anche nel database.  Per altre informazioni sulla sicurezza basata sui ruoli in SQL Server, vedere [Sicurezza di SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md).  
  
## Assembly  
 Gli assembly costituiscono l'unità fondamentale della distribuzione, del controllo della versione, del riutilizzo, dell'ambito di attivazione e delle autorizzazioni di sicurezza per un'applicazione .NET Framework.  Un assembly fornisce infatti una raccolta di tipi e risorse che interagiscono tra loro e costituiscono un'unità logica della funzionalità.  Per CLR un tipo non esiste al di fuori del contesto di un assembly.  Per altre informazioni sulla creazione e la distribuzione di assembly, vedere [Programmazione con gli assembly](../../../../docs/framework/app-domains/programming-with-assemblies.md).  
  
### Assegnazione di nomi sicuri agli assembly  
 Un nome sicuro, o firma digitale, è costituito dall'identità dell'assembly, che include il nome in testo semplice, il numero di versione e informazioni sulle impostazioni cultura \(se fornite\), nonché una chiave pubblica e una firma digitale.  La firma digitale viene generata da un file di assembly usando la chiave privata corrispondente.  Il file di assembly contiene il manifesto dell'assembly, contenente i nomi e gli hash di tutti i file che costituiscono l'assembly.  
  
 L'assegnazione di nomi sicuri consente a un'applicazione o a un componente di disporre di un'identità univoca utilizzabile da altri software per riferirsi esplicitamente a tale applicazione o componente.  Consente inoltre di proteggere gli assembly dallo spoofing da parte di un assembly contenente codice dannoso  e garantisce la compatibilità tra diverse versioni di un componente.  Agli assembly che verranno distribuiti nella Global Assembly Cache \(GAC\) deve essere assegnato un nome sicuro.  Per altre informazioni, vedere [Creazione e utilizzo degli assembly con nome sicuro](../../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md).  
  
## Attendibilità parziale in ADO.NET 2.0  
 Con ADO.NET 2.0 i provider di dati .NET Framework per SQL Server, per OLE DB, per ODBC e per Oracle possono essere eseguiti in ambienti ad attendibilità parziale.  Nelle versioni precedenti di .NET Framework le applicazioni non totalmente attendibili supportavano solo <xref:System.Data.SqlClient>.  
  
 Un'applicazione ad attendibilità parziale che usa il provider per SQL Server deve disporre almeno delle autorizzazioni minime di esecuzione e di <xref:System.Data.SqlClient.SqlClientPermission>.  
  
### Proprietà dell'attributo di autorizzazione per l'attendibilità parziale  
 Per gli scenari ad attendibilità parziale, è possibile usare i membri di <xref:System.Data.SqlClient.SqlClientPermissionAttribute> per restringere ulteriormente le funzionalità a disposizione del provider di dati .NET Framework per SQL Server.  
  
 Nella tabella seguente vengono elencate le proprietà disponibili per la classe <xref:System.Data.SqlClient.SqlClientPermissionAttribute> e le relative descrizioni:  
  
|Proprietà dell'attributo di autorizzazione|Descrizione|  
|------------------------------------------------|-----------------|  
|`Action`|Ottiene o imposta un'azione di sicurezza.  La proprietà viene ereditata da <xref:System.Security.Permissions.SecurityAttribute>.|  
|`AllowBlankPassword`|Viene usata per consentire o meno l'immissione di una password vuota in una stringa di connessione.  Valori validi sono `true`, per consentire l'uso di password vuote, e `false`, per impedire l'uso di password vuote.  La proprietà viene ereditata da <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`ConnectionString`|Viene usata per identificare una stringa di connessione consentita.  È possibile identificare più stringhe di connessione. **Note:**  Non includere un identificatore utente o una password nella stringa di connessione.  In questa versione non è possibile modificare le restrizioni relative alle stringhe di connessione usando lo strumento Configurazione .NET Framework. <br /><br /> La proprietà viene ereditata da <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`KeyRestrictions`|Viene usata per identificare i parametri delle stringhe di connessione consentiti o non consentiti.  I parametri delle stringhe di connessione vengono identificati nel formato *\<nome parametro\>\=*.  Per specificare più parametri, separarli con un punto e virgola \(;\). **Note:**  Se non viene specificata alcuna `KeyRestrictions` e la proprietà `KeyRestrictionBehavior` è impostata su `AllowOnly` o `PreventUsage`, non saranno consentiti parametri aggiuntivi per la stringa di connessione.  La proprietà viene ereditata da <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`KeyRestrictionBehavior`|Viene usata per identificare i parametri della stringa di connessione come unici parametri aggiuntivi consentiti \(`AllowOnly`\) oppure per identificare i parametri aggiuntivi non consentiti \(`PreventUsage`\).  Il valore predefinito è `AllowOnly`.  La proprietà viene ereditata da <xref:System.Data.Common.DBDataPermissionAttribute>.|  
|`TypeID`|Ottiene un identificatore univoco per l'attributo quando viene implementato in una classe derivata.  La proprietà viene ereditata da <xref:System.Attribute>.|  
|`Unrestricted`|Indica che esiste una dichiarazione di accesso senza limitazioni alla risorsa.  La proprietà viene ereditata da <xref:System.Security.Permissions.SecurityAttribute>.|  
  
#### Sintassi di ConnectionString  
 Nell'esempio seguente viene illustrato come usare l'elemento `connectionStrings` di un file di configurazione per consentire l'uso solo di una stringa di connessione specifica.  Per altre informazioni sull'archiviazione e il recupero delle stringhe di connessione dai file di configurazione, vedere [Stringhe di connessione](../../../../docs/framework/data/adonet/connection-strings.md).  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;" />  
</connectionStrings>  
```  
  
#### Sintassi di KeyRestrictions  
 L'esempio seguente abilita la stringa di connessione sopra riportata, consente l'uso delle opzioni di stringa di connessione `Encrypt` e `Packet``Size`, ma impedisce l'uso di ogni altra opzione di stringa di connessione.  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Encrypt=;Packet Size=;"  
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
#### KeyRestrictionBehavior con sintassi di PreventUsage  
 Nell'esempio seguente viene abilitata la stringa di connessione sopra riportata e vengono consentiti tutti gli altri parametri di connessione ad eccezione di `User Id`, `Password` e `Persist Security Info`.  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="User Id=;Password=;Persist Security Info=;"  
    KeyRestrictionBehavior="PreventUsage" />  
</connectionStrings>  
```  
  
#### KeyRestrictionBehavior con sintassi di AllowOnly  
 L'esempio seguente abilita due stringhe di connessione contenenti anche i parametri `Initial Catalog`, `Connection Timeout`, `Encrypt` e `Packet Size`.  Tutti gli altri parametri di stringa di connessione non sono consentiti.  
  
```  
<connectionStrings>  
  <add name="DatabaseConnection"   
    connectionString="Data Source=(local);Initial   
    Catalog=Northwind;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
  
  <add name="DatabaseConnection2"   
    connectionString="Data Source=SqlServer2;Initial   
    Catalog=Northwind2;Integrated Security=true;"  
    KeyRestrictions="Initial Catalog;Connection Timeout=;  
       Encrypt=;Packet Size=;"   
    KeyRestrictionBehavior="AllowOnly" />  
</connectionStrings>  
```  
  
### Abilitazione dell'attendibilità parziale con un set di autorizzazioni personalizzato  
 Per usare le autorizzazioni <xref:System.Data.SqlClient> per un'area particolare, è necessario che un amministratore di sistema crei un set di autorizzazioni personalizzato e lo imposti come set di autorizzazioni per tale area.  I set di autorizzazioni predefiniti, ad esempio `LocalIntranet`, non possono essere modificati.  Ad esempio, per aggiungere autorizzazioni <xref:System.Data.SqlClient> a codice la cui <xref:System.Security.Policy.Zone> sia `LocalIntranet`, un amministratore di sistema può copiare il set di autorizzazioni per `LocalIntranet`, rinominarlo in "CustomLocalIntranet", aggiungervi le autorizzazioni <xref:System.Data.SqlClient>, importare il set di autorizzazioni CustomLocalIntranet usando lo [Caspol.exe \(Code Access Security Policy Tool\)](../../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md) e impostare il set di autorizzazioni di `LocalIntranet_Zone` su CustomLocalIntranet.  
  
### Set di autorizzazioni di esempio  
 Di seguito è riportato un set di autorizzazioni di esempio per il provider di dati .NET Framework per SQL Server in uno scenario ad attendibilità parziale.  Per altre informazioni sulla creazione di set di autorizzazioni personalizzati, vedere [NIB:Configuring Permission Sets Using Caspol.exe](http://msdn.microsoft.com/it-it/94e2625e-21ad-4038-af36-6d1f9df40a57).  
  
```  
<PermissionSet class="System.Security.NamedPermissionSet"  
  version="1"  
  Name="CustomLocalIntranet"  
  Description="Custom permission set given to applications on  
    the local intranet">  
  
<IPermission class="System.Data.SqlClient.SqlClientPermission, System.Data, Version=2.0.0000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
version="1"  
AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Integrated Security=true;"  
 KeyRestrictions="Initial Catalog=;Connection Timeout=;  
   Encrypt=;Packet Size=;"   
 KeyRestrictionBehavior="AllowOnly" />  
 </IPermission>  
</PermissionSet>  
```  
  
## Verifica dell'accesso di codice ADO.NET tramite le autorizzazioni di sicurezza  
 Per scenari ad attendibilità parziale, è possibile identificare nel codice metodi particolari quali la richiesta di un determinato privilegio di sicurezza dall'accesso di codice specificando una proprietà <xref:System.Data.SqlClient.SqlClientPermissionAttribute>.  Se tale privilegio non è consentito dalle restrizioni dei criteri di sicurezza, verrà generata un'eccezione prima dell'esecuzione del codice.  Per altre informazioni sui criteri di sicurezza, vedere [NIB: Security Policy Management](http://msdn.microsoft.com/it-it/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9) e [NIB: Security Policy Best Practices](http://msdn.microsoft.com/it-it/d49bc4d5-efb7-4caa-a2fe-e4d3cec63c05).  
  
### Esempio  
 Nell'esempio seguente viene illustrato come scrivere codice che richieda una stringa di connessione particolare.  Tale codice consente di simulare la negazione a <xref:System.Data.SqlClient> di autorizzazioni senza restrizioni, che in realtà verrebbero implementate da un amministratore di sistema tramite i criteri di sicurezza dall'accesso di codice.  
  
> [!IMPORTANT]
>  Quando si progettano le autorizzazioni di sicurezza dall'accesso di codice per ADO.NET, è consigliabile iniziare dal caso più restrittivo \(nessuna autorizzazione\) e aggiungere le autorizzazioni specifiche necessarie per l'attività particolare che deve essere eseguita dal codice.  Al contrario, non è sicuro concedere inizialmente tutte le autorizzazioni e successivamente negare un'autorizzazione specifica, poiché la stessa stringa di connessione può essere espressa in molti modi diversi.  Ad esempio, se inizialmente si concedono tutte le autorizzazioni e successivamente si tenta di negare l'uso della stringa di connessione "server\=nomeserver", verrà comunque consentito l'uso della stringa "server\=nomeserver.società.com".  Al contrario, se all'inizio non si concede alcuna autorizzazione, si ridurrà la possibilità di problemi di sicurezza nel set di autorizzazioni.  
  
 Nel codice seguente viene illustrato come `SqlClient` esegue la richiesta di sicurezza, che genera una <xref:System.Security.SecurityException> se non sono impostate le autorizzazioni di sicurezza dall'accesso di codice appropriate.  Nella finestra della console verrà visualizzato l'output di <xref:System.Security.SecurityException>.  
  
 [!code-csharp[DataWorks SqlClient.CAS#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.CAS#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.CAS/VB/source.vb#1)]  
  
 Nella finestra della console verrà visualizzato il seguente output:  
  
```  
Failed, as expected: <IPermission class="System.Data.SqlClient.  
SqlClientPermission, System.Data, Version=2.0.0.0,   
  Culture=neutral, PublicKeyToken=b77a5c561934e089" version="1"  
  AllowBlankPassword="False">  
<add ConnectionString="Data Source=(local);Initial Catalog=  
  Northwind;Integrated Security=SSPI" KeyRestrictions=""  
KeyRestrictionBehavior="AllowOnly"/>  
</IPermission>  
  
Connection opened, as expected.  
Failed, as expected: Request failed.  
```  
  
## Interoperabilità con codice non gestito  
 Il codice che non viene eseguito con CLR viene denominato codice non gestito.  Non è pertanto possibile applicare al codice non gestito meccanismi di sicurezza quali la sicurezza dall'accesso di codice \(CAS\).  Esempi di codice non gestito sono i componenti COM, le interfacce ActiveX e le funzioni dell'API Win32.  Quando si esegue codice non gestito, è necessario applicare considerazioni specifiche relative alla sicurezza al fine di non compromettere la sicurezza dell'applicazione.  Per altre informazioni, vedere [Interoperating with Unmanaged Code](../../../../docs/framework/interop/index.md).  
  
 In .NET Framework la compatibilità con versioni precedenti di componenti COM esistenti viene supportata fornendo l'accesso tramite l'interoperabilità COM.  È possibile incorporare componenti COM in un'applicazione .NET Framework usando gli strumenti di interoperabilità COM per importare i tipi COM attinenti.  Una volta importati, i tipi COM sono pronti per l'uso.  L'interoperabilità COM consente anche ai client COM di accedere a codice gestito esportando i metadati dell'assembly in una libreria dei tipi e registrando il componente gestito come componente COM.  Per altre informazioni, vedere [Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb).  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [PAVE Security in Native and .NET Framework Code](http://msdn.microsoft.com/it-it/bd61be84-c143-409a-a75a-44253724f784)   
 [Code Access Security](http://msdn.microsoft.com/it-it/23a20143-241d-4fe5-9d9f-3933fd594c03)   
 [Role\-Based Security](http://msdn.microsoft.com/it-it/239442e3-5be4-4203-b7fd-793baffea803)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)