---
title: "Sviluppo per piattaforme multiple con .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: b153baaa-130c-4169-860b-e580591de91e
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Sviluppo per piattaforme multiple con .NET Framework
Con .NET Framework e Visual Studio è possibile sviluppare app per piattaforme Microsoft e non Microsoft.  
  
## Opzioni per lo sviluppo multipiattaforma  
 Per sviluppare applicazioni per più piattaforme è possibile condividere il codice sorgente ed effettuare chiamate tra il codice .NET Framework e le API di Windows Runtime.  
  
|Per...|Usare...|  
|------------|--------------|  
|Condividere codice sorgente tra app Windows Phone 8.1 e app Windows 8.1|**Progetti condivisi** \(modello per applicazioni universali in Visual Studio 2013 Update 2\).<br /><br /> -   Attualmente Visual Basic non è supportato.<br />-   È possibile separare il codice specifico della piattaforma usando istruzioni \#`if`.<br /><br /> Per informazioni dettagliate, vedere:<br /><br /> -   [Creare app Windows universali per Windows e Windows Phone usando Visual Studio](http://msdn.microsoft.com/library/windows/apps/dn609832.aspx) \(articolo MSDN\)<br />-   [Uso di Visual Studio per la compilazione di app XAML universali](http://blogs.msdn.com/b/visualstudio/archive/2014/04/14/using-visual-studio-to-build-universal-xaml-apps.aspx) \(blog post\)<br />-   [Uso di Visual Studio per la compilazione di app XAML convergenti](http://channel9.msdn.com/Events/Build/2014/3-591) \(video\)|  
|Condividere i binari tra app destinate a piattaforme diverse|**Progetti Libreria di classi portabile** per il codice indipendente dalla piattaforma.<br /><br /> -   In genere questo approccio viene usato per il codice che implementa logica di business.<br />-   È possibile usare Visual Basic o C\#.<br />-   Il supporto delle API varia in base alla piattaforma.<br />-   I progetti Libreria di classi portabile destinati a Windows 8.1 e Windows Phone 8.1 supportano le API di Windows Runtime e XAML.  Queste funzionalità non sono disponibili nelle versioni precedenti di Libreria di classi portabile.<br />-   Se necessario, è possibile astrarre il codice specifico della piattaforma usando interfacce o classi astratte.<br /><br /> Per informazioni dettagliate, vedere:<br /><br /> -   [Libreria di classi portabile](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) \(articolo MSDN\)<br />-   [Come usare le librerie di classi portabili](http://blogs.msdn.com/b/dsplaisted/archive/2012/08/27/how-to-make-portable-class-libraries-work-for-you.aspx) \(post di blog\)<br />-   [Utilizzo della libreria di classi portabile con MVVM](../../../docs/standard/cross-platform/using-portable-class-library-with-model-view-view-model.md) \(articolo MSDN\)<br />-   [Risorse app per librerie destinate a più piattaforme](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md) \(articolo MSDN\)<br />-   [.NET Portability Analyzer](http://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b) \(estensione di Visual Studio\)|  
|Condividere codice sorgente tra app per piattaforme diverse da Windows 8.1 e Windows Phone 8.1|Funzionalità **Aggiungi come collegamento**.<br /><br /> -   Questo approccio è idoneo per la logica comune ad entrambe le app, ma che per qualche motivo non è portabile.  È possibile usare questa funzionalità per il codice C\# o Visual Basic.<br />     Ad esempio, Windows Phone 8 e Windows 8 condividono le API di Windows Runtime, ma le librerie di classi portabili non supportano Windows Runtime per queste piattaforme.  È possibile usare `Add as link` per condividere il codice Windows Runtime tra un'app Windows Phone 8 e un'app di Windows Store destinata a Windows 8.<br /><br /> Per informazioni dettagliate, vedere:<br /><br /> -   [Condividere codice con Aggiungi come collegamento](http://msdn.microsoft.com/library/windowsphone/develop/jj714082\(v=vs.105\).aspx) \(articolo MSDN\)<br />-   [Procedura: aggiungere elementi esistenti a un progetto](http://msdn.microsoft.com/library/vstudio/9f4t9t92\(v=vs.100\).aspx) \(articolo MSDN\)|  
|Scrivere app di Windows Store usando .NET Framework o chiamare API di Windows Runtime API dal codice .NET Framework|**API di Windows Runtime** dal codice .NET Framework C\# o Visual Basic e usare .NET Framework per creare app di Windows Store.  È opportuno tenere presenti le differenze relative alle API tra le due piattaforme,  tuttavia sono disponibili classi che agevolano la gestione di queste differenze.<br /><br /> Per informazioni dettagliate, vedere:<br /><br /> -   [Supporto .NET Framework per applicazioni Windows Store e Windows Runtime](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md) \(articolo MSDN\)<br />-   [Passaggio di un URI a Windows Runtime](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md) \(articolo MSDN\)<br />-   <xref:System.IO.WindowsRuntimeStreamExtensions> \(pagina di riferimento API su MSDN\)<br />-   <xref:System.WindowsRuntimeSystemExtensions> \(pagina di riferimento API su MSDN\)|  
|Sviluppare app .NET Framework per piattaforme non Microsoft|**Assembly di riferimento per Libreria di classi portabile** in .NET Framework e un'estensione di Visual Studio o uno strumento di terze parti come Xamarin.<br /><br /> Per informazioni dettagliate, vedere:<br /><br /> -   [Disponibilità di Libreria di classi portabile su tutte le piattaforme.](http://blogs.msdn.com/b/dotnet/archive/2013/10/14/portable-class-library-pcl-now-available-on-all-platforms.aspx) \(post di blog\)<br />-   [Xamarin](http://xamarin.com/visual-studio) \(sito Web Xamarin\)|  
|Usare JavaScript e HTML per lo sviluppo multipiattaforma|**Modelli per applicazioni universali** in Visual Studio 2013 Update 2 per scrivere codice usando le API di Windows Runtime per Windows 8.1 e Windows Phone 8.1.  Attualmente non è possibile usare JavaScript e HTML con le API .NET Framework per sviluppare app multipiattaforma.<br /><br /> Per informazioni dettagliate, vedere:<br /><br /> -   [Modelli di progetto JavaScript](http://msdn.microsoft.com/library/windows/apps/hh758331.aspx)<br />-   [Come trasferire un'app di Windows Runtime scritta in JavaScript a Windows Phone](http://msdn.microsoft.com/library/windows/apps/dn636144.aspx)|