---
title: "Data type(s) of the type parameter(s) cannot be inferred from these arguments | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36644"
  - "bc36647"
  - "vbc36647"
  - "vbc36644"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36644"
  - "BC36647"
ms.assetid: 0e0050f2-2039-4311-b260-f0ebfde84189
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Data type(s) of the type parameter(s) cannot be inferred from these arguments
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Impossibile dedurre da questi argomenti i tipi di dati dei parametri di tipo.L'errore potrebbe essere corretto specificando i tipi di dati in modo esplicito.  
  
 Questo errore si verifica quando la risoluzione dell'overload non riesce.  Si verifica come messaggio subordinato in cui viene indicato il motivo per cui un determinato elemento dell'overload è stato eliminato.  Nel messaggio di errore viene descritto che il compilatore non è in grado di utilizzare l'inferenza dei tipi per individuare i tipi di dati per i parametri di tipo.  
  
> [!NOTE]
>  Quando è obbligatorio specificare gli argomenti, ad esempio per gli operatori di query nelle espressioni di query, il messaggio di errore viene visualizzato senza la seconda frase.  
  
 L'errore viene illustrato nel codice riportato di seguito.  
  
```vb#  
Module Module1  
  
    Sub Main()  
  
        '' Not Valid.  
        'OverloadedGenericMethod("Hello", "World")  
  
    End Sub  
  
    Sub OverloadedGenericMethod(Of T)(ByVal x As String,   
                                      ByVal y As InterfaceExample(Of T))  
    End Sub  
  
    Sub OverloadedGenericMethod(Of T, R)(ByVal x As T,   
                                         ByVal y As InterfaceExample(Of R))  
    End Sub  
  
End Module  
  
Interface InterfaceExample(Of T)  
End Interface  
```  
  
 **ID errore:** BC36647 e BC36644  
  
### Per correggere l'errore  
  
-   È possibile specificare un tipo di dati per il parametro o i parametri di tipo anziché basarsi sull'inferenza dei tipi.  
  
## Vedere anche  
 [Relaxed Delegate Conversion](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [Generic Procedures in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)   
 [Type Conversions in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)