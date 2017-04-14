---
title: "Caspol.exe (Code Access Security Policy Tool) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "permission sets, modifying security policy"
  - "security policy [.NET Framework], Code Access Security Policy tool"
  - "enterprise security policy"
  - "referencing code groups and permission sets"
  - "user security policy"
  - "Caspol.exe"
  - "Code Access Security Policy tool"
  - "code groups, modifying security policy"
  - "application development [.NET Framework], security"
  - "machine security policy"
  - "security policy [.NET Framework], modifying"
  - "manually editing security configuration files"
ms.assetid: d2bf6123-7b0c-4e60-87ad-a39a1c3eb2e0
caps.latest.revision: 44
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 43
---
# Caspol.exe (Code Access Security Policy Tool)
Lo strumento Criteri di sicurezza dall'accesso di codice \(Caspol.exe\) consente a utenti e amministratori di modificare i criteri di sicurezza definiti a livello di computer, di utente e di azienda.  
  
> [!IMPORTANT]
>  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Caspol.exe non influisce sui criteri di sicurezza dall'accesso di codice a meno che l'[elemento \<legacyCasPolicy\>](../../../docs/framework/configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md) sia impostato su `true`.  Eventuali impostazioni indicate o modificate da CasPol.exe interesseranno solo le applicazioni per le quali viene scelto esplicitamente di utilizzare i criteri di sicurezza dall'accesso di codice.  Per ulteriori informazioni, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
> [!NOTE]
>  I computer a 64 bit includono sia versioni a 64 che a 32 bit dei criteri di sicurezza.  Per assicurarsi che le modifiche ai criteri vengano applicate sia alle applicazioni a 32 bit che a quelle a 64 bit, eseguire entrambe le versioni di Caspol.exe.  
  
 Lo strumento Criteri di sicurezza dall'accesso di codice viene installato automaticamente con .NET Framework e con Visual Studio.  Caspol.exe è situato in %windir%\\Microsoft.NET\\Framework\\*version* sui sistemi a 32 bit o in %windir%\\Microsoft.NET\\Framework64\\*version* sui sistemi a 64 bit. Ad esempio, il percorso è %windir%\\Microsoft.NET\\Framework64\\v4.030319\\caspol.exe per .NET Framework 4 in un sistema a 64 bit. È possibile installare più versioni dello strumento se nel computer sono in esecuzione side\-by\-side più versioni di .NET Framework.  È possibile eseguire lo strumento dalla directory di installazione.  Tuttavia, è consigliabile utilizzare il [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md), che non richiede di passare alla cartella di installazione.  
  
 Al prompt dei comandi digitare quanto segue:  
  
## Sintassi  
  
```  
  
caspol [options]  
```  
  
#### Parametri  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|**\-addfulltrust** *assembly\_file*<br /><br /> oppure<br /><br /> **\-af** *assembly\_file*|Aggiunge un assembly che implementa un oggetto di sicurezza personalizzato, ad esempio un'autorizzazione o una condizione di appartenenza personalizzata, nell'elenco di assembly completamente attendibili per uno specifico livello di criteri.  L'argomento *assembly\_file* specifica l'assembly da aggiungere.  Il file deve essere firmato con un [nome sicuro](../../../docs/framework/app-domains/strong-named-assemblies.md).  A questo scopo è possibile utilizzare lo [strumento Nome sicuro \(Sn.exe\)](../../../docs/framework/tools/sn-exe-strong-name-tool.md).<br /><br /> Ogni volta che un set di autorizzazioni contenente un'autorizzazione personalizzata viene aggiunto ai criteri, è necessario aggiungere l'assembly che implementa l'autorizzazione personalizzata all'elenco completamente attendibile per tale livello di criteri.  Gli assembly che implementano oggetti di sicurezza personalizzati, quali condizioni di appartenenza o gruppi di codice personalizzati, utilizzati nei criteri di sicurezza, ad esempio i criteri del computer, devono essere sempre aggiunti all'elenco di assembly completamente attendibili. **Caution:**  Se l'assembly che implementa l'oggetto di sicurezza personalizzato fa riferimento ad altri assembly, aggiungere all'elenco di assembly completamente attendibili prima quelli a cui si fa riferimento.  Gli oggetti di sicurezza personalizzati creati con Visual Basic, C\+\+ e JScript fanno riferimento rispettivamente a Microsoft.VisualBasic.dll, Microsoft.VisualC.dll o Microsoft.JScript.dll.  Per impostazione predefinita, questi assembly non sono contenuti nell'elenco degli assembly totalmente attendibili,  per cui è necessario aggiungere l'assembly appropriato all'elenco prima di aggiungere un oggetto di sicurezza personalizzato.  Se questa operazione non riesce si verificheranno problemi nel sistema di sicurezza, provocando il mancato caricamento di tutti gli assembly.  In questa situazione, l'opzione **\-all \-reset** di Caspol.exe non è in grado di ripristinare la sicurezza.  Per ripristinare la sicurezza, modificare manualmente i file di sicurezza per rimuovere l'oggetto di sicurezza personalizzato.|  
|**\-addgroup** {*parent\_label &#124; parent\_name*} *mship pset\_name* \[*flags*\]<br /><br /> oppure<br /><br /> **\-ag** {*parent\_label &#124; parent\_name*} *mship pset\_name* \[*flags*\]|Aggiunge un nuovo gruppo di codice alla gerarchia dei gruppi di codice.  È possibile specificare *parent\_label* oppure *parent\_name*.  L'argomento *parent\_label* specifica l'etichetta \(come 1. o 1.1.\) del gruppo di codice padre del gruppo di codice aggiunto.  L'argomento *parent\_name* specifica il nome del gruppo di codice padre del gruppo di codice aggiunto.  Dal momento che è possibile utilizzare indifferentemente *parent\_label* e *parent\_name*, Caspol.exe deve essere in grado di distinguerli.  Pertanto *parent\_name* non può iniziare con un numero.  Inoltre, *parent\_name* può contenere solo i caratteri dalla A alla Z, i numeri da 0 a 9 e il carattere di sottolineatura.<br /><br /> L'argomento *mship* specifica la condizione di appartenenza del nuovo gruppo di codice.  Per ulteriori informazioni, vedere la tabella degli argomenti *mship* più avanti in questa sezione.<br /><br /> L'argomento *pset\_name* è il nome del set di autorizzazioni che verrà associato al nuovo gruppo di codice.  È inoltre possibile impostare uno o più *flags* per il nuovo gruppo.  Per ulteriori informazioni, vedere la tabella degli argomenti *flags* più avanti in questa sezione.|  
|**\-addpset** {*psfile* &#124; *psfile* p*set\_name*}<br /><br /> oppure<br /><br /> **\-ap** {*named*\_*psfile* &#124; *psfile* *pset\_name*}|Aggiunge ai criteri un nuovo set di autorizzazioni denominato.  Tale set deve essere creato in XML e archiviato in un file XML.  Se il file XML contiene il nome del set di autorizzazioni, va specificato solo tale file \(*psfile*\).  Se il file XML non contiene il nome del set di autorizzazioni, è necessario specificare sia il nome del file XML \(*psfile*\) che il nome del set di autorizzazioni \(*pset\_name*\).<br /><br /> Tutte le autorizzazioni utilizzate in un set di autorizzazioni devono essere definite in assembly contenuti nella Global Assembly Cache.|  
|**\-a**\[**ll**\]|Indica che tutte le opzioni specificate dopo questa verranno applicate ai criteri definiti a livello di computer, di utente e di azienda.  L'opzione **\-all** fa sempre riferimento ai criteri dell'utente correntemente connesso al sistema.  Per far riferimento ai criteri relativi a un utente diverso da quello corrente, vedere l'opzione **\-customall**.|  
|**\-chggroup** {*label &#124;name*} {*mship* &#124; *nome\_set\_autorizzazioni* &#124;<br /><br /> *flags* `}`<br /><br /> oppure<br /><br /> **\-cg** {*label &#124;name*} {*mship* &#124; *nome\_set\_autorizzazioni* &#124;<br /><br /> *flags* `}`|Modifica la condizione di appartenenza, il set di autorizzazioni o l'impostazione dei flag **exclusive**, **levelfinal**, **name** o **description** di un gruppo di codice.  È possibile specificare l'argomento *label* o *name*.  L'argomento *label* specifica l'etichetta \(ad esempio 1. o 1.1.\) del gruppo di codice.  L'argomento *name* specifica il nome del gruppo di codice da modificare.  Dal momento che è possibile utilizzare indifferentemente *label* o *name*, Caspol.exe deve essere in grado di distinguerli.  Pertanto *name* non può iniziare con un numero.  Inoltre, *name* può contenere solo i caratteri dalla A alla Z, i numeri da 0 a 9 e il carattere di sottolineatura.<br /><br /> L'argomento *pset\_name* specifica il nome del set di autorizzazioni da associare al gruppo di codice.  Per informazioni sugli argomenti *mship* e *flags*, vedere le tabelle più avanti in questa sezione.|  
|**\-chgpset**  *fpsfile pset\_name*<br /><br /> oppure<br /><br /> **\-cp** *psfile pset\_name*|Modifica un set di autorizzazioni denominato.  L'argomento *psfile* fornisce la nuova definizione per il set di autorizzazioni. Si tratta di un file di set di autorizzazioni serializzato in formato XML.  L'argomento *pset\_name* specifica il nome del set di autorizzazioni che si desidera modificare.|  
|**\-customall**  *path*<br /><br /> oppure<br /><br /> **\-ca**  *path*|Indica che tutte le opzioni specificate dopo questa verranno applicate ai criteri definiti a livello di computer e di azienda, nonché ai criteri personalizzati definiti a livello di uno specifico utente.  È necessario specificare il percorso del file di configurazione della sicurezza utente personalizzata mediante l'argomento *path*.|  
|**\-cu**\[**stomuser**\] *path*|Consente di amministrare criteri utente personalizzati che non appartengono all'utente per conto del quale Caspol.exe è in esecuzione.  È necessario specificare il percorso del file di configurazione della sicurezza utente personalizzata mediante l'argomento *path*.|  
|**\-enterprise**<br /><br /> oppure<br /><br /> **\-en**|Indica che tutte le opzioni specificate dopo questa verranno applicate ai criteri definiti a livello di azienda.  Gli utenti che non rivestono il ruolo di amministratori all'interno dell'azienda non dispongono di diritti sufficienti per modificare i criteri aziendali, ma possono visualizzarli.  In scenari non aziendali questi criteri, per impostazione predefinita, non interferiscono con i criteri definiti a livello di computer e di utente.|  
|**\-e**\[**xecution**\] {**on** &#124; **off**}|Abilita o disabilita il meccanismo che verifica l'autorizzazione all'esecuzione prima dell'avvio del codice. **Note:**  Questa opzione è stata rimossa in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] e versioni successive.  Per ulteriori informazioni, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).|  
|**\-f**\[**orce**\]|Evita la verifica di compatibilità con l'esecuzione dello strumento e modifica i criteri in base alle specifiche dell'utente.  In genere Caspol.exe verifica se eventuali modifiche apportate ai criteri potrebbero compromettere la sua esecuzione. In questo caso, le modifiche apportate non vengono salvate e viene stampato un messaggio di errore.  Per imporre la modifica dei criteri anche se questo impedirà l'esecuzione di Caspol.exe, utilizzare l'opzione **–force**.|  
|**\-h**\[**elp**\]|Visualizza la sintassi e le opzioni di Caspol.exe.|  
|**\-l**\[**ist**\]|Elenca la gerarchia dei gruppi di codice e i set di autorizzazioni relativi ai criteri definiti a livello di specifico computer, utente o azienda oppure a tutti i livelli.  Viene visualizzata prima l'etichetta del gruppo di codice, seguita dal nome, se non è null.|  
|**\-listdescription**<br /><br /> oppure<br /><br /> **\-ld**|Elenca le descrizioni di tutti i gruppi di codice per il livello di criteri specificato.|  
|**\-listfulltrust**<br /><br /> oppure<br /><br /> **\-lf**|Riporta il contenuto dell'elenco di assembly completamente attendibili per il livello di criteri specificato.|  
|**\-listgroups**<br /><br /> oppure<br /><br /> **\-lg**|Visualizza i gruppi di codice del livello di criteri specificato o di tutti i livelli di criteri.  Viene visualizzata prima l'etichetta del gruppo di codice, seguita dal nome, se non è null.|  
|**\-listpset** o **\-lp**|Visualizza i set di autorizzazioni per il livello di criteri specificato o per tutti i livelli di criteri.|  
|**\-m**\[**achine**\]|Indica che tutte le opzioni specificate dopo questa verranno applicate ai criteri definiti a livello di computer.  Gli utenti che non rivestono il ruolo di amministratori non dispongono di diritti sufficienti per modificare i criteri definiti a livello di computer, ma possono visualizzarli.  Per gli amministratori, **\-machine** è l'impostazione predefinita.|  
|**\-polchgprompt** {**on** &#124; **off**}<br /><br /> oppure<br /><br /> **\-pp** {**on** &#124; **off**}|Abilita o disabilita la visualizzazione di una richiesta di conferma ogni volta che Caspol.exe viene eseguito con un'opzione che causerebbe modifiche ai criteri.|  
|**\-quiet**<br /><br /> oppure<br /><br /> **\-q**|Disabilita temporaneamente la visualizzazione di una richiesta di conferma relativa a un'opzione che causa modifiche ai criteri.  L'impostazione della richiesta di conferma di modifica globale non viene modificata.  Utilizzare questa opzione esclusivamente in singoli comandi per evitare di disabilitare la richiesta di conferma per tutti i comandi Caspol.exe.|  
|**\-r**\[**ecover**\]|Recupera i criteri da un file di backup.  Ogni volta che viene apportata una modifica ai criteri, i criteri precedenti vengono archiviati in un file di backup.|  
|**\-remfulltrust** *assembly\_file*<br /><br /> oppure<br /><br /> **\-rf**  *assembly\_file*|Rimuove un assembly dall'elenco completamente attendibile di un livello di criteri.  È consigliabile effettuare questa operazione se un set di autorizzazioni contenente un'autorizzazione personalizzata non è più utilizzato dai criteri.  È tuttavia opportuno rimuovere dall'elenco completamente attendibile un assembly che implementa un'autorizzazione personalizzata solo se tale assembly non implementa alcuna altra autorizzazione personalizzata correntemente in uso.  Quando si rimuove un assembly dall'elenco, è necessario rimuovere anche eventuali altri assembly da cui esso dipende.|  
|**\-remgroup** {*label &#124;name*}<br /><br /> oppure<br /><br /> **\-rg** {*label &#124; name*}|Rimuove il gruppo di codice specificato in base all'etichetta o al nome.  Se il gruppo di codice specificato presenta gruppi di codice figlio, anche questi verranno automaticamente rimossi.|  
|**\-rempset** *pset\_name*<br /><br /> oppure<br /><br /> **\-rp** *pset\_name*|Rimuove dai criteri il set di autorizzazioni specificato.  L'argomento *pset\_name* indica il set di autorizzazioni da rimuovere.  Tale set viene rimosso solo se non è associato ad alcun gruppo di codice.  I set di autorizzazioni predefiniti \(incorporati\) non possono essere rimossi.|  
|**\-reset**<br /><br /> oppure<br /><br /> **\-rs**|Ripristina lo stato predefinito dei criteri e li rende persistenti su disco.  Questa opzione è utile ogni volta che non è possibile correggere criteri a cui sono state apportate modifiche errate e si desidera ricominciare con i valori di installazione predefiniti.  La reimpostazione può risultare utile anche quando si desidera utilizzare i criteri predefiniti come punto di partenza per apportare modifiche a specifici file di configurazione della sicurezza.  Per ulteriori informazioni, vedere [Modifica manuale dei file di configurazione della sicurezza](#cpgrfcodeaccesssecuritypolicyutilitycaspolexeanchor1).|  
|**\-resetlockdown**<br /><br /> oppure<br /><br /> **\-rsld**|Ripristina una versione più restrittiva dello stato predefinito dei criteri e lo rende persistente su disco. Crea una copia di backup dei criteri precedenti del computer e la rende persistente in un file denominato `security.config.bac`.  I criteri bloccati sono simili a quelli predefiniti, tranne per il fatto che non vengono concesse autorizzazioni al codice proveniente da zone `Local Intranet`, `Trusted Sites` e `Internet` e i gruppi di codice corrispondenti non dispongono di gruppi di codice figlio.|  
|**\-resolvegroup** *assembly\_file*<br /><br /> oppure<br /><br /> **\-rsg**  *assembly\_file*|Mostra i gruppi di codice a cui appartiene un assembly specifico \(*assembly\_file*\).  Per impostazione predefinita, questa opzione visualizza i criteri definiti a livello di computer, utente e azienda a cui appartiene l'assembly.  Per visualizzare solo un livello di criteri, utilizzare questa opzione con l'opzione **\-machine**, **\-user** o **\-enterprise**.|  
|**\-resolveperm** *assembly\_file*<br /><br /> oppure<br /><br /> **\-rsp** *assembly\_file*|Visualizza tutte le autorizzazioni che il livello di criteri di sicurezza specificato, o predefinito, concederebbe all'assembly se fosse consentita l'esecuzione di tale assembly.  L'argomento *assembly\_file* specifica l'assembly.  Se si specifica l'opzione **\-all**, le autorizzazioni per l'assembly verranno calcolate sulla base dei criteri definiti a livello di utente, computer e azienda. In caso contrario, verranno applicate le regole di comportamento predefinite.|  
|**\-s**\[**ecurity**\] {**on** &#124; **off**}|Abilita o disabilita la sicurezza dall'accesso di codice.  Se si specifica l'opzione **\-s off**, la sicurezza basata sui ruoli non viene disabilitata. **Note:**  Questa opzione è stata rimossa in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] e versioni successive.  Per ulteriori informazioni, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md). **Caution:**  Quando la sicurezza per l'accesso al codice è disabilitata, tutte le richieste di accesso avanzate dal codice verranno esaudite.  La disabilitazione della sicurezza dall'accesso di codice rende il sistema vulnerabile agli attacchi di codice dannoso, tra cui virus e programmi distruttivi.  La disabilitazione della sicurezza consente di migliorare le prestazioni ma è un'operazione da effettuare solo quando sono state già adottate altre misure di sicurezza per assicurare che la sicurezza complessiva del sistema non venga compromessa.  Esempi di precauzioni alternative sono la disconnessione da reti pubbliche, la sicurezza fisica dei computer e così via.|  
|**\-u**\[**ser**\]|Indica che tutte le opzioni specificate dopo questa verranno applicate ai criteri definiti a livello dell'utente per conto del quale Caspol.exe è in esecuzione.  Per gli utenti che non rivestono il ruolo di amministratori, **\-user** rappresenta l'opzione predefinita.|  
|**\-?**|Visualizza la sintassi e le opzioni di Caspol.exe.|  
  
 L'argomento *mship* , che specifica la condizione di appartenenza di un gruppo di codice, è utilizzabile con le opzioni **\-addgroup** e **\-chggroup**.  Ogni argomento *mship* viene implementato come classe di .NET Framework.  Per specificare *mship*, utilizzare uno degli argomenti elencati di seguito.  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|**\-allcode**|Specifica tutto il codice.  Per ulteriori informazioni su questa condizione di appartenenza, vedere la [classe AllMembershipCondition](frlrfSystemSecurityPolicyAllMembershipConditionClassTopic).|  
|**\-appdir**|Specifica la directory dell'applicazione.  Se si specifica **\-appdir** come condizione di appartenenza, l'evidenza URL del codice verrà confrontata con l'evidenza della directory dell'applicazione di tale codice.  Se i valori delle evidenze sono identici, questa condizione di appartenenza è soddisfatta.  Per ulteriori informazioni su questa condizione di appartenenza, vedere la [classe ApplicationDirectoryMembershipCondition](frlrfSystemSecurityPolicyApplicationDirectoryMembershipConditionClassTopic).|  
|**\-custom**  *xmlfile*|Aggiunge una condizione di appartenenza personalizzata.  L'argomento obbligatorio *xmlfile* specifica il file XML contenente la serializzazione XML della condizione di appartenenza personalizzata.|  
|**\-hash** *hashAlg* {**\-hex** *hashValue* &#124; **\-file** *assembly\_file*}|Specifica il codice che include l'hash di assembly specificato.  Per utilizzare un hash come condizione di appartenenza di un gruppo di codice, è necessario specificare il valore hash oppure il file di assembly.  Per ulteriori informazioni su questa condizione di appartenenza, vedere la [classe HashMembershipCondition](frlrfSystemSecurityPolicyHashMembershipConditionClassTopic).|  
|**\-pub** { **\-cert** *cert\_file\_name* &#124;<br /><br /> **\-file** *signed\_file\_name* &#124; **\-hex**  *hex\_string*}|Specifica il codice che include l'editore di software specificato, come indicato da un file di certificato, da una firma su un file o dalla rappresentazione esadecimale di un certificato X509.  Per ulteriori informazioni su questa condizione di appartenenza, vedere la [classe PublisherMembershipCondition](frlrfSystemSecurityPolicyPublisherMembershipConditionClassTopic).|  
|**\-site** *website*|Specifica il codice che include il sito di origine specificato.  Di seguito è riportato un esempio.<br /><br /> **\-site** www.proseware.com<br /><br /> Per ulteriori informazioni su questa condizione di appartenenza, vedere la [classe SiteMembershipCondition](frlrfSystemSecurityPolicySiteMembershipConditionClassTopic).|  
|**\-strong \-file** *file\_name* {*name* &#124; **\-noname**} {*version* &#124; **\-noversion**}|Specifica il codice che include un nome sicuro specifico, composto dal nome del file, dal nome dell'assembly sotto forma di stringa e dalla versione dell'assembly nel formato *major*.*minor*.*build*.*revision*.  Di seguito è riportato un esempio.<br /><br /> **\-strong \-file** myAssembly.exe myAssembly 1.2.3.4<br /><br /> Per ulteriori informazioni su questa condizione di appartenenza, vedere la [classe StrongNameMembershipCondition](frlrfSystemSecurityPolicyStrongNameMembershipConditionClassTopic).|  
|**\-url** *URL*|Specifica il codice che deriva dall'URL specificato.  L'URL deve includere un protocollo, quale http:\/\/ o ftp:\/\/.  È inoltre possibile utilizzare un carattere jolly \(\*\) per specificare più assembly da un determinato URL. **Note:**  Poiché un URL può essere identificato utilizzando più nomi, l'utilizzo di un URL come condizione di appartenenza non è un metodo sicuro per determinare l'identità del codice.  Se possibile, è consigliabile utilizzare una condizione di appartenenza con un nome sicuro, una condizione di appartenenza editore o una condizione di appartenenza hash. <br /><br /> Per ulteriori informazioni su questa condizione di appartenenza, vedere la [classe UrlMembershipCondition](frlrfSystemSecurityPolicyURLMembershipConditionClassTopic).|  
|**\-zone** *zonename*|Specifica il codice con la zona di origine specificata.  L'argomento *zonename* può essere impostato su **MyComputer**, **Intranet**, **Trusted**, **Internet** o **Untrusted**.  Per ulteriori informazioni su questa condizione di appartenenza, vedere la classe <xref:System.Security.Policy.ZoneMembershipCondition>.|  
  
 L'argomento *flags*, utilizzabile con le opzioni **\-addgroup** e **\-chggroup**, viene specificato mediante uno degli argomenti elencati di seguito.  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|**\-description "** *description* **"**|Se viene utilizzato con l'opzione **\-addgroup**, specifica la descrizione di un gruppo di codice da aggiungere.  Se viene utilizzato con l'opzione **\-chggroup**, specifica la descrizione di un gruppo di codice da modificare.  L'argomento *description* deve essere racchiuso tra virgolette doppie.|  
|**\-exclusive** {**on**&#124;**off**}|Quando è impostato su **on**, indica che solo il set di autorizzazioni associato al gruppo di codice da aggiungere o modificare verrà considerato quando del codice soddisferà la condizione di appartenenza del gruppo di codice.  Quando questa opzione è impostata su **off**, vengono considerati i set di autorizzazioni di tutti i gruppi di codice corrispondenti nel livello di criteri.|  
|**\-levelfinal** {**on**&#124;**off**}|Quando è impostato su **on**, indica che non verrà considerato alcun livello di criteri inferiore al livello del gruppo di codice aggiunto o modificato.  Questa opzione è in genere utilizzata per i criteri definiti a livello di computer.  Se ad esempio si imposta questo flag per un gruppo di codice a livello di computer ed esiste codice che soddisfa la condizione di appartenenza di tale gruppo di codice, i criteri definiti a livello utente per questo codice non verranno né calcolati né applicati.|  
|**\-name "** *name* **"**|Se viene utilizzato con l'opzione **\-addgroup**, specifica il nome di script di un gruppo di codice da aggiungere.  Se viene utilizzato con l'opzione **\-chggroup**, specifica il nome di script di un gruppo di codice da modificare.  L'argomento *name* deve essere racchiuso tra virgolette doppie.  L'argomento *name* non può iniziare con un numero e può contenere solo i caratteri dalla A alla Z, i numeri da 0 a 9 e il carattere di sottolineatura.  È possibile fare riferimento ai gruppi di codice in base a questo *name* anziché in base all'etichetta numerica.  *name* è inoltre estremamente utile per la creazione di script.|  
  
## Note  
 I criteri di sicurezza vengono espressi mediante tre livelli computer, utente e azienda.  Il set di autorizzazioni che un assembly riceve è determinato dall'intersezione dei set di autorizzazioni consentiti da questi tre livelli di criteri.  Ciascun livello di criteri è rappresentato da una struttura gerarchica di gruppi di codice.  Ciascun gruppo di codice presenta una condizione di appartenenza che determina quale codice appartiene a tale gruppo.  A ciascun gruppo di codice è inoltre associato un set di autorizzazioni denominato.  Questo set di autorizzazioni specifica le autorizzazioni concesse dal runtime al codice che soddisfa la condizione di appartenenza.  Una gerarchia dei gruppi di codice, insieme ai set di autorizzazioni denominati a essa associati, definisce e mantiene ciascun livello dei criteri di sicurezza.  È possibile utilizzare le opzioni**\-user**, **\-customuser**, **\-machine** ed **\-enterprise** per impostare il livello dei criteri di sicurezza.  
  
 Per ulteriori informazioni sui criteri di sicurezza e sulle modalità con cui il runtime determina quali autorizzazioni concedere al codice, vedere [Gestione dei criteri di sicurezza](http://msdn.microsoft.com/it-it/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9).  
  
## Riferimenti a gruppi di codice e a set di autorizzazioni  
 Per facilitare i riferimenti ai gruppi di codice presenti in una gerarchia, l'opzione **\-list** visualizza un elenco con rientri dei gruppi di codice insieme alle corrispondenti etichette numeriche \(1, 1.1, 1.1.1 e così via\).  Anche le altre operazioni da riga di comando relative ai gruppi di codice utilizzano le etichette numeriche per far riferimento a gruppi di codice specifici.  
  
 Ai set di autorizzazioni denominati viene fatto riferimento mediante il nome.  L'opzione **\-list** visualizza l'elenco dei gruppi di codice seguito dall'elenco dei set di autorizzazioni denominati disponibili in tali criteri.  
  
## Comportamento di Caspol.exe  
 Per tutte le opzioni tranne **\-s**\[**ecurity**\] {**on** &#124; **off**} viene utilizzata la versione di. NET Framework con cui è stato installato Caspol.exe.  Se si esegue la versione di Caspol.exe installata con la versione *X* del runtime, le modifiche verranno applicate solo a quella versione.  Eventuali altre installazioni side\-by\-side del runtime non saranno interessate.  Se si esegue Caspol.exe dalla riga di comando, ma non da una directory relativa a una versione specifica del runtime, lo strumento verrà eseguito dalla prima directory della versione del runtime presente nel percorso, generalmente la più recente.  
  
 L'opzione **\-s**\[**ecurity**\] {**on** &#124; **off**} è un'operazione eseguita a livello di computer.  Se si disabilita la sicurezza dall'accesso di codice, termineranno tutti i controlli di sicurezza eseguiti per tutto il codice gestito e tutti gli utenti del computer.  Se sono installate versioni side\-by\-side di .NET Framework, con questo comando verrà disabilitata la sicurezza per ogni versione installata nel computer.  Sebbene l'opzione **\-list** indichi che la sicurezza è disabilitata, nessun altro elemento indica chiaramente agli altri utenti che la sicurezza è stata disabilitata.  
  
 Quando Caspol.exe viene eseguito da un utente che non dispone di diritti amministrativi, tutte le opzioni fanno riferimento ai criteri definiti a livello di utente, se non è specificata l'opzione **\-machine**.  Quando Caspol.exe viene eseguito da un amministratore, tutte le opzioni fanno riferimento ai criteri definiti a livello di computer, se non è specificata l'opzione **\-user**.  
  
 Per consentire l'esecuzione di Caspol.exe, è necessario concedere allo strumento l'equivalente del set di autorizzazioni **Everything**.  Lo strumento dispone di un meccanismo protettivo che impedisce che i criteri vengano modificati in modo da compromettere la concessione delle autorizzazioni necessarie per l'esecuzione.  Se si tenta di apportare modifiche di questo tipo, verrà visualizzato un messaggio indicante che le modifiche richieste per i criteri impedirebbero il corretto funzionamento dello strumento e che pertanto vengono rifiutate.  È possibile disabilitare questo meccanismo protettivo per un determinato comando utilizzando l'opzione **\-force**.  
  
<a name="cpgrfcodeaccesssecuritypolicyutilitycaspolexeanchor1"></a>   
## Modifica manuale dei file di configurazione della sicurezza  
 Sono disponibili tre file di configurazione della sicurezza, corrispondenti ai tre livelli di criteri supportati da Caspol.exe: uno per i criteri a livello di computer, uno per i criteri relativi a un determinato utente e uno per i criteri dell'azienda.  Questi file vengono creati su disco solo quando vengono modificati criteri relativi a computer, utente o azienda utilizzando Caspol.exe.  È possibile utilizzare l'opzione **\-reset** in Caspol.exe per salvare i criteri di sicurezza predefiniti su disco, se necessario.  
  
 Nella maggior parte dei casi la modifica manuale dei file di configurazione della sicurezza non è consigliata.  In alcuni scenari, tuttavia, la modifica di questi file può essere effettivamente necessaria, ad esempio quando un amministratore desidera modificare la configurazione di sicurezza per un particolare utente.  
  
## Esempi  
 **\-addfulltrust**  
  
 Si supponga che un set di autorizzazioni contenente un'autorizzazione personalizzata sia stato aggiunto ai criteri definiti a livello di computer.  Questa autorizzazione personalizzata viene implementata in `MyPerm.exe` e `MyPerm.exe` fa riferimento a classi contenute in `MyOther.exe`.  Entrambi gli assembly dovranno essere aggiunti all'elenco di assembly completamente attendibili.  Il comando che segue aggiunge l'assembly `MyPerm.exe` all'elenco completamente attendibile relativo ai criteri a livello di computer.  
  
```  
caspol -machine -addfulltrust MyPerm.exe  
```  
  
 Il comando che segue aggiunge l'assembly `MyOther.exe` all'elenco completamente attendibile relativo ai criteri a livello di computer.  
  
```  
caspol -machine -addfulltrust MyOther.exe  
```  
  
 **\-addgroup**  
  
 Il comando che segue aggiunge un gruppo di codice figlio alla radice della gerarchia dei gruppi di codice dei criteri definiti a livello di computer.  Il nuovo gruppo di codice appartiene alla zona **Internet** ed è associato al set di autorizzazioni **Execution**.  
  
```  
caspol -machine -addgroup 1.  -zone Internet Execution  
```  
  
 Il comando che segue aggiunge un gruppo di codice figlio che fornisce le autorizzazioni per l'intranet locale alla condivisione \\\\netserver\\netshare.  
  
```  
caspol -machine -addgroup 1. -url \\netserver\netshare\* LocalIntranet  
```  
  
 **\-addpset**  
  
 Il comando che segue aggiunge il set di autorizzazioni `Mypset` ai criteri definiti a livello di utente.  
  
```  
caspol -user -addpset Mypset.xml Mypset  
```  
  
 **\-chggroup**  
  
 Il comando che segue sostituisce il set di autorizzazioni nei criteri definiti a livello di utente del gruppo di codice con etichetta 1.2. con il set di autorizzazioni **Execution**.  
  
```  
caspol -user -chggroup 1.2. Execution  
```  
  
 Il comando che segue modifica la condizione di appartenenza nei criteri predefiniti del gruppo di codice con etichetta 1.2.1. e l'impostazione del flag **exclusive**.  La condizione di appartenenza viene definita come codice originato nella zona **Internet** e viene attivato il flag **exclusive**.  
  
```  
caspol -chggroup 1.2.1. -zone Internet -exclusive on  
```  
  
 **\-chgpset**  
  
 Il comando che segue sostituisce il set di autorizzazioni denominato `Mypset` con il set di autorizzazioni contenuto in `newpset.xml`.  Si noti che l'attuale versione dello strumento non supporta la modifica dei set di autorizzazioni utilizzati dalla gerarchia dei gruppi di codice.  
  
```  
caspol -chgpset Mypset newpset.xml  
```  
  
 **\-force**  
  
 Il comando che segue associa il gruppo di codice radice dei criteri per l'utente \(con etichetta 1\) al set di autorizzazioni denominato **Nothing**.  Questo impedisce l'esecuzione di Caspol.exe.  
  
```  
caspol -force -user -chggroup 1 Nothing  
```  
  
 **\-recover**  
  
 Il comando che segue recupera gli ultimi criteri salvati a livello di computer.  
  
```  
caspol -machine -recover  
```  
  
 **\-remgroup**  
  
 Il comando che segue rimuove il gruppo di codice con etichetta 1.1.  Se tale gruppo di codice presenta gruppi di codice figlio, anche questi verranno eliminati.  
  
```  
caspol -remgroup 1.1.  
```  
  
 **\-rempset**  
  
 Il comando che segue rimuove il set di autorizzazioni **Execution** dai criteri definiti a livello di utente.  
  
```  
caspol -user -rempset Execution  
```  
  
 Il comando che segue rimuove `Mypset` dal livello dei criteri utente.  
  
```  
caspol -rempset MyPset  
```  
  
 **\-resolvegroup**  
  
 Il comando che segue mostra tutti i gruppi di codice dei criteri definiti a livello di computer a cui `myassembly` appartiene.  
  
```  
caspol -machine -resolvegroup myassembly  
```  
  
 Il comando che segue mostra tutti i gruppi di codice dei criteri definiti a livello di computer e di azienda nonché dei criteri personalizzati definiti a livello di utente ai quali `myassembly` appartiene.  
  
```  
caspol -customall "c:\config_test\security.config" -resolvegroup myassembly  
```  
  
 **\-resolveperm**  
  
 Il comando che segue calcola le autorizzazioni di `testassembly` sulla base dei livelli di criteri relativi a computer e utente.  
  
```  
caspol -all -resolveperm testassembly  
```  
  
## Vedere anche  
 [Tools](../../../docs/framework/tools/index.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)