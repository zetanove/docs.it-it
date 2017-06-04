---
title: "IWpfHostSupport | Microsoft Docs"
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
  - "IWpfHostSupport (interfaccia)"
ms.assetid: cc5a0281-de81-4cc1-87e4-0e46b1a811e9
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# IWpfHostSupport
Le applicazioni che ospitano contenuto [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] tramite PresentationHost.exe implementano questa interfaccia per fornire un punto di integrazione tra l'host e PresentationHost.exe.  
  
## Note  
 Le applicazioni [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] quali i browser Web possono ospitare contenuto [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)], incluse le [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] e la sintassi XAML separata.  Per ospitare il contenuto [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)], le applicazioni [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] creano un'istanza del [controllo WebBrowser](http://go.microsoft.com/fwlink/?LinkId=97911) \(informazioni in lingua inglese\).  Per essere ospitato, [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] crea un'istanza di PresentationHost.exe che fornisce il contenuto [!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)] di hosting all'host per la visualizzazione nel [controllo WebBrowser](http://go.microsoft.com/fwlink/?LinkId=97911).  
  
 L'integrazione abilitata da `IWpfHostSupport` consente a PresentationHost.exe di effettuare le seguenti operazioni:  
  
-   Individuare i dispositivi di input non elaborato \(Human Interface Devices\) che interessano l'applicazione host ed eseguire la registrazione a questi dispositivi.  
  
-   Ricevere messaggi di input dai dispositivi di input non elaborato registrati e inoltra i messaggi appropriati all'applicazione host.  
  
-   Eseguire una query all'applicazione host per le interfacce utente personalizzate relative allo stato di avanzamento e agli errori.  
  
> [!NOTE]
>  Questa API è solo intesa e supportata per l'utilizzo sul computer client locale  
  
## Membri  
  
|Membro|Descrizione|  
|------------|-----------------|  
|[GetRawInputDevices](../../../../docs/framework/wpf/app-development/getrawinputdevices.md)|Consente a PresentationHost.exe di individuare i dispositivi di input non elaborato \(HID, Human Interface Devices\) che interessano l'applicazione host.|  
|[FilterInputMessage](../../../../docs/framework/wpf/app-development/filterinputmessage.md)|Chiamato da PresentationHost.exe ogni volta che viene ricevuto un messaggio, a meno che non venga restituito E\_NOTIMPL.|  
|[GetCustomUI](../../../../docs/framework/wpf/app-development/getcustomui.md)|Per impostazione predefinita, PresentationHost.exe fornisce interfacce utente proprie relative allo stato di avanzamento della distribuzione e agli errori, che vengono visualizzate quando viene distribuito il contenuto WPF.|