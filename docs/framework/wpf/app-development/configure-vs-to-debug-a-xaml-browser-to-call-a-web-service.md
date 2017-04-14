---
title: "Procedura: configurare Visual Studio per eseguire il debug di un&#39;applicazione browser XAML in grado di chiamare un servizio Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Visual Studio (configurazione per il debug di applicazioni browser XAML) [WPF]"
  - "Visual Studio (configurazione per il debug di applicazioni XBAP) [WPF]"
  - "debug delle eccezioni di sicurezza per le applicazioni XBAP [WPF]"
  - "debug di applicazioni XBAP chiamanti un servizio Web [WPF]"
  - "eccezioni di sicurezza per le applicazioni XBAP [WPF], debug"
ms.assetid: fd1db082-a7bb-4c4b-9331-6ad74a0682d0
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: configurare Visual Studio per eseguire il debug di un&#39;applicazione browser XAML in grado di chiamare un servizio Web
Le [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] vengono eseguite all'interno di un sandbox di sicurezza con attendibilità parziale ristretto al set di autorizzazioni dell'area Internet.  Questo set di autorizzazioni limita le chiamate del servizio Web ai servizi Web che si trovano nel sito di origine dell'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)].  Tuttavia, quando un'[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] è sottoposta a debug da [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)], non viene considerata come proveniente dallo stesso sito di origine del servizio Web a cui fa riferimento.  Pertanto, quando l'[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] tenta di chiamare il servizio Web vengono generate delle eccezioni di sicurezza.  In ogni caso, è possibile configurare un progetto dell'[!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)] di [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] in modo da simulare la provenienza dallo stesso sito di origine del servizio Web chiamato durante il debug.  Tale operazione consente all'[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] di chiamare in modo sicuro il servizio Web senza generare eccezioni di sicurezza.  
  
## Configurazione di Visual Studio  
 Per configurare [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] affinché venga eseguito il debug di un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] che chiama un servizio Web:  
  
1.  Con un progetto selezionato in **Esplora soluzioni**, scegliere **Proprietà** dal menu **Progetto**.  
  
2.  Fare clic sulla scheda **Debug** in **Progettazione progetti**.  
  
3.  Nella sezione **Azione di avvio** selezionare **Avvia programma esterno** e immettere quanto segue:  
  
     `C:\WINDOWS\System32\PresentationHost.exe`  
  
4.  Nella sezione **Opzioni di avvio** immettere quanto segue nella casella di testo **Argomenti della riga di comando**:  
  
     `-debug`  *nome file*  
  
     Il valore *nome file* per il parametro **\-debug** è il nome del file con estensione xbap, ad esempio:  
  
     `-debug c:\example.xbap`  
  
> [!NOTE]
>  Si tratta della configurazione predefinita per soluzioni create con il modello di progetto [!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)] di [!INCLUDE[TLA2#tla_visualstu2005](../../../../includes/tla2sharptla-visualstu2005-md.md)].  
  
1.  Con un progetto selezionato in **Esplora soluzioni**, scegliere **Proprietà** dal menu **Progetto**.  
  
2.  Fare clic sulla scheda **Debug** in **Progettazione progetti**.  
  
3.  Nella sezione **Opzioni di avvio**, aggiungere il parametro della riga di comando nella casella di testo **Argomenti della riga di comando**:  
  
     `-debugSecurityZoneURL`  *URL*  
  
     Il valore *URL* per il parametro **\-debugSecurityZoneURL** rappresenta l'[!INCLUDE[TLA#tla_url](../../../../includes/tlasharptla-url-md.md)] del percorso che si desidera simulare come sito di origine dell'applicazione.  
  
 Ad esempio, considerare un'applicazione [!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)] che utilizza un servizio Web con il seguente [!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)]:  
  
 `http://services.msdn.microsoft.com/ContentServices/ContentService.asmx`  
  
 L'[!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)] del sito di origine per questo servizio Web è:  
  
 `http://services.msdn.microsoft.com`  
  
 Di conseguenza, il parametro della riga di comando **\-debugSecurityZoneURL** e il valore completi saranno:  
  
 `-debugSecurityZoneURL http://services.msdn.microsoft.com`  
  
## Vedere anche  
 [Host WPF \(PresentationHost.exe\)](../../../../docs/framework/wpf/app-development/wpf-host-presentationhost-exe.md)