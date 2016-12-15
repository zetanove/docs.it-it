---
title: "Objects (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "objects [Visual Basic]"
ms.assetid: 651c73e4-dca8-402b-9c6b-e3902b3a3f4b
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Objects (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In questo argomento vengono forniti i collegamenti ad altri argomenti in cui sono descritti gli oggetti di runtime di Visual Basic e sono disponibili tabelle delle routine, delle proprietà e degli eventi dei relativi membri.  
  
## Oggetti di runtime di Visual Basic  
  
|||  
|-|-|  
|<xref:Microsoft.VisualBasic.Collection>|Consente di considerare un gruppo correlato di elementi come se si trattasse di un unico oggetto.|  
|<xref:Microsoft.VisualBasic.Information.Err%2A>|Contiene informazioni relative a errori di runtime.|  
|L'oggetto `My.Application` è costituito dalle classi seguenti:<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase> fornisce i membri disponibili in tutti i progetti.<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> fornisce i membri disponibili nelle applicazioni Windows Form.<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> fornisce i membri disponibili nelle applicazioni console.|Fornisce solo i dati associati all'applicazione o alla DLL corrente.  L'oggetto `My.Application` non altera le informazioni a livello di sistema.<br /><br /> Alcuni membri sono disponibili solo per i Windows Form o le applicazioni console.|  
|`My.Application.Info` \(<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Info%2A>\)|Fornisce le proprietà per ottenere informazioni su un'applicazione, ad esempio il numero della versione, la descrizione, gli assembly caricati e così via.|  
|`My.Application.Log` \(<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log%2A>\)|Fornisce una proprietà e i metodi per scrivere le informazioni relative all'evento e all'eccezione sui listener di log dell'applicazione.|  
|`My.Computer` \(<xref:Microsoft.VisualBasic.Devices.Computer>\)|Fornisce le proprietà per la gestione dei componenti del computer come audio, orologio, tastiera, file system e così via.|  
|`My.Computer.Audio` \(<xref:Microsoft.VisualBasic.Devices.Audio>\)|Fornisce i metodi per la riproduzione di suoni.|  
|`My.Computer.Clipboard` \(<xref:Microsoft.VisualBasic.Devices.Computer.Clipboard%2A>\)|Fornisce metodi per la modifica degli Appunti.|  
|`My.Computer.Clock` \(<xref:Microsoft.VisualBasic.Devices.Clock>\)|Fornisce le proprietà per accedere all'ora locale corrente e al tempo universale coordinato \(UTC\), equivalente all'ora di Greenwich, dall'orologio di sistema.|  
|`My.Computer.FileSystem` \(<xref:Microsoft.VisualBasic.FileIO.FileSystem>\)|Fornisce le proprietà e i metodi per l'utilizzo di unità, file e directory.|  
|`My.Computer.FileSystem.SpecialDirectories` \(<xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>\)|Fornisce le proprietà necessarie per accedere alle directory cui si fa riferimento più comunemente.|  
|`My.Computer.Info` \(<xref:Microsoft.VisualBasic.Devices.ComputerInfo>\)|Fornisce le proprietà che consentono di ottenere informazioni sulla memoria, sugli assembly caricati, sul nome e sul sistema operativo del computer.|  
|`My.Computer.Keyboard` \(<xref:Microsoft.VisualBasic.Devices.Keyboard>\)|Fornisce le proprietà per accedere allo stato corrente della tastiera, ad esempio ai tasti attualmente premuti, e un metodo per inviare le sequenze di tasti alla finestra attiva.|  
|`My.Computer.Mouse` \(<xref:Microsoft.VisualBasic.Devices.Mouse>\)|Fornisce le proprietà per ottenere informazioni sul formato e la configurazione del mouse installato nel computer locale.|  
|`My.Computer.Network` \(<xref:Microsoft.VisualBasic.Devices.Network>\)|Fornisce una proprietà, un evento e dei metodi per l'interazione con la rete a cui è connesso il computer.|  
|`My.Computer.Ports` \(<xref:Microsoft.VisualBasic.Devices.Ports>\)|Fornisce una proprietà e un metodo per accedere alle porte seriali del computer.|  
|`My.Computer.Registry` \(<xref:Microsoft.VisualBasic.MyServices.RegistryProxy>\)|Fornisce proprietà e metodi per la modifica del Registro di sistema.|  
|[My.Forms Object](../../../visual-basic/language-reference/objects/my-forms-object.md)|Fornisce le proprietà che consentono di accedere alle istanze di ciascun Windows Form dichiarato nel progetto corrente.|  
|`My.Log` \(<xref:Microsoft.VisualBasic.Logging.AspLog>\)|Fornisce una proprietà e metodi per scrivere informazioni su eventi ed eccezioni nei listener del log dell'applicazione per le applicazioni Web.|  
|[My.Request Object](../../../visual-basic/language-reference/objects/my-request-object.md)|Ottiene l'oggetto <xref:System.Web.HttpRequest> per la pagina richiesta.  L'oggetto `My.Request` contiene le informazioni relative alla richiesta HTTP corrente.<br /><br /> L'oggetto `My.Request` è disponibile solo per le applicazioni [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].|  
|[My.Resources Object](../../../visual-basic/language-reference/objects/my-resources-object.md)|Fornisce proprietà e classi per accedere alle risorse di un'applicazione.|  
|[My.Response Object](../../../visual-basic/language-reference/objects/my-response-object.md)|Ottiene l'oggetto <xref:System.Web.HttpResponse> associato a <xref:System.Web.UI.Page>.  Questo oggetto consente di inviare i dati di una risposta HTTP a un client e contiene informazioni su quella risposta.<br /><br /> L'oggetto `My.Response` è disponibile solo per le applicazioni [!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)].|  
|[My.Settings Object](../../../visual-basic/language-reference/objects/my-settings-object.md)|Fornisce proprietà e metodi per accedere alle impostazioni di un'applicazione.|  
|`My.User` \(<xref:Microsoft.VisualBasic.ApplicationServices.User>\)|Fornisce l'accesso alle informazioni relative all'utente corrente.|  
|[My.WebServices Object](../../../visual-basic/language-reference/objects/my-webservices-object.md)|Fornisce proprietà per la creazione e l'accesso a una singola istanza di ciascun servizio Web a cui fa riferimento il progetto corrente.|  
|<xref:Microsoft.VisualBasic.FileIO.TextFieldParser>|Fornisce i metodi e le proprietà per l'analisi dei file di testo strutturati.|  
  
## Vedere anche  
 [Visual Basic Language Reference](../../../visual-basic/language-reference/index.md)   
 [Visual Basic](../../../visual-basic/index.md)