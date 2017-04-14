---
title: "FilterInputMessage | Microsoft Docs"
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
  - "FilterInputMessage (metodo)"
  - "input non elaborato [WPF]"
ms.assetid: 4d74c6cf-7d1d-49ff-96c1-231340ce54f5
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# FilterInputMessage
Chiamato da PresentationHost.exe ogni volta che viene ricevuto un messaggio, a meno che non venga restituito E\_NOTIMPL.  
  
## Sintassi  
  
```  
HRESULT FilterInputMessage( [in] MSG* pMsg ) ;  
```  
  
#### Parametri  
 `pMsg`  
  
 \[in\] Messaggio WM\_INPUT inviato alla finestra che sta ricevendo l'input non elaborato.  
  
## Valore proprietà\/Valore restituito  
 HRESULT:  
  
 S\_OK: il filtro non ha elaborato il messaggio e l'elaborazione può proseguire.  
  
 S\_FALSE: il filtro ha elaborato questo messaggio e non viene eseguita alcuna ulteriore elaborazione.  
  
 E\_NOTIMPL: se viene restituito questo valore, non viene nuovamente chiamato [FilterInputMessage](../../../../docs/framework/wpf/app-development/filterinputmessage.md).  È possibile che venga restituito da un'applicazione host interessata solo a fornire interfacce utente personalizzate di stato ed errore a PresentationHost.exe e non a ricevere messaggi di input non elaborato da PresentationHost.exe.  
  
## Note  
 PresentationHost.exe è la destinazione di vari dispositivi di input non elaborato, tra cui tastiere, mouse e telecomandi.  In alcuni casi, il comportamento nell'applicazione host dipende dall'input che, in caso contrario, verrebbe usato da PresentationHost.exe.  Ad esempio, la visualizzazione di specifici elementi dell'interfaccia utente da parte di un'applicazione host può dipendere dalla ricezione di determinati messaggi di input.  
  
 Per consentire all'applicazione host di ricevere i messaggi di input necessari per questi comportamenti, mediante PresentationHost.exe vengono inviati messaggi di input non elaborato adatti all'applicazione ospitata chiamando [FilterInputMessage](../../../../docs/framework/wpf/app-development/filterinputmessage.md).  
  
 L'applicazione ospitata riceve i messaggi di input non elaborato tramite la registrazione con l'insieme di dispositivi di input non elaborato \(Human Interface Device, HID\) restituito da [GetRawInputDevices](../../../../docs/framework/wpf/app-development/getrawinputdevices.md).  
  
## Vedere anche  
 [Notifica WM\_INPUT](http://msdn.microsoft.com/library/default.asp?url=/library/winui/winui/windowsuserinterface/userinput/rawinput/rawinputreference/rawinputmessages/wm_input.asp)