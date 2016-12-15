---
title: "Throw Statement (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Throw"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "structured exception handling, throw statements"
  - "try-catch exception handling, throw statements"
  - "throw statement, about throw statements"
  - "throwing exceptions, throw statement"
  - "exception handling, throw statement"
  - "On Error statement, throwing exceptions"
  - "throwing exceptions"
  - "exception handling, unstructured"
  - "throw statement"
ms.assetid: a6e07406-5c8a-4498-87a2-8339f3651d62
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Throw Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Viene generata un'eccezione in una routine.  
  
## Sintassi  
  
```  
Throw [ expression ]  
```  
  
## Parte  
 `expression`  
 Consente di fornire informazioni relative all'eccezione da generare.  Facoltativo quando risiede in un'istruzione `Catch`, in caso contrario è necessario.  
  
## Note  
 Tramite l'istruzione `Throw` viene generata un'eccezione che può essere gestita con un codice di gestione delle eccezioni strutturato \(`Try`...`Catch`...`Finally`\) oppure un codice di gestione delle eccezioni non strutturato \(`On Error GoTo`\).  L'istruzione `Throw` consente di intercettare gli errori presenti nel codice, poiché Visual Basic scorre lo stack di chiamate fino a trovare il codice di gestione delle eccezioni appropriato.  
  
 È possibile utilizzare un'istruzione `Throw` priva di espressioni soltanto in un'istruzione `Catch`, nel qual caso verrà nuovamente generata l'eccezione attualmente gestita dall'istruzione `Catch` stessa.  
  
 L'istruzione `Throw` reimposta lo stack di chiamate per l'eccezione `expression`.  Se `expression` non viene fornito, lo stack di chiamate resta invariato.  È possibile accedere allo stack di chiamate per l'eccezione mediante la proprietà <xref:System.Exception.StackTrace%2A>.  
  
## Esempio  
 Nel codice seguente l'istruzione `Throw` viene utilizzata per generare un'eccezione:  
  
 [!code-vb[VbVbalrStatements#84](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/throw-statement_1.vb)]  
  
## Requisiti  
 **Spazio dei nomi:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **Modulo:** `Interaction`  
  
 **Assembly:** Visual Basic Runtime Library \(in Microsoft.VisualBasic.dll\)  
  
## Vedere anche  
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [On Error Statement](../../../visual-basic/language-reference/statements/on-error-statement.md)