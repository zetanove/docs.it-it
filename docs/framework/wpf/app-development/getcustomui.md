---
title: "GetCustomUI | Microsoft Docs"
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
  - "messaggi di errore personalizzati [WPF]"
  - "GetCustomUI (metodo)"
ms.assetid: e55180fc-35bb-4f80-a136-772b5eb3e4e5
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# GetCustomUI
Chiamato da PresentationHost.exe per ottenere messaggi personalizzati di stato e di errore dall'host, se implementato.  
  
## Sintassi  
  
```  
HRESULT GetCustomUI( [out] BSTR* pwzProgressAssemblyName, [out] BSTR* pwzProgressClassName, [out] BSTR* pwzErrorAssemblyName, [out] BSTR* pwzErrorClassName );  
```  
  
#### Parametri  
 `pwzProgressAssemblyName`  
  
 \[out\] Puntatore all'assembly che contiene l'interfaccia utente di stato fornita dall'host.  
  
 `pwzProgressClassName`  
  
 \[out\] Nome della classe che rappresenta l'interfaccia utente di stato fornita dall'host, preferibilmente un file [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] con <xref:System.Windows.Controls.Page> che rappresenta l'elemento di primo livello.  Questa classe si trova nell'assembly specificato da `pwzProgressAssemblyName`.  
  
 `pwzErrorAssemblyName`  
  
 \[out\] Puntatore all'assembly che contiene l'interfaccia utente di errore fornito dall'host.  
  
 `pwzErrorClassName`  
  
 \[out\] Nome della classe che rappresenta l'interfaccia utente di errore fornita dall'host, preferibilmente un file XAML con<xref:System.Windows.Controls.Page> che rappresenta l'elemento di primo livello.  Questa classe si trova nell'assembly specificato da `pwzErrorAssemblyName`.  
  
## Valore proprietà\/Valore restituito  
 HRESULT: ignorato.  
  
## Note  
 Un'applicazione host può avere un tema specifico a cui le interfacce utente predefinite di PresentationHost.exe non sono conformi.  In tal caso l'applicazione host può implementare [GetCustomUI](../../../../docs/framework/wpf/app-development/getcustomui.md) per restituire interfacce utente di stato ed errore a PresentationHost.exe.  PresentationHost.exe chiamerà sempre [GetCustomUI](../../../../docs/framework/wpf/app-development/getcustomui.md) prima di utilizzare le interfacce utente predefinite.  
  
 Questa funzione viene chiamata una volta durante l'inizializzazione di PresentationHost.  
  
## Vedere anche  
 [IWpfHostSupport](../../../../docs/framework/wpf/app-development/iwpfhostsupport.md)