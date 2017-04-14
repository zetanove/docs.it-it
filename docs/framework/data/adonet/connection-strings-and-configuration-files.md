---
title: "Stringhe di connessione e file di configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37df2641-661e-407a-a3fb-7bf9540f01e8
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Stringhe di connessione e file di configurazione
Se le stringhe di connessione vengono incorporate nel codice dell'applicazione, è possibile che si verifichino vulnerabilità della sicurezza e problemi di manutenzione.  Le stringhe di connessione non crittografate compilate nel codice sorgente di un'applicazione possono essere visualizzate tramite lo strumento [Ildasm.exe \(IL Disassembler\)](../../../../docs/framework/tools/ildasm-exe-il-disassembler.md).  Inoltre, se la stringa di connessione viene modificata, è necessario ricompilare l'applicazione.  Per questi motivi, si consiglia di archiviare le stringhe di connessione in un file di configurazione dell'applicazione.  
  
## Utilizzo dei file di configurazione delle applicazioni  
 I file di configurazione delle applicazioni contengono impostazioni specifiche di una determinata applicazione.  Ad esempio, un'applicazione ASP.NET può includere uno o più file **web.config**, mentre un'applicazione Windows può includere un file **app.config** facoltativo.  I file di configurazione condividono elementi comuni, anche se il nome e il percorso variano a seconda dell'host dell'applicazione.  
  
### Sezione connectionStrings  
 Le stringhe di connessione possono essere archiviate come coppie chiave\/valore nella sezione **connectionStrings** dell'elemento **configuration** di un file di configurazione dell'applicazione.  Gli elementi figlio includono **add**, **clear** e **remove**.  
  
 Nel frammento di file di configurazione seguente sono illustrati lo schema e la sintassi per l'archiviazione di una stringa di connessione.  L'attributo **name** corrisponde al nome specificato per identificare in modo univoco una connessione, in modo che possa essere recuperato in fase di esecuzione.  L'attributo **providerName** è il nome invariabile del provider di dati .NET Framework, registrato nel file machine.config.  
  
```  
<?xml version='1.0' encoding='utf-8'?>  
  <configuration>  
    <connectionStrings>  
      <clear />  
      <add name="Name"   
       providerName="System.Data.ProviderName"   
       connectionString="Valid Connection String;" />  
    </connectionStrings>  
  </configuration>  
```  
  
> [!NOTE]
>  È possibile salvare parte di una stringa di connessione in un file di configurazione e usare la classe <xref:System.Data.Common.DbConnectionStringBuilder> per completarlo in fase di esecuzione.  Questa funzione è utile nelle situazioni in cui non si conoscono in anticipo gli elementi della stringa di connessione o quando non si desidera salvare informazioni sensibili in un file di configurazione.  Per altre informazioni, vedere [Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
### Uso di file di configurazione esterni  
 I file di configurazione esterni sono file distinti che contengono un frammento di un file di configurazione costituito da un'unica sezione.  Al file di configurazione esterno viene quindi fatto riferimento dal file di configurazione principale.  L'archiviazione della sezione **connectionStrings** in un file fisicamente distinto risulta utile nelle situazioni in cui le stringhe di connessione potrebbero essere modificate dopo la distribuzione dell'applicazione.  Ad esempio, il comportamento ASP.NET standard prevede il riavvio di un dominio di applicazione quando i file di configurazione vengono modificati, con la conseguenza che le informazioni sullo stato vanno perse.  Tuttavia, la modifica di un file di configurazione esterno non provoca un riavvio dell'applicazione.  Oltre che in ASP.NET, i file di configurazione esterni possono essere usati anche nelle applicazioni Windows.  È possibile inoltre usare la sicurezza e le autorizzazioni di accesso ai file per limitare l'accesso ai file di configurazione esterni.  L'uso di file di configurazione esterni in fase di esecuzione è trasparente e non richiede codice speciale.  
  
 Per archiviare le stringhe di connessione in un file di configurazione esterno, creare un file distinto che contiene solo la sezione **connectionStrings**.  Non includere altri elementi, sezioni o attributi.  Questo esempio illustra la sintassi di un file di configurazione esterno.  
  
```  
<connectionStrings>  
  <add name="Name"   
   providerName="System.Data.ProviderName"   
   connectionString="Valid Connection String;" />  
</connectionStrings>  
```  
  
 Nel file di configurazione principale dell'applicazione usare l'attributo **configSource** per specificare il nome completo e il percorso del file esterno.  In questo esempio si fa riferimento a un file di configurazione esterno denominato `connections.config`.  
  
```  
<?xml version='1.0' encoding='utf-8'?>  
<configuration>  
    <connectionStrings configSource="connections.config"/>  
</configuration>  
```  
  
## Recupero delle stringhe di connessione in fase di esecuzione  
 In .NET Framework 2.0 sono state introdotte nuove classi nello spazio dei nomi <xref:System.Configuration> per semplificare il recupero delle stringhe di connessione dai file di configurazione in fase di esecuzione.  È possibile recuperare una stringa di connessione a livello di codice in base al nome o al nome del provider.  
  
> [!NOTE]
>  Il file **machine.config** include anche una sezione **connectionStrings** contenente le stringhe di connessione usate da Visual Studio.  Se le stringhe di connessione vengono recuperate in base al nome del provider dal file **app.config** in un'applicazione Windows, vengono caricate dapprima le stringhe di connessione presenti in **machine.config** e quindi le voci di **app.config**.  L'aggiunta di **clear** immediatamente dopo l'elemento **connectionStrings** consente di rimuovere tutti i riferimenti ereditati dalla struttura dati in memoria, in modo che vengano considerate solo le stringhe di connessione definite nel file **app.config** locale.  
  
### Utilizzo delle classi di configurazione  
 A partire da .NET Framework 2.0, quando si usano i file di configurazione nel computer locale, viene usato <xref:System.Configuration.ConfigurationManager> al posto dell'oggetto <xref:System.Configuration.ConfigurationSettings> deprecato.  Per i file di configurazione di ASP.NET, viene usato <xref:System.Web.Configuration.WebConfigurationManager>,  progettato per essere usato con i file di configurazione in un server Web, che consente l'accesso a livello di codice alle sezioni del file di configurazione come **system.web**.  
  
> [!NOTE]
>  L'accesso ai file di configurazione in fase di esecuzione richiede la concessione di autorizzazioni al chiamante. Le autorizzazioni necessarie dipendono dal tipo di applicazione, dal file di configurazione e dal percorso.  Per altre informazioni, vedere [Using the Configuration Classes](../Topic/Using%20the%20Configuration%20Classes.md) e <xref:System.Web.Configuration.WebConfigurationManager> per le applicazioni ASP.NET e <xref:System.Configuration.ConfigurationManager> per le applicazioni Windows.  
  
 È possibile usare <xref:System.Configuration.ConnectionStringSettingsCollection> per recuperare le stringhe di connessione dai file di configurazione dell'applicazione.  Contiene una raccolta di oggetti <xref:System.Configuration.ConnectionStringSettings> ognuno dei quali rappresenta una singola voce della sezione **connectionStrings**.  Le proprietà sono mappate ad attributi di stringa di connessione, consentendo di recuperare una stringa di connessione in base al nome o al nome del provider.  
  
|Proprietà|Descrizione|  
|---------------|-----------------|  
|<xref:System.Configuration.ConnectionStringSettings.Name%2A>|Nome della stringa di connessione.  È mappata all'attributo **name**.|  
|<xref:System.Configuration.ConnectionStringSettings.ProviderName%2A>|Nome completo del provider.  È mappata all'attributo **providerName**.|  
|<xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>|Stringa di connessione.  È mappata all'attributo **connectionString**.|  
  
### Esempio: elenco di tutte le stringhe di connessione  
 In questo esempio viene scorsa la raccolta `ConnectionStringSettings` e vengono visualizzate le proprietà <xref:System.Configuration.ConnectionStringSettings.Name%2A>, <xref:System.Configuration.ConnectionStringSettings.ProviderName%2A> e <xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A> nella finestra della console.  
  
> [!NOTE]
>  System.Configuration.dll non è incluso in tutti i tipi di progetto e potrebbe essere necessario impostare un riferimento a questo file per usare le classi di configurazione.  Il nome e il percorso di un determinato file di configurazione dell'applicazione variano in base al tipo di applicazione e al processo di hosting.  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfig#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfig/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfig#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfig/VB/source.vb#1)]  
  
### Esempio: recupero di una stringa di connessione in base al nome  
 In questo esempio viene illustrato come recuperare una stringa di connessione da un file di configurazione specificandone il nome.  Nel codice viene creato un oggetto <xref:System.Configuration.ConnectionStringSettings> e il parametro di input specificato viene associato al nome <xref:System.Configuration.ConfigurationManager.ConnectionStrings%2A>.  Se non viene trovato alcun nome corrispondente, la funzione restituisce `null` \(`Nothing` in Visual Basic\).  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByName#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByName/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfigByName#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByName/VB/source.vb#1)]  
  
### Esempio: recupero di una stringa di connessione in base al nome del provider  
 In questo esempio viene illustrato come recuperare una stringa di connessione specificando il nome invariabile del provider nel formato *System.Data.ProviderName*.  Il codice consente di scorrere <xref:System.Configuration.ConnectionStringSettingsCollection> e restituisce la stringa di connessione per il primo <xref:System.Configuration.ConnectionStringSettings.ProviderName%2A> trovato.  Se il nome del provider non viene trovato, la funzione restituisce `null` \(`Nothing` in Visual Basic\).  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/VB/source.vb#1)]  
  
## Crittografia di sezioni dei file di configurazione tramite configurazione protetta  
 In ASP.NET 2.0 è stata introdotta una nuova funzionalità, denominata *configurazione protetta*, che consente di crittografare le informazioni riservate in un file di configurazione.  Sebbene sia stata progettata principalmente per ASP.NET, questa funzionalità può essere usata anche per crittografare sezioni dei file di configurazione nelle applicazioni Windows.  Per una descrizione dettagliata delle funzionalità di configurazione protetta, vedere [Encrypting Configuration Information Using Protected Configuration](../Topic/Encrypting%20Configuration%20Information%20Using%20Protected%20Configuration.md).  
  
 Nel frammento di file di configurazione seguente è illustrata la sezione **connectionStrings** dopo la crittografia.  Nella sezione **configProtectionProvider** è specificato il provider di configurazione protetta usato per crittografare e decrittografare le stringhe di connessione.  La sezione **EncryptedData** contiene il testo crittografato.  
  
```  
<connectionStrings configProtectionProvider="DataProtectionConfigurationProvider">  
  <EncryptedData>  
    <CipherData>  
      <CipherValue>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAH2... </CipherValue>  
    </CipherData>  
  </EncryptedData>  
</connectionStrings>  
```  
  
 Quando la stringa di connessione crittografata viene recuperata in fase di esecuzione, in .NET Framework viene usato il provider specificato per decrittografare **CipherValue** e renderlo disponibile per l'applicazione.  Non è necessario scrivere codice aggiuntivo per gestire il processo di decrittografia.  
  
### Provider di configurazione protetta  
 I provider di configurazione protetta sono registrati nella sezione **configProtectedData** del file **machine.config** nel computer locale, come illustrato nel frammento seguente, in cui sono indicati i due provider di configurazione protetta disponibili in .NET Framework.  I valori mostrati sono stati troncati per facilitarne la lettura.  
  
```  
<configProtectedData defaultProvider="RsaProtectedConfigurationProvider">  
  <providers>  
    <add name="RsaProtectedConfigurationProvider"   
      type="System.Configuration.RsaProtectedConfigurationProvider, ... />  
    <add name="DataProtectionConfigurationProvider"   
      type="System.Configuration.DpapiProtectedConfigurationProvider, ... />  
  </providers>  
</configProtectedData>  
```  
  
 È possibile configurare altri provider di configurazione protetta aggiungendoli al file **machine.config**.  È inoltre possibile creare un proprio provider di configurazione protetta ereditando dalla classe base astratta <xref:System.Configuration.ProtectedConfigurationProvider>.  La tabella seguente descrive i due file di configurazione inclusi in .NET Framework.  
  
|Provider|Descrizione|  
|--------------|-----------------|  
|<xref:System.Configuration.RSAProtectedConfigurationProvider>|Usa l'algoritmo di crittografia RSA per crittografare e decrittografare i dati.  L'algoritmo RSA può essere usato per la crittografia a chiave pubblica e per le firme digitali.  È anche noto come crittografia a "chiave pubblica" o asimmetrica perché impiega due chiavi diverse.  È possibile usare [ASP.NET IIS Registration Tool \(Aspnet\_regiis.exe\)](../Topic/ASP.NET%20IIS%20Registration%20Tool%20\(Aspnet_regiis.exe\).md) per crittografare le sezioni di un file Web.config e gestire le chiavi di crittografia.  In ASP.NET il file di configurazione viene decrittografato al momento dell'elaborazione.  L'identità dell'applicazione ASP.NET deve disporre di accesso in lettura alla chiave di crittografia usata per crittografare e decrittografare le sezioni crittografate.|  
|<xref:System.Configuration.DPAPIProtectedConfigurationProvider>|Usa DPAPI \(Data Protection API\) di Windows per crittografare le sezioni di configurazione.  Usa i servizi di crittografia incorporati di Windows e può essere configurato per la protezione specifica del computer o specifica dell'account utente.  La protezione specifica del computer risulta utile quando più applicazioni sullo stesso server devono condividere informazioni.  La protezione specifica dell'account utente può essere usata con i servizi eseguiti con un'identità utente specifica, ad esempio un ambiente di hosting condiviso.  Ogni applicazione viene eseguita con un'identità distinta, limitando l'accesso a risorse quali file e database.|  
  
 Entrambi i provider offrono una crittografia avanzata per i dati.  Se tuttavia si prevede di usare lo stesso file di configurazione crittografato in più server, ad esempio una Web farm, solo `RsaProtectedConfigurationProvider` consente di esportare le chiavi di crittografia usate per crittografare i dati e importarle in un altro server.  Per altre informazioni, vedere [Importing and Exporting Protected Configuration RSA Key Containers](../Topic/Importing%20and%20Exporting%20Protected%20Configuration%20RSA%20Key%20Containers.md).  
  
### Utilizzo delle classi di configurazione  
 Lo spazio dei nomi <xref:System.Configuration> fornisce classi per specificare le impostazioni di configurazione a livello di codice.  La classe <xref:System.Configuration.ConfigurationManager> fornisce accesso a file di configurazione del computer, dell'applicazione e dell'utente.  Se si crea un'applicazione ASP.NET, è possibile usare la classe <xref:System.Web.Configuration.WebConfigurationManager>, che fornisce la stessa funzionalità consentendo anche di accedere a impostazioni che sono univoche per le applicazioni ASP.NET, ad esempio quelle disponibili in **\<system.web\>**.  
  
> [!NOTE]
>  Lo spazio dei nomi <xref:System.Security.Cryptography> contiene classi che forniscono opzioni aggiuntive per la crittografia e la decrittografia dei dati.  Usare queste classi se si richiedono servizi di crittografia che non sono disponibili tramite configurazione protetta.  In alcuni casi si tratta di wrapper presenti nelle CryptoAPI di Microsoft non gestite, in altri semplicemente di implementazioni gestite.  Per altre informazioni, vedere [Cryptographic Services](http://msdn.microsoft.com/it-it/68a1e844-c63c-44af-9247-f6716eb23781).  
  
### Esempio di App.config  
 In questo esempio viene illustrato come attivare e disattivare la crittografia della sezione **connectionStrings** in un file **app.config** per un'applicazione Windows.  La procedura assume il nome dell'applicazione come argomento, ad esempio "MyApplication.exe".  Il file **app.config** verrà quindi crittografato e copiato nella cartella che contiene il file eseguibile con il nome "MyApplication.exe.config".  
  
> [!NOTE]
>  La stringa di connessione può essere decrittografata solo nel computer in cui è stata crittografata.  
  
 Nel codice viene usato il metodo <xref:System.Configuration.ConfigurationManager.OpenExeConfiguration%2A> per aprire il file **app.config** per la modifica, mentre il metodo <xref:System.Configuration.ConfigurationManager.GetSection%2A> restituisce la sezione **connectionStrings**.  Viene quindi controllata la proprietà <xref:System.Configuration.SectionInformation.IsProtected%2A>, con una chiamata a <xref:System.Configuration.SectionInformation.ProtectSection%2A> per crittografare la sezione, se non è crittografata.  Il metodo <xref:System.Configuration.SectionInformation.UnProtectSection%2A> viene richiamato per decrittografare la sezione.  Il metodo <xref:System.Configuration.Configuration.Save%2A> completa l'operazione e salva le modifiche.  
  
> [!NOTE]
>  È necessario impostare un riferimento a `System.Configuration.dll` nel progetto affinché il codice venga eseguito.  
  
 [!code-csharp[DataWorks ConnectionStrings.Encrypt#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStrings.Encrypt/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStrings.Encrypt#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStrings.Encrypt/VB/source.vb#1)]  
  
### Esempio di Web.config  
 In questo esempio viene usato il metodo <xref:System.Web.Configuration.WebConfigurationManager.OpenWebConfiguration%2A> di `WebConfigurationManager`.  Si noti che in questo caso è possibile specificare il percorso relativo del file **Web.config** usando una tilde.  Il codice richiede un riferimento alla classe `System.Web.Configuration`.  
  
 [!code-csharp[DataWorks ConnectionStringsWeb.Encrypt#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringsWeb.Encrypt/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringsWeb.Encrypt#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringsWeb.Encrypt/VB/source.vb#1)]  
  
 Per altre informazioni sulla protezione di applicazioni ASP.NET, vedere la [NIB: ASP.NET Security](http://msdn.microsoft.com/it-it/04b37532-18d9-40b4-8e5f-ee09a70b311d) e [panoramica delle procedure di sicurezza consigliate per ASP.NET 2.0](http://go.microsoft.com/fwlink/?LinkId=59997) sul sito Web ASP.NET Developer Center.  
  
## Vedere anche  
 [Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md)   
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)   
 [Using the Configuration Classes](../Topic/Using%20the%20Configuration%20Classes.md)   
 [Configurazione di app](../../../../docs/framework/configure-apps/index.md)   
 [ASP.NET Web Site Administration](../Topic/ASP.NET%20Web%20Site%20Administration.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)