---
title: Introduzione a .NET Framework | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework-4.6
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework, getting started
- getting started [.NET Framework]
ms.assetid: c693fd34-88fe-4d90-b332-19eeadf3b7e7
caps.latest.revision: 35
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: adb9c30b6dc52ea17410423fd76c938e258549eb
ms.openlocfilehash: 6c069db2e6138f73935a4bdd458fbe94ef57d968
ms.lasthandoff: 05/02/2017

---
# <a name="getting-started-with-the-net-framework"></a>Introduzione a .NET Framework
.NET Framework è un ambiente di esecuzione runtime in cui vengono gestite le applicazioni destinate a .NET Framework. È costituito da Common Language Runtime, che fornisce la gestione della memoria e altri servizi di sistema, e da un'ampia libreria di classi, che consente ai programmatori di sfruttare codice affidabile per tutte le aree principali dello sviluppo di applicazioni.  
  
<a name="Introducing"></a>   
## <a name="what-is-the-net-framework"></a>Cos'è .NET Framework?  
 .NET Framework è un ambiente di esecuzione gestita che fornisce un'ampia gamma di servizi alle applicazioni in esecuzione. È costituito da due componenti principali: Common Language Runtime (CLR), vale a dire il motore di esecuzione mediante il quale vengono gestite le applicazioni in esecuzione, e la libreria di classi .NET Framework, che fornisce una raccolta di codice testato e riutilizzabile che gli sviluppatori possono chiamare dalle rispettive applicazioni. Tra i servizi forniti da .NET Framework per le applicazioni in esecuzione sono inclusi:  
  
-   Gestione della memoria. In molti linguaggi di programmazione, i programmatori sono responsabili dell'allocazione e del rilascio di memoria, nonché della gestione della durata degli oggetti. Nelle applicazioni .NET Framework, CLR fornisce questi servizi per conto dell'applicazione.  
  
-   Common Type System. Nei linguaggi di programmazione tradizionali, i tipi di base vengono definiti dal compilatore, mediante il quale l'interoperabilità tra i linguaggi viene resa più complicata. In .NET Framework i tipi di base vengono definiti dal sistema di tipi di .NET Framework e sono comuni a tutti i linguaggi destinati a .NET Framework.  
  
-   Libreria di classi estesa. Anziché dover scrivere grandi quantità di codice per gestire operazioni comuni di programmazione di basso livello, i programmatori possono usare una libreria di tipi facilmente accessibile e i relativi membri dalla libreria di classi .NET Framework.  
  
-   Framework e tecnologie di sviluppo. In .NET Framework sono incluse librerie per aree specifiche dello sviluppo di applicazioni, ad esempio ASP.NET per applicazioni Web, ADO.NET per l'accesso ai dati e Windows Communication Foundation per applicazioni orientate ai servizi.  
  
-   Interoperabilità del linguaggio. Tramite i compilatori di linguaggio destinati a .NET Framework viene generato un codice intermedio denominato Common Intermediate Language (CIL) che, a sua volta, viene compilato in fase di esecuzione tramite Common Language Runtime. Con questa funzionalità, le routine scritte in un linguaggio sono accessibili ad altri linguaggi e i programmatori possono concentrarsi sulla creazione di applicazioni in uno o più linguaggi preferiti.  
  
-   Compatibilità tra versioni. In rare eccezioni, le applicazioni sviluppate usando una particolare versione di .NET Framework possono essere eseguite senza modifiche in una versione successiva.  
  
-   Esecuzione affiancata. .NET Framework consente di risolvere conflitti tra versioni permettendo la coesistenza di più versioni di Common Language Runtime nello stesso computer. Ciò significa che possono anche coesistere più versioni di applicazioni e che un'applicazione può essere eseguita nella versione di .NET Framework con cui è stata creata.  
  
-   Multitargeting. Scegliendo come destinazione la libreria di classi portabile di .NET Framework, gli sviluppatori possono creare assembly che funzionano su più piattaforme .NET Framework, come ad esempio Windows 7, Windows 8, Windows 8.1, Windows 10, Windows Phone e Xbox 360. Per altre informazioni, vedere [Libreria di classi portabile](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).  
  
<a name="ForUsers"></a>   
## <a name="the-net-framework-for-users"></a>.NET Framework per utenti  
 Se non si sviluppano ma si usano applicazioni .NET Framework, non è necessario avere una specifica conoscenza di .NET Framework o del relativo funzionamento. .NET Framework è sostanzialmente trasparente agli utenti.  
  
 Se si usa il sistema operativo Windows, .NET Framework potrebbe essere già installato nel computer. Inoltre, se si installa un'applicazione per cui è richiesto .NET Framework, è possibile che tramite il programma di installazione dell'applicazione venga installata una versione specifica di .NET Framework nel computer locale. In alcuni casi, potrebbe essere visualizzata una finestra di dialogo in cui viene chiesto di installare .NET Framework. Se quando viene visualizzata questa finestra di dialogo si è tentato solo di eseguire un'applicazione e se il computer dispone di accesso a Internet, è possibile visitare una pagina Web che consente di installare la versione mancante di .NET Framework.  
  
 In generale, le versioni di .NET Framework installate nel computer non devono essere disinstallate per due motivi:  
  
-   Se un'applicazione in uso dipende da una specifica versione di .NET Framework che viene rimossa, l'applicazione potrebbe essere interrotta.  
  
-   Alcune versioni di .NET Framework sono aggiornamenti sul posto di versioni precedenti. Ad esempio, [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] è un aggiornamento sul posto alla versione 2.0 e .NET Framework 4.6 è un aggiornamento sul posto alle versioni 4, 4.5, 4.5.1 e 4.5.2. Per altre informazioni, vedere [Versioni e dipendenze di .NET Framework](../../../docs/framework/migration-guide/versions-and-dependencies.md).  
  
 Se si sceglie di rimuovere .NET Framework, usare sempre **Programmi e funzionalità** dal Pannello di controllo per disinstallarlo. Non rimuovere mai manualmente una versione di .NET Framework.  
  
 È possibile caricare più versioni di .NET Framework contemporaneamente in un computer. Ciò significa che non è necessario disinstallare le versioni precedenti per installare una versione successiva.  
  
<a name="ForDevelopers"></a>   
## <a name="the-net-framework-for-developers"></a>.NET Framework per sviluppatori  
 Uno sviluppatore può scegliere qualsiasi linguaggio di programmazione che supporta .NET Framework per creare l'applicazione. Poiché .NET Framework fornisce interoperabilità e indipendenza di linguaggio, è possibile interagire con altre applicazioni e componenti .NET Framework indipendentemente dal linguaggio con cui sono stati sviluppati.  
  
 Per sviluppare applicazioni o componenti .NET Framework, effettuare le operazioni seguenti:  
  
1.  Se non è già preinstallata nel sistema operativo, installare la versione di .NET Framework che userà l'applicazione. La versione di produzione più recente è .NET Framework 4.7, preinstallata in Windows 10 Creative Update e disponibile per il download nelle versioni precedenti del sistema operativo Windows. Per i requisiti di sistema di .NET Framework, vedere [Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md). Per informazioni sull'installazione di .NET Framework, vedere [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md). Sono disponibili pacchetti aggiuntivi di .NET Framework rilasciati fuori programma. Per informazioni su questi pacchetti, vedere [.NET Framework e rilascio fuori programma](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md).  
  
2.  Selezionare uno o più linguaggi .NET Framework che verranno usati per sviluppare le applicazioni. Sono disponibili numerosi linguaggi, tra cui Visual Basic, C#, Visual F# e C++ di Microsoft. Un linguaggio di programmazione che consente di sviluppare applicazioni per .NET Framework è conforme alla [specifica CLI (Common Language Infrastructure)](http://go.microsoft.com/fwlink/?LinkId=199862).  
  
3.  Selezionare e installare l'ambiente di sviluppo che verrà usato per creare le applicazioni e che supporti uno o più linguaggi di programmazione selezionati. L'ambiente di sviluppo integrato Microsoft per le applicazioni .NET Framework è [Visual Studio](http://go.microsoft.com/fwlink/?LinkId=325532). È disponibile in numerose edizioni commerciali e gratuite.  
  
 Per altre informazioni sullo sviluppo di app destinate a .NET Framework, vedere [Guida di sviluppo](../../../docs/framework/development-guide.md).  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Panoramica](../../../docs/framework/get-started/overview.md)|Vengono fornite informazioni dettagliate per gli sviluppatori che realizzano applicazioni destinate a .NET Framework.|  
|[.NET Framework e rilascio fuori programma](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)|Vengono descritti i rilasci fuori programma di .NET Framework e viene illustrato come usarli nell'applicazione.|  
|[Requisiti di sistema](../../../docs/framework/get-started/system-requirements.md)|Vengono elencati i requisiti hardware e software per l'esecuzione di .NET Framework.|  
|[Componenti di base e open-source di .NET](../../../docs/framework/get-started/net-core-and-open-source.md)|Viene descritto .NET Core in relazione a .NET Framework e viene spiegato come accedere ai progetti .NET Core open source.|  
|[Documentazione di .NET Core](https://docs.microsoft.com/dotnet/)|Documentazione concettuale e di riferimento delle API per .NET Core.|  
|[Guida all'installazione](../../../docs/framework/install/guide-for-developers.md)|Vengono fornite informazioni sull'installazione di .NET Framework.|  
  
## <a name="see-also"></a>Vedere anche  
 [.NET Framework 4.6 e 4.5](../../../docs/framework/index.md)   
 [Novità](../../../docs/framework/whats-new/index.md)   
 [Libreria di classi .NET Framework](http://go.microsoft.com/fwlink/?LinkId=227195)   
 [Guida di sviluppo](../../../docs/framework/development-guide.md)
