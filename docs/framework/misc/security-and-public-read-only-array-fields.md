---
title: "Security and Public Read-only Array Fields | Microsoft Docs"
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
  - "security [.NET Framework], public read-only array fields"
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Security and Public Read-only Array Fields
Non utilizzare mai i campi di matrice pubblici di sola lettura provenienti da librerie gestite per definire il comportamento dei tipi di limite ossia la sicurezza delle applicazioni, poiché tali campi possono essere modificati.  
  
## Osservazioni  
 In alcune classi di .NET Framework sono inclusi campi pubblici di sola lettura che contengono parametri di limite specifici per la piattaforma.  Il campo <xref:System.IO.Path.InvalidPathChars>, ad esempio, è una matrice che contiene i caratteri non consentiti in una stringa relativa al percorso di un file.  In .NET Framework sono presenti numerosi campi analoghi.  
  
 I valori dei campi pubblici di sola lettura come <xref:System.IO.Path.InvalidPathChars> possono essere modificati dal codice scritto dallo sviluppatore o da codice che ne condivide il dominio applicazione.  Di conseguenza, si consiglia di non utilizzare campi di questo tipo per definire il comportamento dei tipi di limite delle applicazioni,  altrimenti si corre il rischio che le definizioni dei limiti vengano modificate da malware provocando un comportamento imprevisto del codice.  
  
 In .NET Framework 2.0 e versioni successive è opportuno utilizzare metodi che restituiscono una nuova matrice anziché campi di matrice pubblici,  ad esempio il metodo <xref:System.IO.Path.GetInvalidPathChars%2A> anziché il campo <xref:System.IO.Path.InvalidPathChars>.  
  
 Si noti che in .NET Framework per definire internamente i tipi dei limiti non vengono utilizzati campi pubblici,  ma campi privati separati.  In questo modo, le eventuali modifiche apportate ai valori di questi campi pubblici non influiscono sul comportamento dei tipi di .NET Framework.  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)