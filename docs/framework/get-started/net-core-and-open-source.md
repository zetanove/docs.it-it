---
title: "Componenti di base e open-source di .NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 6
---
# Componenti di base e open-source di .NET
.NET Core è una versione modulare di .NET Framework progettata in modo da garantire la portabilità tra piattaforme per consentire il riutilizzo e la condivisione del codice. .NET Core sarà inoltre open source e accetterà i contributi della community. In questo argomento viene data risposta ad alcune domande comuni su .NET Core e su come accedere e contribuire ai pacchetti open source.  
  
<a name="BKMK_WhatisNETCore"></a>   
## Informazioni su .NET Core  
 Come accennato in precedenza, .NET Core è una versione modulare di .NET Framework progettata per garantire la portabilità tra piattaforme.  
  
 La portabilità tra piattaforme è data dal fatto che, nonostante sia un sottoinsieme della versione completa di .NET Framework, .NET Core offre le funzionalità chiave per implementare le funzionalità dell'app necessarie e riutilizzare questo codice indipendentemente dalla piattaforma di destinazione. In passato, nelle versioni di .NET per le diverse piattaforme mancava la funzionalità condivisa per attività chiave, ad esempio per la lettura di file locali. Con .NET Core è possibile predisporre app destinate a piattaforme Microsoft quali quella Windows desktop tradizionale, oltre che quelle per Windows Phone e dispositivi Windows. Se usato con strumenti di terze parti, come Xamarin, .NET Core deve garantire la portabilità con i dispositivi iOS e Android. A breve, inoltre, .NET Core sarà disponibile per i sistemi operativi Mac e Linux e consentirà di eseguire app Web anche in tali sistemi.  
  
 .NET Core è modulare perché viene rilasciato tramite NuGet in pacchetti di assembly di dimensioni ridotte. Invece di un unico assembly grande contenente la maggior parte delle funzionalità di base, .NET Core è disponibile sotto forma di pacchetti più piccoli incentrati sulle funzionalità. Costituisce quindi la base per un modello di sviluppo più agile in quanto consente di scegliere le singole funzionalità necessarie per le app e le librerie. Per altre informazioni sui pacchetti .NET rilasciati su NuGet, vedere [.NET Framework e rilascio fuori programma](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md).  
  
 Le seguenti sono domande frequenti su .NET Core.  
  
### In che modo è possibile sfruttare al meglio .NET Core?  
 Per sfruttare al meglio .NET Core e massimizzare il riutilizzo del codice con app esistenti, è consigliabile usare progetti di app universali e librerie di classi portabili \(PCL, Portable Class Library\), nonché separare la logica di business dal codice specifico della piattaforma. Per facilitare la migrazione delle app a .NET Core, è possibile scegliere tra le architetture MVC \(Model\-View\-Controller\) e MVVM \(Model View\-ViewModel\).  
  
### In che modo .NET Core influisce sulla compatibilità e sulla distribuzione?  
 Sono disponibili diversi scenari di distribuzione, ma in ogni caso la distribuzione dovrebbe risultare agevole. .NET Framework verrà distribuito con Windows e aggiornato tramite Microsoft Update esattamente come accade oggi. In alcuni casi l'app si baserà su questa distribuzione su disco di .NET Framework, mentre in altri sugli assembly .NET distribuiti con il pacchetto dell'app. La compatibilità da una versione all'altra costituisce inoltre ancora una priorità per .NET Framework, di conseguenza se l'app viene eseguita in una versione più recente di un assembly rispetto a quella con cui è stata compilata, non dovrebbero verificarsi problemi di funzionamento.  
  
|Scenario|Distribuzione|  
|--------------|-------------------|  
|App desktop di Windows e ASP.NET eseguite in computer Windows|La distribuzione è identica a quella attuale. Un'app si basa sull'installazione di .NET Framework disponibile nel server o nel computer dell'utente. Se .NET Framework non è installato, verrà chiesto di installarlo. In alternativa, è possibile concatenare un'installazione di .NET con l'app. Se si usano assembly di .NET Core non inclusi in .NET Framework, tali assembly vengono inclusi nel pacchetto dell'app. Se inoltre la stessa app fa riferimento a due versioni dello stesso assembly, l'app verrà reindirizzata automaticamente a quella più recente. Per altre informazioni, vedere [Reindirizzamento delle versioni di assembly a livello di app](../../../docs/framework/configure-apps/redirect-assembly-versions.md#BKMK_Redirectingassemblyversionsattheapplevel) e [Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).<br /><br /> Per altre informazioni sulla distribuzione di .NET, vedere [Guida alla distribuzione per gli sviluppatori](../../../docs/framework/deployment/deployment-guide-for-developers.md).|  
|App di Windows e Windows Phone disponibili tramite Windows Store e Windows Phone Store|La distribuzione è analoga a quella attuale e le app usano gli assembly di .NET Framework inclusi con il sistema operativo. Se l'app usa la funzionalità rilasciata in un assembly di .NET Core non incluso in .NET Framework, l'assembly verrà incluso nel pacchetto dell'app. Se l'app fa riferimento a più versioni dello stesso assembly, l'app userà automaticamente quella più recente.|  
|App di ASP.NET Core 5.0|Gli assembly di .NET Core sono locali dell'app, di conseguenza gli assembly necessari devono essere distribuiti con il pacchetto dell'app. Per altre informazioni su ASP.NET Core 5.0, vedere [Panoramica di ASP.NET 5](http://www.asp.net/vnext/overview/aspnet-vnext/aspnet-5-overview).|  
|App compilate con strumenti Xamarin eseguiti su altre piattaforme|Al momento queste app vengono distribuite con un set semplificato di assembly Mono, forniti con il pacchetto dell'app. Questa situazione potrebbe cambiare via via che più assembly .NET Core diventeranno open source.|  
  
<a name="BKMK_NETCoreOpenSourcePackages"></a>   
## Pacchetti open source di .NET Core  
 In aggiunta alla modularizzazione di .NET Framework, Microsoft mette a disposizione pacchetti open source di .NET Core su[GitHub](https://github.com/) in base alla licenza [MIT](https://github.com/dotnet/corefx/blob/master/LICENSE). Questo significa che è possibile clonare il repository Git, leggere e compilare il codice e inviare richieste pull come con qualsiasi altro pacchetto open source disponibile su GitHub. In considerazione dell'impegno di Microsoft a garantire la qualità e la compatibilità, ogni richiesta pull verrà valutata accuratamente prima di essere accettata. Di seguito sono elencate alcune domande frequenti.  
  
### Come si scarica e si compila il codice?  
 I pacchetti di origine di .NET Core sono archiviati in `GitHub`, che usa `Git` come sistema di controllo del codice sorgente. Per accedere e compilare il codice, è necessario conoscere le funzionalità di base di [Git](http://git-scm.com/), [GitHub](https://github.com/dotnet/corefx) e [Visual Studio](http://msdn.microsoft.com/vstudio/aa718325.aspx). Nei passaggi seguenti verranno comunque fornite informazioni utili, oltre a collegamenti per iniziare.  
  
 Per configurare Git e GitHub, vedere l'articolo relativo alla [configurazione di Git](https://help.github.com/articles/set-up-git/) sul sito GitHub.  
  
 Per accedere al codice di .NET Framework, è necessario biforcare il repository Git che lo contiene e clonarlo nel computer di sviluppo. Per biforcare il codice, passare al repository e fare clic su **Fork** nell'angolo in alto a destra del browser. È possibile clonare la biforcazione usando l'app GitHub oppure dalla riga di nella shell di GitHub. Per clonare il repository nella shell di GitHub, eseguire questo comando:  
  
```  
git clone https://github.com/dotnet/corefx  
```  
  
 Per compilare il codice, è necessario aver installato Visual Studio 2013. È quindi possibile aprire e compilare le soluzioni con Visual Studio 2013 premendo F5 oppure compilarle sulla riga di comando con il prompt dei comandi per gli sviluppatori. Per compilare le soluzioni con il prompt dei comandi, aprire un prompt e passare alla cartella in cui è stato clonato il codice sorgente, quindi digitare:  
  
```  
build.cmd  
  
```  
  
 Per altre informazioni su come accedere al prompt dei comandi per gli sviluppatori, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
### Quali sono le linee guida per l'invio di codice?  
 Prima di poter incorporare il codice nel ramo master, sarà necessario firmare un [contratto di licenza di collaborazione \(CLA, Contributor License Agreement\)](https://cla.dotnetfoundation.org/).  
  
 Vengono accettati i contributi della community creati con il modello Fork e pull. In base a tale modello, è necessario biforcare e clonare il codice prima di inviare una richiesta pull al ramo master di .NET Framework. Per altre informazioni sulle richieste pull, vedere l'articolo relativo all'[uso di richieste pull](https://help.github.com/articles/using-pull-requests/). Per le linee guida dettagliate sull'invio di una richiesta pull, vedere la [guida alla collaborazione su .NET Core](https://github.com/dotnet/corefx/wiki/Contributing).  
  
### Perché la richiesta pull inviata non è stata accettata?  
 In caso di rifiuto di una richiesta, verrà fornita una spiegazione. In generale, è importante sapere che Microsoft tiene particolarmente alla qualità e alla compatibilità del codice. Se la richiesta pull non è stata accettata, è molto probabile che non siano state rispettate le linee guida per la scrittura di codice, che non siano stati eseguiti test adeguati prima di inviare il codice oppure che sia stata compromessa la compatibilità delle API. Le modifiche al codice devono inoltre essere allineate alla guida di orientamento Microsoft per .NET Framework. Per le linee guida sulla scrittura del codice e per altre informazioni, vedere la [guida alla collaborazione su .NET Core](https://github.com/dotnet/corefx/wiki/Contributing).  
  
## Vedere anche  
 [Post di blog su .NET open source](http://blogs.msdn.com/b/dotnet/archive/2014/11/12/net-core-is-open-source.aspx)   
 [Articolo su .NET open source su Curah](https://curah.microsoft.com/254870/net-core-open-source)   
 [Panoramica di ASP.NET 5](http://www.asp.net/vnext/overview/aspnet-vnext/aspnet-5-overview)