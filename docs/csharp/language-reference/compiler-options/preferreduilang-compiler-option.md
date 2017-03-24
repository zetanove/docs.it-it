---
title: "/preferreduilang (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/preferreduilang"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "preferreduilang compiler option [C#]"
  - "/preferreduilang compiler option [C#]"
  - "-preferreduilang compiler option [C#]"
ms.assetid: 68b2462f-6778-48d7-8052-62805fe8e02c
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# /preferreduilang (C# Compiler Options)
Utilizzando l'opzione del compilatore `/preferreduilang`, è possibile specificare il linguaggio in cui il compilatore C\# visualizza l'output, come ad esempio i messaggi di errore.  
  
## Sintassi  
  
```  
/preferreduilang: language  
```  
  
## Argomenti  
 `language`  
 Il [nome della lingua](http://go.microsoft.com/fwlink/p/?LinkId=236992) del linguaggio da utilizzare per l'output del compilatore.  
  
## Note  
 È possibile utilizzare l'opzione del compilatore `/preferreduilang` per specificare il linguaggio che si desidera che il compilatore C\# usi per i messaggi di errore e altri output della riga di comando.  Se il pacchetto lingua della lingua non è installato, viene utilizzata l'impostazione della lingua del sistema operativo e nessun errore viene restituito.  
  
```c#  
csc.exe /preferreduilang:ja-JP  
```  
  
## Requisiti  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)