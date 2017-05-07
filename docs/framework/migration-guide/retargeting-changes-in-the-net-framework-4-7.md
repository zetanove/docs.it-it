---
title: Reindirizzamento delle modifiche in .NET Framework 4.7 | Documenti di Microsoft
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes,.NET Framework
- retargeting changes,.NET Framework 4.7
- application compatibility
ms.assetid: d98bf1e3-0017-4933-8e7b-191ac3542fcc
caps.latest.revision: 14
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 2881049ee490bf0abdd8b2f0651ca3703ccae76a
ms.lasthandoff: 04/18/2017

---
# <a name="retargeting-changes-in-the-net-framework-47"></a>Reindirizzamento delle modifiche in .NET Framework 4.7

In rari casi, il reindirizzamento delle modifiche può influire sulle app che vengono ricompilate per .NET Framework 4.7. Non influiscono sui file binari destinati a una versione precedente di .NET Framework ma vengono eseguiti nella versione 4.7. .NET Framework 4.7 include modifiche di reindirizzamento nelle seguenti aree:  

-   [Base](#Core)  
-   [ASP.NET 2.0](#asp) 
-   [Windows Communication Foundation (WCF)](#WCF)  
-   [Windows Presentation Foundation (WPF)](#WPF)
 
 La colonna Ambito nelle tabelle seguenti contiene il significato di ogni modifica:  
  
-   Principale Una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice. Si noti che le modifiche di reindirizzamento non rientrano in questa categoria.  
  
-   Secondaria. Una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.  
  
-   Bordo. Una modifica che influisce sulle app in scenari molto specifici e non comuni.  
  
-   Trasparente. Una modifica che non ha effetti evidenti sullo sviluppatore o sull'utente dell'app. L'app non dovrebbe richiedere variazioni a causa di questa modifica.  
  
## <a name="a-namecore--core"></a><a name="Core" /> Base

| Funzionalità | Modifica | Impatto | Ambito |
|----|----|----|----|
|<xref:System.Security.Cryptography.CspParameters.ParentWindowHandle%2A> | Le applicazioni destinate a .NET Framework 4.6.2 e alle versioni precedenti prevedono che il valore assegnato a questa proprietà sia un <xref:System.IntPtr> nel percorso specificato in memoria in cui si trova il valore HWND.<br/></br>A partire dalle applicazioni destinate a NET Framework 4.7, un'applicazione Windows Forms può impostare il valore di questa proprietà con il codice seguente: <br/><br/>` cspParameters.ParentWindowHandle = form.Handle; ` | Le app che non trovano opportuno questa modifica del comportamento possono rifiutarlo esplicitamente. Analogamente, le applicazioni destinate alle versioni precedenti di .NET Framework ma che vengono eseguite in .NET Framework 4.7 possono acconsentire esplicitamente a questa modifica. Per altre informazioni, vedere [Mitigazione: CspParameters.ParentWindowHandle prevede un HWND](../../../docs/framework/migration-guide/mitigation-cspparameters-parentwindowhandle-expects-an-hwnd.md). | Secondario |
| Serializzazione con <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> | A partire dalle app destinate a .NET Framework 4.7, la serializzazione dei caratteri di controllo con <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> è ora compatibile con ECMAScript V6 e V8 | Questa modifica è conforme allo standard ECMAScript e deve avere un impatto minimo. In caso contrario, è disponibile un commutatore di compatibilità per ripristinare il comportamento precedente. Per altre informazioni, vedere [Mitigazione: Serializzazione dei caratteri di controllo con DataContractJsonSerializer](../../../docs/framework/migration-guide/mitigation-serialization-control-characters.md)  | Microsoft Edge |

## <a name="a-nameasp--aspnet"></a><a name="asp" /> ASP.NET

| Funzionalità  |Modifica  |Impatto | Ambito | 
---------|---------|---------|-----|
Limitazione delle richieste simultanee per sessione | In .NET Framework 4.6.2 e versioni precedenti, ASP.NET esegue in sequenza le richieste con lo stesso <xref:System.Web.SessionState.HttpSessionState.SessionID%2A>, e in ASP.NET viene sempre generato <xref:System.Web.SessionState.HttpSessionState.SessionID%2A> tramite un cookie per impostazione predefinita. Se una pagina impiega molto tempo per il caricamento, premere <kbd>F5</kbd> nel browser peggiora in modo significativo le prestazioni del server.<br/><br/>A partire da .NET Framework 4.7, un contatore tiene traccia delle richieste in coda e termina le richieste quando superano il limite specificato. Il valore predefinito è 50. Se si raggiunge il limite, viene registrato un avviso nel registro eventi e potrebbe essere registrata una risposta HTTP 500 nel registro di IIS.|Questa modifica può migliorare le prestazioni generali del server.<br/><br/>Per ripristinare il comportamento precedente, è possibile aggiungere l'impostazione seguente al file web. config per rifiutare esplicitamente il nuovo comportamento.<br/><br/>`<appSettings>`<br/>&nbsp;&nbsp;&nbsp;`<add key="aspnet:RequestQueueLimitPerSession" value="2147483647"/>`<br/>`</appSettings>` | Microsoft Edge |

## <a name="a-namewcf--windows-communication-foundation"></a><a name="WCF" /> Windows Communication Foundation

| Funzionalità  |Modifica  |Impatto | Ambito | 
---------|---------|---------|-----|
| Protezione dei messaggi WCF | Le applicazioni in esecuzione in .NET Framework 4.7 o versioni successive sono in grado di usare TLS 1.1 e TLS 1.2 nella protezione dei messaggi WCF tramite impostazioni di configurazione dell'applicazione. È una funzionalità che prevede il consenso esplicito; per impostazione predefinita, il supporto per TLS 1.1 e TLS 1.2 nella protezione dei messaggi WCF è disabilitato. | Il comportamento predefinito della protezione dei messaggi WCF rimane invariato. <br/><br/> Per abilitare il supporto per TLS 1.1 e TLS 1.2, aggiungere l'impostazione di configurazione seguente per la sezione [runtime](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) di `app.config` o il file `web.config`:  <br/><br/>`<runtime>` <br/> &nbsp;&nbsp;&nbsp;`<AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;`<br/>&nbsp;&nbsp;&nbsp;`Switch.System.Net.DontEnableSchUseStrongCrypto=false" />`<br/>`</runtime>` | Microsoft Edge |         

## <a name="a-namewpf--windows-presentation-foundation-wpf"></a><a name="WPF" /> Windows Presentation Foundation (WPF)  

| Funzionalità | Modifica | Impatto | Ambito |
|---|---|---|---|
| Allocazione dello spazio del controllo <xref:System.Windows.Controls.Grid> alle colonne a stella | A partire dalle applicazioni destinate a .NET Framework 4.7, WPF sostituisce l'algoritmo usato dal controllo <xref:System.Windows.Controls.Grid> per allocare spazio a \*-columns.md) | Per le applicazioni destinate a versioni di .NET Framework a partire dalla 4.7, questa modifica influisce sulla larghezza effettiva assegnata alle colonne \* in un numero di casi. Se questa modifica non è opportuna, è possibile continuare ad applicare l'algoritmo precedente mediante l'aggiunta di una voce al file di configurazione dell'applicazione. Per altre informazioni, vedere [Mitigazione: Allocazione dello spazio di controllo della griglia alle colonne a stella](../../../docs/framework/migration-guide/mitigation-grid-control.md). | Secondario |
| <xref:System.Windows.Media.ImageSourceConverter.ConvertFrom%2A> | Nelle applicazioni destinate a .NET Framework 4.6.2 e versioni precedenti, un errore nel codice di gestione delle eccezioni per il metodo <xref:System.Windows.Media.ImageSourceConverter.ConvertFrom%2A> ha causato la generazione di [NullReferenceException] (assetId:///T:System.NullReferenceException] invece dell'eccezione prevista, ad esempio [DirectoryNotFoundException](assetId:///T:System.IO.DirectoryNotFoundException) o [FileNotFoundException](assetId:///T:System.IO.FileNotFoundException).<br/><br/>A partire dalle applicazioni destinate a .NET Framework 4.7, viene generata l'eccezione corretta.  | Le applicazioni destinate a .NET Framework 4.7 e che dipendono dalla gestione di [NullReferenceException](assetId:///T:System.NullReferenceException) possono ripristinare il comportamento precedente aggiungendo il codice seguente all'impostazione di configurazione della sezione [runtime](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file `app.config`: <br/><br/>`<runtime>`<br/>&nbsp;&nbsp;&nbsp;`<AppContextSwitchOverrides value="Switch.System.Windows.Media.ImageSourceConverter.OverrideExceptionWithNullReferenceException=true"/>`<br/>`</runtime>`| Microsoft Edge | 
| Supporto per il consenso esplicito per uno stack di tocco/stilo basato su `WM_POINTER` | A partire dalle applicazioni destinate a .NET Framework 4.7, WPF aggiunge il supporto per un parametro facoltativo di tocco basato su 'WM_POINTER.  | Questa è una funzionalità di consenso esplicito disponibile nei sistemi Windows a partire da Windows 10 Creators Update. Le applicazioni WPF che acconsentono esplicitamente al supporto tocco/stilo basato su puntatore non sono interessate. Per altre informazioni, vedere [Mitigazione: Supporto di tocco e stilo basato su puntatore](../Topic/Mitigation:%20Pointer-based%20Touch%20and%20Stylus%20Support.md). | Microsoft Edge |
| Classe [PrintQueue](assetId:///T:System.Printing.PrintQueue) | A partire da .NET Framework 4.7, le API di stampa WPF che usano [PrintQueue](assetId:///T:System.Printing.PrintQueue) per impostazione predefinita chiamano l'API di Windows Print Document Package anziché l'API di stampa XPS attualmente deprecata.<br/><br/>Il vecchio stack di stampa continua a funzionare come in precedenza nelle versioni precedenti di Windows. | Né gli utenti né gli sviluppatori dovrebbero riscontrare modifiche nel comportamento o nell'uso dell'API. <br/><br/>Per usare lo stack precedente in Windows 10 Creators Update, impostare il valore `UseXpsOMPrinting` `REG_DWORD` della chiave del Registro di sistema `HKEY_CURRENT_USER\Software\Microsoft.NETFramework\Windows Presentation Foundation\Printing` su 1. | Microsoft Edge | 
## <a name="see-also"></a>Vedere anche
[Compatibilità delle applicazioni in .NET Framework 4.7](Application%20Compatibility%20in%20the%20.NET%20Framework%204.7.md)

