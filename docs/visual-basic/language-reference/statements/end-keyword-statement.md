---
title: "End &lt;keyword&gt; Statement (Visual Basic) | Microsoft Docs"
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
  - "vb.EndDefinition"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "End keyword"
ms.assetid: 42d6e088-ab0f-4cda-88e8-fdce3e5fcf4f
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# End &lt;keyword&gt; Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando è seguito da una parola chiave aggiuntiva, termina la definizione del blocco di istruzioni introdotto dalla parola chiave.  
  
## Sintassi  
  
```  
End AddHandler  
End Class   
End Enum   
End Event   
End Function   
End Get   
End If   
End Interface   
End Module   
End Namespace   
End Operator   
End Property   
End RaiseEvent  
End RemoveHandler  
End Select   
End Set   
End Structure   
End Sub   
End SyncLock   
End Try   
End While   
End With  
```  
  
## Parti  
 `End`  
 Obbligatorio.  Termina la definizione dell'elemento di programmazione.  
  
 `AddHandler`  
 Necessaria per terminare una funzione di accesso `AddHandler` iniziata mediante un'istruzione `AddHandler` corrispondente in un'[Event Statement](../../../visual-basic/language-reference/statements/event-statement.md) personalizzata.  
  
 `Class`  
 Necessaria per terminare una definizione di classe iniziata mediante un'[Class Statement](../../../visual-basic/language-reference/statements/class-statement.md) corrispondente.  
  
 `Enum`  
 Necessaria per terminare una definizione di enumerazione iniziata mediante un'[Enum Statement](../../../visual-basic/language-reference/statements/enum-statement.md) corrispondente.  
  
 `Event`  
 Necessaria per terminare una definizione di evento `Custom` iniziata mediante un'[Event Statement](../../../visual-basic/language-reference/statements/event-statement.md) corrispondente.  
  
 `Function`  
 Necessaria per terminare una definizione di routine `Function` iniziata mediante un'[Function Statement](../../../visual-basic/language-reference/statements/function-statement.md) corrispondente.  Se durante l'esecuzione viene rilevata un'istruzione `End` `Function`, il controllo torna al codice chiamante.  
  
 `Get`  
 Necessaria per terminare una definizione di routine `Property` iniziata mediante un'[Get Statement](../../../visual-basic/language-reference/statements/get-statement.md) corrispondente.  Se durante l'esecuzione viene rilevata un'istruzione `End` `Get`, il controllo torna all'istruzione che richiede il valore della proprietà.  
  
 `If`  
 Necessaria per terminare una definizione di blocco `If`...`Then`...`Else` iniziata mediante un'istruzione `If` corrispondente.  Vedere [If...Then...Else Statement](../../../visual-basic/language-reference/statements/if-then-else-statement.md).  
  
 `Interface`  
 Necessaria per terminare una definizione di interfaccia iniziata mediante un'[Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md) corrispondente.  
  
 `Module`  
 Necessaria per terminare una definizione di modulo iniziata mediante un'[Module Statement](../../../visual-basic/language-reference/statements/module-statement.md) corrispondente.  
  
 `Namespace`  
 Necessaria per terminare una definizione di spazio dei nomi iniziata mediante un'[Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md) corrispondente.  
  
 `Operator`  
 Necessaria per terminare una definizione di operatore iniziata mediante un'[Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md) corrispondente.  
  
 `Property`  
 Necessaria per terminare una definizione di proprietà iniziata mediante un'[Property Statement](../../../visual-basic/language-reference/statements/property-statement.md) corrispondente.  
  
 `RaiseEvent`  
 Necessaria per terminare una funzione di accesso `RaiseEvent` iniziata mediante un'istruzione `RaiseEvent` corrispondente in un'[Event Statement](../../../visual-basic/language-reference/statements/event-statement.md) personalizzata.  
  
 `RemoveHandler`  
 Necessaria per terminare una funzione di accesso `RemoveHandler` iniziata mediante un'istruzione `RemoveHandler` corrispondente in un'[Event Statement](../../../visual-basic/language-reference/statements/event-statement.md) personalizzata.  
  
 `Select`  
 Necessaria per terminare una definizione di blocco `Select`...`Case` iniziata mediante un'istruzione `Select` corrispondente.  Vedere [Select...Case Statement](../../../visual-basic/language-reference/statements/select-case-statement.md).  
  
 `Set`  
 Necessaria per terminare una definizione di routine `Property` iniziata mediante un'[Set Statement](../../../visual-basic/language-reference/statements/set-statement.md) corrispondente.  Se durante l'esecuzione viene rilevata un'istruzione `End` `Set`, il controllo torna all'istruzione che imposta il valore della proprietà.  
  
 `Structure`  
 Necessaria per terminare una definizione di struttura iniziata mediante un'[Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md) corrispondente.  
  
 `Sub`  
 Necessaria per terminare una definizione di routine `Sub` iniziata mediante un'[Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md) corrispondente.  Se durante l'esecuzione viene rilevata un'istruzione `End` `Sub`, il controllo torna al codice chiamante.  
  
 `SyncLock`  
 Necessaria per terminare una definizione di blocco `SyncLock` iniziata mediante un'istruzione `SyncLock` corrispondente.  Vedere [SyncLock Statement](../../../visual-basic/language-reference/statements/synclock-statement.md).  
  
 `Try`  
 Necessaria per terminare una definizione di blocco `Try`...`Catch`...`Finally` iniziata mediante un'istruzione `Try` corrispondente.  Vedere [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
 `While`  
 Necessaria per terminare una definizione di ciclo `While` iniziata mediante un'istruzione `While` corrispondente.  Vedere [While...End While Statement](../../../visual-basic/language-reference/statements/while-end-while-statement.md).  
  
 `With`  
 Necessaria per terminare una definizione di blocco `With` iniziata mediante un'istruzione `With` corrispondente.  Vedere [With...End With Statement](../../../visual-basic/language-reference/statements/with-end-with-statement.md).  
  
## Note  
 Se non viene specificata alcuna parola chiave aggiuntiva, l'[End Statement](../../../visual-basic/language-reference/statements/end-statement.md) termina immediatamente l'esecuzione.  
  
 Quando è preceduta da un segno di numero \(`#`\), la parola chiave `End` termina un blocco di pre\-elaborazione introdotto dalla direttiva corrispondente.  
  
 `#End`  
 Obbligatorio.  Termina la definizione del blocco di pre\-elaborazione.  
  
 `#ExternalSource`  
 Necessaria per terminare un blocco di codice sorgente esterno iniziato mediante una [\#ExternalSource Directive](../../../visual-basic/language-reference/directives/externalsource-directive.md) corrispondente.  
  
 `#If`  
 Necessaria per terminare un blocco di compilazione condizionale iniziato mediante una direttiva `#If` corrispondente.  Vedere [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md).  
  
 `#Region`  
 Necessaria per terminare un blocco region sorgente iniziato mediante una [\#Region Directive](../../../visual-basic/language-reference/directives/region-directive.md) corrispondente.  
  
## Note per gli sviluppatori di applicazioni per Smart Device  
 Se non viene specificata alcuna parola chiave aggiuntiva, l'istruzione `End` non è supportata.  
  
## Vedere anche  
 [End Statement](../../../visual-basic/language-reference/statements/end-statement.md)