---
title: "Enabling JIT-Attach Debugging | Microsoft Docs"
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
  - "JIT-attach debugging"
  - "debugging [.NET Framework], JIT-attach debugging"
ms.assetid: f91fc5f7-de5a-4f23-b6ac-f450e63c662e
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# Enabling JIT-Attach Debugging
Debug ad associazione JIT è il termine utilizzato per descrivere l'associazione di un debugger a un processo quando si rilevano errori. In alternativa il debugger può essere attivato tramite metodi o funzioni specifici.  
  
 Il debug ad associazione JIT viene utilizzato nelle condizioni di errore riportate di seguito:  
  
-   Eccezioni non gestite \(sia in codice nativo che in codice gestito\).  
  
-   metodo <xref:System.Environment.FailFast%2A?displayProperty=fullName> o funzione [RaiseFailFastException](http://go.microsoft.com/fwlink/?LinkId=182107) \(famiglia Windows 7\).  
  
-   Errori irreversibili di runtime.  
  
 Il debug ad associazione JIT viene attivato anche mediante chiamate ai metodi e alle funzioni riportate di seguito:  
  
-   Metodo <xref:System.Diagnostics.Debugger.Launch%2A?displayProperty=fullName>.  
  
-   Metodo <xref:System.Diagnostics.Debugger.Break%2A?displayProperty=fullName>.  
  
-   [DebugBreak](http://go.microsoft.com/fwlink/?LinkId=182106) funzione \(Win32\).  
  
 Prima di [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], .NET Framework forniva chiavi del Registro di sistema separate per controllare il comportamento dei debugger nativi e gestiti.  A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], il controllo si è unificato in una singola chiave del Registro di sistema: HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\Current Version\\AeDebug.  I valori impostabili per tale chiave determinano se viene chiamato un debugger, e, in tal caso, se viene chiamato con una finestra di dialogo che richiede interazione da parte dell'utente.  Per informazioni sull'impostazione di questa chiave del Registro di sistema, vedere [Debug di configurazione automatica](http://go.microsoft.com/fwlink/?LinkId=181767) in MSDN Library.  
  
## Vedere anche  
 [Debugging, Tracing, and Profiling](../../../docs/framework/debug-trace-profile/index.md)   
 [Semplificazione del debug di un'immagine](../../../docs/framework/debug-trace-profile/making-an-image-easier-to-debug.md)   
 [Enabling Profiling](http://msdn.microsoft.com/it-it/3b669676-f0e0-4ebf-8674-68986dd2020d)