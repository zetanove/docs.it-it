---
title: "Application Settings Architecture | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "application settings [Windows Forms], architecture"
ms.assetid: c8eb2ad0-fac6-4ea2-9140-675a4a44d562
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Application Settings Architecture
In questo argomento viene descritto il funzionamento dell'architettura Impostazioni applicazione e ne vengono analizzate alcune funzioni avanzate, quali i raggruppamenti di impostazioni e le chiavi delle impostazioni.  
  
 L'architettura Impostazioni applicazione supporta la definizione di impostazioni fortemente tipizzate con ambito di applicazione o utente, nonché la persistenza delle impostazioni tra le varie sessioni dell'applicazione.  Fornisce un motore di persistenza predefinito per il salvataggio e il caricamento delle impostazioni nel\/dal file system locale.  L'architettura definisce inoltre interfacce che consentono di fornire un motore di persistenza personalizzato.  
  
 Vengono fornite interfacce che consentono a componenti personalizzati di rendere persistenti le rispettive impostazioni quando vengono utilizzati in un'applicazione.  Mediante le chiavi delle impostazioni, i componenti possono tenere separate le impostazioni di più istanze del componente.  
  
## Definizione delle impostazioni  
 L'architettura Impostazioni applicazione viene utilizzata sia in [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] che in Windows Form e contiene diverse classi base condivise in entrambi gli ambienti.  La classe più importante è <xref:System.Configuration.SettingsBase>, che consente l'accesso alle impostazioni mediante una raccolta e fornisce metodi di basso livello per il caricamento e il salvataggio delle impostazioni.  In ogni ambiente viene implementata una classe specifica derivata dalla classe base <xref:System.Configuration.SettingsBase> per arricchire l'ambiente stesso di ulteriori funzionalità delle impostazioni.  In un'applicazione basata su Windows Form tutte le impostazioni dell'applicazione devono essere definite su una classe derivata dalla classe <xref:System.Configuration.ApplicationSettingsBase> e ciò aggiunge le funzionalità seguenti alla classe base:  
  
-   Operazioni di caricamento e salvataggio di alto livello  
  
-   Supporto per impostazioni con ambito di utente  
  
-   Ripristino dei valori predefiniti delle impostazioni dell'utente  
  
-   Aggiornamento delle impostazioni da una versione precedente dell'applicazione  
  
-   Convalida delle impostazioni, prima della modifica o prima del salvataggio  
  
 È possibile descrivere le impostazioni utilizzando alcuni attributi definiti nello spazio dei nomi <xref:System.Configuration>. Per ulteriori informazioni, vedere [Application Settings Attributes](../../../../docs/framework/winforms/advanced/application-settings-attributes.md).  Quando si definisce un'impostazione, è necessario applicarla con la classe <xref:System.Configuration.ApplicationScopedSettingAttribute> oppure con la classe <xref:System.Configuration.UserScopedSettingAttribute>, che descrive se l'impostazione si applica all'intera applicazione o solo all'utente corrente.  
  
 Nell'esempio di codice riportato di seguito viene definita una classe di impostazioni personalizzata con una sola impostazione, `BackgroundColor`.  
  
 [!code-csharp[ApplicationSettings.Create#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/MyAppSettings.cs#1)]
 [!code-vb[ApplicationSettings.Create#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/MyAppSettings.vb#1)]  
  
## Persistenza delle impostazioni  
 La classe <xref:System.Configuration.ApplicationSettingsBase> non esegue la persistenza o il caricamento delle impostazioni. Tale operazione è effettuata dal provider di impostazioni, una classe che deriva da <xref:System.Configuration.SettingsProvider>.  Se una classe derivata dalla classe <xref:System.Configuration.ApplicationSettingsBase> non specifica un provider di impostazioni mediante la classe <xref:System.Configuration.SettingsProviderAttribute>, viene utilizzato il provider predefinito <xref:System.Configuration.LocalFileSettingsProvider>.  
  
 Il sistema di configurazione reso disponibile in origine con [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] supporta la fornitura di dati di configurazione dell'applicazione statici mediante il file machine.config del computer locale o in un file `app.`exe.config da distribuire con l'applicazione.  La classe <xref:System.Configuration.LocalFileSettingsProvider> espande tale supporto nativo nei modi seguenti:  
  
-   È possibile archiviare le impostazioni con ambito di applicazione nel file machine.config o `app.`exe.config.  Il file machine.config è sempre di sola lettura mentre `app`.exe.config è di sola lettura per gran parte delle applicazioni per motivi di sicurezza.  
  
-   Le impostazioni possono essere archiviate con ambito di utente in file `app`.exe.config e in tal caso sono considerate come valori predefiniti statici.  
  
-   Le impostazioni con ambito di utente non predefinite sono archiviate in un nuovo file, *utente*.config, dove *utente* è il nome dell'utente che esegue l'applicazione al momento.  È possibile specificare un valore predefinito per un'impostazione con ambito di utente con <xref:System.Configuration.DefaultSettingValueAttribute>.  Poiché le impostazioni con ambito di utente subiscono spesso modifiche durante l'esecuzione dell'applicazione, il file `user`.config è sempre accessibile in lettura e scrittura.  
  
 In tutti e tre i file di configurazione le impostazioni sono archiviate in formato XML.  L'elemento XML superiore per le impostazioni con ambito di applicazione è `<appSettings>`, mentre `<userSettings>` è utilizzato per impostazioni con ambito di utente.  Un file `app`.exe.config contenente impostazioni con ambito sia di applicazione sia di utente si presenta come segue:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
    <configSections>  
        <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >  
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
        </sectionGroup>  
        <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >  
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />  
        </sectionGroup>  
    </configSections>  
    <applicationSettings>  
        <WindowsApplication1.Properties.Settings>  
            <setting name="Cursor" serializeAs="String">  
                <value>Default</value>  
            </setting>  
            <setting name="DoubleBuffering" serializeAs="String">  
                <value>False</value>  
            </setting>  
        </WindowsApplication1.Properties.Settings>  
    </applicationSettings>  
    <userSettings>  
        <WindowsApplication1.Properties.Settings>  
            <setting name="FormTitle" serializeAs="String">  
                <value>Form1</value>  
            </setting>  
            <setting name="FormSize" serializeAs="String">  
                <value>595, 536</value>  
            </setting>  
        </WindowsApplication1.Properties.Settings>  
    </userSettings>  
</configuration>  
```  
  
 Per la definizione degli elementi all'interno della sezione relativa a Impostazioni applicazione di un file di configurazione, vedere [Schema Application Settings](../../../../docs/framework/configure-apps/file-schema/application-settings-schema.md).  
  
### Associazione delle impostazioni  
 L'architettura Impostazioni applicazione utilizza l'architettura di associazione dati di Windows Form per consentire la comunicazione bidirezionale degli aggiornamenti delle impostazioni tra i relativi componenti e oggetti.  Se si utilizza Visual Studio per creare le impostazioni delle applicazioni e assegnarle alle proprietà dei componenti, queste associazioni verranno generate automaticamente.  
  
 Un'impostazione dell'applicazione può essere associata soltanto a un componente che supporta l'interfaccia <xref:System.Windows.Forms.IBindableComponent>.  Il componente, inoltre, deve implementare un evento di modifica per una specifica proprietà associata oppure deve notificare alla funzione Impostazioni applicazione che la proprietà è stata modificata tramite l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>.  Se il componente non implementa <xref:System.Windows.Forms.IBindableComponent> e l'associazione viene eseguita tramite Visual Studio, le proprietà associate verranno inizialmente impostate ma non verranno aggiornate.  Se il componente implementa <xref:System.Windows.Forms.IBindableComponent> ma non supporta le notifiche per la modifica delle proprietà, l'associazione non verrà aggiornata nel file delle impostazioni quando la proprietà viene modificata.  
  
 Alcuni componenti Windows Form, ad esempio <xref:System.Windows.Forms.ToolStripItem>, non supportano le associazioni delle impostazioni.  
  
### Serializzazione delle impostazioni  
 Quando <xref:System.Configuration.LocalFileSettingsProvider> deve salvare le impostazioni su disco, esegue le azioni seguenti:  
  
1.  Utilizza la reflection per esaminare tutte le proprietà definite sulla classe derivata da <xref:System.Configuration.ApplicationSettingsBase>, trovando quelle applicate con la classe <xref:System.Configuration.ApplicationScopedSettingAttribute> o <xref:System.Configuration.UserScopedSettingAttribute>.  
  
2.  Serializza la proprietà su disco.  Tenta in primo luogo di chiamare il metodo <xref:System.ComponentModel.TypeConverter.ConvertToString%2A> o <xref:System.ComponentModel.TypeConverter.ConvertFromString%2A> sulla classe associata <xref:System.ComponentModel.TypeConverter> del tipo.  Se il tentativo non riesce, utilizza la serializzazione XML.  
  
3.  Stabilisce un'associazione tra impostazioni e file di destinazione, in base all'attributo dell'impostazione.  
  
 Se si implementa una propria classe di impostazioni, è possibile utilizzare <xref:System.Configuration.SettingsSerializeAsAttribute> per contrassegnare un'impostazione per la serializzazione binaria o personalizzata mediante l'enumerazione <xref:System.Configuration.SettingsSerializeAs>.  Per ulteriori informazioni sulla creazione di una propria classe di impostazioni nel codice, vedere [How to: Create Application Settings](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md).  
  
### Posizioni dei file delle impostazioni  
 La posizione dei file `app`.exe.config e *utente*.config dipende dalla modalità di installazione dell'applicazione.  Per un'applicazione basata su Windows Form copiata nel computer locale, il file `app`.exe.config si troverà nella stessa directory della directory di base del file eseguibile principale dell'applicazione, mentre *utente*.config risiederà nel percorso specificato dalla proprietà <xref:System.Windows.Forms.Application.LocalUserAppDataPath%2A?displayProperty=fullName>.  Per un'applicazione installata tramite [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)], entrambi i file risiederanno nella directory Dati [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] nel percorso %InstallRoot%\\\\Documents and Settings\\\\*nomeutente*\\Impostazioni locali.  
  
 La posizione di archiviazione dei file è leggermente diversa se l'utente ha attivato i profili comuni in quanto ciò gli consente di definire impostazioni di Windows e di applicazione diverse quando utilizza altri computer all'interno di un dominio.  In tal caso tanto per le applicazioni [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] quanto per quelle non [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] i file `app`.exe.config e *utente*.config verranno archiviati in %InstallRoot%\\\\Documents and Settings\\*nomeutente*\\Dati applicazioni.  
  
 Per ulteriori informazioni sul funzionamento di Impostazioni applicazione con la nuova tecnologia di distribuzione, vedere [ClickOnce and Application Settings](../Topic/ClickOnce%20and%20Application%20Settings.md).  Per ulteriori informazioni sulla directory Dati [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)], vedere [Accesso a dati locali e remoti in applicazioni ClickOnce](../Topic/Accessing%20Local%20and%20Remote%20Data%20in%20ClickOnce%20Applications.md).  
  
## Sicurezza di Impostazioni applicazione  
 La funzione Impostazioni applicazione è stata progettata per il funzionamento in contesti di attendibilità parziale, ovvero in un ambiente limitato che costituisce l'impostazione predefinita per le applicazioni Windows Form accessibili in Internet o in una rete intranet.  Per utilizzare Impostazioni applicazione con il provider di impostazioni predefinito non sono necessarie autorizzazioni speciali oltre all'attendibilità parziale.  
  
 Quando la funzione Impostazioni applicazione viene utilizzata in un'applicazione [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)], il file `user`.config viene archiviato nella directory dei dati di [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)].  La dimensione del file `user`.config dell'applicazione non può superare la quota della directory dei dati impostata da [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)].  Per ulteriori informazioni, vedere [ClickOnce and Application Settings](../Topic/ClickOnce%20and%20Application%20Settings.md).  
  
## Provider di impostazioni personalizzati  
 Nell'architettura Impostazioni applicazione esiste una debole associazione tra la classe wrapper di Impostazioni applicazione, derivata dalla classe <xref:System.Configuration.ApplicationSettingsBase>, e i provider di impostazioni associati, derivati dalla classe <xref:System.Configuration.SettingsProvider>.  Tale associazione è definita solo dalla classe <xref:System.Configuration.SettingsProviderAttribute> applicata alla classe wrapper o alle singole proprietà di questa.  Se non viene specificato espressamente un provider di impostazioni, viene utilizzato il provider predefinito <xref:System.Configuration.LocalFileSettingsProvider>.  Di conseguenza, l'architettura supporta la creazione e l'utilizzo di provider di impostazioni personalizzati.  
  
 Si supponga, ad esempio, di desiderare di sviluppare e utilizzare `SqlSettingsProvider`, un provider che archivi tutti i dati delle impostazioni in un database di Microsoft SQL Server.  La classe derivata da <xref:System.Configuration.SettingsProvider> riceverebbe tali informazioni nel metodo `Initialize` come parametro del tipo <xref:System.Collections.Specialized.NameValueCollection?displayProperty=fullName>.  Si passerebbe quindi a implementare il metodo <xref:System.Configuration.SettingsProvider.GetPropertyValues%2A> per recuperare le impostazioni dall'archivio di dati e <xref:System.Configuration.SettingsProvider.SetPropertyValues%2A> per salvarle.  Il provider è in grado di utilizzare la classe <xref:System.Configuration.SettingsPropertyCollection> fornita a <xref:System.Configuration.SettingsProvider.GetPropertyValues%2A> per determinare nome, tipo e ambito della proprietà, nonché eventuali altri attributi di impostazioni definiti per essa.  
  
 Sarà necessario per il provider eseguire un'implementazione non ovvia di una proprietà e un metodo.  <xref:System.Configuration.SettingsProvider.ApplicationName%2A> è una proprietà astratta della classe <xref:System.Configuration.SettingsProvider>. Programmarla affinché restituisca quanto segue:  
  
 [!code-csharp[ApplicationSettings.Architecture#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Architecture/CS/DummyClass.cs#2)]
 [!code-vb[ApplicationSettings.Architecture#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Architecture/VB/DummyProviderClass.vb#2)]  
  
 La classe derivata, inoltre, deve implementare un metodo `Initialize` che non utilizzi argomenti e non restituisca valori.  Questo metodo non è definito dalla classe <xref:System.Configuration.SettingsProvider>.  
  
 Si implementa infine <xref:System.Configuration.IApplicationSettingsProvider> nel provider per consentire l'aggiornamento delle impostazioni, il ripristino dei valori predefiniti e l'aggiornamento delle applicazioni da una versione all'altra di un'applicazione.  
  
 Terminata l'implementazione e la compilazione del provider, è necessario configurare la classe delle impostazioni in modo che utilizzi tale provider anziché quello predefinito.  Eseguire tale operazione mediante la classe <xref:System.Configuration.SettingsProviderAttribute>.  Se applicato a un'intera classe di impostazioni, il provider viene utilizzato per ogni impostazione definita nella classe. Se applicato a singole impostazioni, l'architettura Impostazioni applicazione utilizza il provider per le impostazioni specificate e la classe <xref:System.Configuration.LocalFileSettingsProvider> per le altre.  Nell'esempio di codice riportato di seguito viene illustrato come configurare la classe delle impostazioni per l'utilizzo del provider personalizzato.  
  
 [!code-csharp[ApplicationSettings.Architecture#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Architecture/CS/DummyClass.cs#1)]
 [!code-vb[ApplicationSettings.Architecture#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Architecture/VB/DummyProviderClass.vb#1)]  
  
 Un provider può essere chiamato da più thread contemporaneamente ma scriverà sempre nella stessa posizione di archiviazione. Di conseguenza, l'architettura Impostazioni applicazione creerà sempre una sola istanza della classe del provider.  
  
> [!IMPORTANT]
>  È necessario accertarsi che il provider sia thread\-safe e che consenta a un solo thread alla volta di scrivere nei file di configurazione.  
  
 Non è necessario che il provider supporti tutti gli attributi delle impostazioni definiti nello spazio dei nomi <xref:System.Configuration?displayProperty=fullName> ma deve almeno supportare le classi <xref:System.Configuration.ApplicationScopedSettingAttribute> e <xref:System.Configuration.UserScopedSettingAttribute> nonché <xref:System.Configuration.DefaultSettingValueAttribute>.  Per gli attributi non supportati, è sufficiente che il provider generi l'errore senza visualizzare avvisi. Non deve produrre un'eccezione.  Se la classe delle impostazioni utilizza una combinazione non valida di attributi, tuttavia, ad esempio applicando <xref:System.Configuration.ApplicationScopedSettingAttribute> e <xref:System.Configuration.UserScopedSettingAttribute> alla stessa impostazione, il provider deve generare un'eccezione e annullare l'operazione.  
  
## Vedere anche  
 <xref:System.Configuration.ApplicationSettingsBase>   
 <xref:System.Configuration.SettingsProvider>   
 <xref:System.Configuration.LocalFileSettingsProvider>   
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [Application Settings for Custom Controls](../../../../docs/framework/winforms/advanced/application-settings-for-custom-controls.md)   
 [ClickOnce and Application Settings](../Topic/ClickOnce%20and%20Application%20Settings.md)   
 [Schema Application Settings](../../../../docs/framework/configure-apps/file-schema/application-settings-schema.md)