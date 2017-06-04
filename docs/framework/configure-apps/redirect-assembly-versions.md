---
title: "Reindirizzamento delle versioni di assembly | Microsoft Docs"
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
  - "configurazione di applicazioni [.NET Framework]"
  - "assembly [.NET Framework], reindirizzamento dell'associazione"
  - "associazione di assembly, reindirizzamento"
  - "configurazione [.NET Framework], applicazioni"
  - "ridirezionamento associazione assembly a una versione precedente"
ms.assetid: 88fb1a17-6ac9-4b57-8028-193aec1f727c
caps.latest.revision: 26
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 26
---
# Reindirizzamento delle versioni di assembly
È possibile reindirizzare i riferimenti delle associazioni in fase di compilazione agli assembly di .NET Framework, di terze parti o specifici dell'app. È possibile reindirizzare l'app per l'uso di una diversa versione di un assembly in diversi modi: con i criteri editore, tramite un file di configurazione dell'app o mediante il file di configurazione del computer. In questo articolo viene illustrato il funzionamento dell'associazione di assembly in .NET Framework e come può essere configurato.  
  
<a name="BKMK_Assemblyunificationanddefaultbinding"></a>   
## Unificazione e associazione predefinita degli assembly  
 Le associazioni agli assembly .NET Framework vengono talvolta reindirizzate mediante un processo denominato *unificazione degli assembly*. .NET Framework è costituito da una versione di Common Language Runtime e da oltre venti assembly .NET Framework che costituiscono la libreria dei tipi. Questi assembly .NET Framework vengono gestiti dal runtime come una singola unità. Per impostazione predefinita, quando viene avviata un'app, tutti i riferimenti ai tipi nel codice eseguito dal runtime vengono indirizzati agli assembly .NET Framework che hanno lo stesso numero di versione del runtime caricato in un processo. I reindirizzamenti eseguiti con questo modello rappresentano il comportamento predefinito per il runtime.  
  
 Ad esempio, se l'app fa riferimento ai tipi nello spazio dei nomi di System.XML ed è stata compilata usando [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], contiene riferimenti statici all'assembly System.XML assembly fornito con la versione 4.5 del runtime. Per reindirizzare il riferimento dell'associazione in modo da puntare all'assembly System.XML fornito con .NET Framework 4, si possono inserire le informazioni di reindirizzamento nel file di configurazione dell'app. Il reindirizzamento di un'associazione in un file di configurazione per un assembly .NET Framework unificato determina l'annullamento dell'unificazione per tale assembly.  
  
 Inoltre, è possibile reindirizzare manualmente l'associazione di assembly per gli assembly di terze parti in caso di più versioni disponibili.  
  
<a name="BKMK_Redirectingassemblyversionsbyusingpublisherpolicy"></a>   
## Reindirizzamento delle versioni di assembly mediante i criteri editore  
 I fornitori di assembly possono dirigere le app verso una versione più recente di un assembly fornendo un file dei criteri editore con l'assembly aggiornato. Il file dei criteri editore si trova nella Global Assembly Cache e contiene le impostazioni per il reindirizzamento degli assembly.  
  
 Ogni versione *principale*.*secondaria* di un assembly è dotata del relativo file dei criteri editore. Ad esempio, le impostazioni di reindirizzamento dalla versione 2.0.2.222 alla 2.0.3.000 e dalla 2.0.2.321 alla 2.0.3.000 sono contenute nello stesso file, poiché sono associate alla versione 2.0. Tuttavia, un reindirizzamento dalla versione 3.0.0.999 alla versione 4.0.0.000 va inserito nel file per la versione 3.0.999. Ogni versione principale di .NET Framework è dotata del relativo file dei criteri editore.  
  
 Se è disponibile un file dei criteri editore per un assembly, il runtime controlla tale file dopo aver controllato il manifesto dell'assembly e i file di configurazione dell'app. I fornitori usano i file dei criteri editore solo se il nuovo assembly è compatibile con la versione precedente dell'assembly reindirizzato.  
  
 È possibile ignorare i criteri editore per l'app specificando le impostazioni nel file di configurazione dell'app, come illustrato nella sezione [Esclusione dei criteri editore](#bypass_PP).  
  
<a name="BKMK_Redirectingassemblyversionsattheapplevel"></a>   
## Reindirizzamento delle versioni di assembly a livello di app  
 Esistono alcune tecniche differenti per modificare il comportamento di associazione per l'app dal file di configurazione dell'app: è possibile modificare manualmente il file, basarsi sul reindirizzamento dell'associazione automatico oppure specificare il comportamento di associazione ignorando i criteri editore.  
  
### Modifica manuale del file di configurazione di un'app  
 È possibile modificare manualmente il file di configurazione di un'app per risolvere i problemi dell'assembly. Ad esempio, se un fornitore rilascia una versione più recente di un assembly usato dall'app senza fornire i criteri dell'editore, poiché tramite essi non viene garantita la compatibilità con le versioni precedenti, l'app può essere configurata in modo da usare la versione più recente dell'assembly inserendo informazioni di associazione dell'assembly nel file di configurazione dell'app come riportato di seguito.  
  
```  
<dependentAssembly> <assemblyIdentity name="someAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <bindingRedirect oldVersion="7.0.0.0" newVersion="8.0.0.0" /> </dependentAssembly>  
```  
  
### Reindirizzamento di associazione automatico  
 A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], le nuove app desktop destinate a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] usano il reindirizzamento di associazione automatico. Ciò significa che se due componenti fanno riferimento a versioni diverse dello stesso assembly con nome sicuro, il runtime aggiunge automaticamente un reindirizzamento di associazione alla versione più recente dell'assembly nel file di output di configurazione dell'app \(app.config\). Il reindirizzamento esegue l'override dell'unificazione di assembly che in caso contrario potrebbe essere eseguito. Il file app.config di origine non viene modificato. Si supponga, ad esempio, che l'app faccia riferimento direttamente a un componente di .NET Framework fuori banda, ma viene usata una libreria di terze parti destinata a una versione precedente dello stesso componente. Quando si compila l'app, il file di configurazione dell'app di output viene modificato in modo da contenere un reindirizzamento di associazione alla versione più recente del componente. Se si crea un'app Web, si riceve un avviso di compilazione relativo al conflitto di associazione, che a sua volta offre la possibilità di aggiungere il reindirizzamento di associazione necessario al file di configurazione Web di origine.  
  
 Se si aggiungono manualmente reindirizzamenti di associazione al file app.config di origine, in fase di compilazione, [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] tenta di unificare gli assembly in base ai reindirizzamenti di associazione aggiunti. Ad esempio, si inserisce il seguente reindirizzamento dell'associazione per un assembly:  
  
 `<bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0" />`  
  
 Se un altro progetto nell'app fa riferimento alla versione 1.0.0.0 dello stesso assembly, tramite il reindirizzamento di associazione automatico viene aggiunta la seguente voce al file app.config di output in modo da unificare l'app nella versione 2.0.0.0 di questo assembly:  
  
 `<bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" />`  
  
 È possibile abilitare un reindirizzamento di associazione automatico se l'app è destinata alle versioni precedenti di .NET Framework in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)]. È possibile eseguire l'override di questo comportamento predefinito fornendo informazioni per il reindirizzamento di associazione nel file app.config per qualsiasi assembly o disattivare la funzionalità di reindirizzamento di associazione. Per informazioni su come abilitare o disabilitare questa funzionalità, vedere [Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).  
  
<a name="bypass_PP"></a>   
### Esclusione dei criteri editore  
 È possibile eseguire l'override dei criteri editore nel file di configurazione dell'app, se necessario. Ad esempio, le nuove versioni degli assembly, anche se si presentano come compatibili con le versioni precedenti, possono causare problemi per l'esecuzione di un'app. Se si desidera ignorare i criteri dell'editore, aggiungere un elemento [\<publisherPolicy\>](../../../docs/framework/configure-apps/file-schema/runtime/publisherpolicy-element.md) all'elemento [\<dependentAssembly\>](../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md) nel file di configurazione dell'app e impostare l'attributo **apply** su **no**, in modo da eseguire l'override di qualsiasi impostazione **yes** precedente.  
  
 `<publisherPolicy apply="no" />`  
  
 Ignorare quindi i criteri editore per garantire agli utenti il corretto funzionamento dell'app, ma assicurarsi di notificare il problema al fornitore dell'assembly. Se per un assembly è disponibile il file sui criteri editore, il fornitore deve assicurare la compatibilità dell'assembly con le versioni precedenti e garantire il corretto funzionamento della nuova versione per i client.  
  
<a name="BKMK_Redirectingassemblyversionsatthemachinelevel"></a>   
## Reindirizzamento delle versioni di assembly a livello di computer  
 In rari casi, è possibile che l'amministratore del computer desideri impostare tutte le app installate in un computer affinché usino una determinata versione di un assembly. Ad esempio, l'amministratore potrebbe voler usare una particolare versione dell'assembly in tutte le app, perché tale versione è in grado di risolvere un problema di sicurezza. Se un assembly viene reindirizzato in un file di configurazione di un computer, tutte le app presenti sul computer che usano la versione precedente saranno indirizzate all'uso della nuova versione. Il file di configurazione del computer esegue l'override del file di configurazione dell'app e del file dei criteri editore. Questo file si trova nella directory %*percorso installazione runtime*%\\Config. In genere, .NET Framework è installato nella directory %drive%\\Windows\\Microsoft.NET\\Framework.  
  
<a name="BKMK_Specifyingassemblybindinginconfigurationfiles"></a>   
## Specifica dell'associazione di assembly nei file di configurazione  
 Si usa lo stesso formato XML per specificare i reindirizzamenti delle associazioni, indipendentemente dal fatto che venga usato il file di configurazione dell'app, il file di configurazione del computer o il file dei criteri editore. Per reindirizzare una versione di un assembly a un'altra, usare l'elemento [\<bindingRedirect\>](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md). L'attributo **oldVersion** può specificare una singola versione di assembly oppure un insieme di versioni. L'attributo `newVersion` deve specificare una singola versione.  Se si imposta `<bindingRedirect oldVersion="1.1.0.0-1.2.0.0" newVersion="2.0.0.0"/>`, ad esempio, il runtime userà la versione 2.0.0.0 anziché una versione di assembly compresa tra 1.1.0.0 e 1.2.0.0.  
  
 Nell'esempio di codice seguente viene illustrata una varietà di scenari di reindirizzamento dell'associazione. L'esempio specifica un reindirizzamento per un intervallo delle versioni per `myAssembly` e un singolo reindirizzamento dell'associazione per `mySecondAssembly`. L'esempio specifica inoltre che il file dei criteri editore non esegue l'override di reindirizzamenti delle associazioni per `myThirdAssembly`.  
  
 Per associare un assembly, è necessario specificare la stringa "urn:schemas\-microsoft\-com:asm.v1" con l'attributo **xmlns** nel tag [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md).  
  
```  
<configuration> <runtime> <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1"> <dependentAssembly> <assemblyIdentity name="myAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <!-- Assembly versions can be redirected in app, publisher policy, or machine configuration files. --> <bindingRedirect oldVersion="1.0.0.0-2.0.0.0" newVersion="3.0.0.0" /> </dependentAssembly> <dependentAssembly> <assemblyIdentity name="mySecondAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" /> </dependentAssembly> <dependentAssembly> <assemblyIdentity name="myThirdAssembly" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" /> <!-- Publisher policy can be set only in the app configuration file. --> <publisherPolicy apply="no" /> </dependentAssembly> </assemblyBinding> </runtime> </configuration>  
```  
  
### Limitazione delle associazioni di assembly a una versione specifica  
 È possibile usare l'attributo **appliesTo** dell'elemento [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) in un file di configurazione di un'app per reindirizzare un riferimento di un'associazione di assembly a una versione specifica di .NET Framework. Questo attributo facoltativo usa un numero di versione di .NET Framework per indicare la versione a cui deve essere applicato. Se non si specifica l'attributo **appliesTo**, l'elemento [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) viene applicato a tutte le versioni di .NET Framework.  
  
 Per reindirizzare l'associazione di assembly per un assembly .NET Framework 3.5, ad esempio, verrà incluso il codice XML riportato di seguito nel file di configurazione dell'app.  
  
```  
<runtime> <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v3.5"> <dependentAssembly> <!-- assembly information goes here --> </dependentAssembly> </assemblyBinding> </runtime>  
```  
  
 È necessario fornire le informazioni di reindirizzamento nell'ordine della versione. Ad esempio, immettere le informazioni di reindirizzamento dell'associazione dell'assembly per gli assembly .NET Framework 3.5 seguiti dagli assembly .NET Framework 4.5. Immettere infine le informazioni di reindirizzamento dell'binding di assembly per qualsiasi reindirizzamento di assembly .NET Framework in cui non viene usato l'attributo **appliesTo** e che quindi viene applicato a tutte le versioni di .NET Framework. In caso di conflitto nel reindirizzamento, verrà usata la prima istruzione di reindirizzamento corrispondente nel file di configurazione.  
  
 Per reindirizzare, ad esempio, un riferimento a un assembly di .NET Framework 3.5 e un altro riferimento a un assembly di .NET Framework 4, usare il modello illustrato nel frammento di codice che segue.  
  
```  
<assemblyBinding xmlns="..." appliesTo="v3.5 "> <!—.NET Framework version 3.5 redirects here --> </assemblyBinding> <assemblyBinding xmlns="..." appliesTo="v4.0.30319"> <!—.NET Framework version 4.0 redirects here --> </assemblyBinding> <assemblyBinding xmlns="..."> <!-- redirects meant for all versions of the runtime --> </assemblyBinding>  
```  
  
## Vedere anche  
 [Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)   
 [Elemento \<bindingRedirect\>](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md)   
 [Autorizzazione di sicurezza per il reindirizzamento delle versioni di assembly](../../../docs/framework/configure-apps/assembly-binding-redirection-security-permission.md)   
 [Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Configurazione di app](../../../docs/framework/configure-apps/index.md)   
 [Configurazione di app .NET Framework](http://msdn.microsoft.com/it-it/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md)   
 [Procedura: creare criteri editore](../../../docs/framework/configure-apps/how-to-create-a-publisher-policy.md)