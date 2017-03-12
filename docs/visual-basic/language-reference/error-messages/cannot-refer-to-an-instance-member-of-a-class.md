---
title: "Cannot refer to an instance member of a class from within a shared method or shared member initializer without an explicit instance of the class | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30369"
  - "bc30369"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Shared"
  - "BC30369"
ms.assetid: 39d9466b-c1f3-4406-91a5-3d6c52d23a3d
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Cannot refer to an instance member of a class from within a shared method or shared member initializer without an explicit instance of the class
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Si è tentato di fare riferimento a un membro non condiviso di una classe dall'interno di una routine condivisa.  Nell'esempio riportato di seguito viene illustrata una situazione di questo tipo.  
  
```  
Class sample  
    Public x as Integer  
    Public Shared Sub setX()  
        x = 10  
    End Sub  
End Class  
```  
  
 Nell'esempio precedente l'istruzione di assegnazione `x = 10` genera il messaggio di errore  perché una routine condivisa tenta di accedere a una variabile di istanza.  
  
 La variabile `x` è un membro di istanza poiché non è dichiarata come [Shared](../../../visual-basic/language-reference/modifiers/shared.md).  Ciascuna istanza della classe `sample` contiene una specifica variabile `x`.  L'impostazione o la modifica del valore di `x` in un'istanza non influisce sul valore di `x` nelle altre istanze.  
  
 Tuttavia, la routine `setX` è `Shared` tra tutte le istanze della classe `sample`.  In altri termini, tale routine non è associata ad alcuna istanza della classe, ma funziona in modo indipendente dalle singole istanze.  Poiché la routine `setX` non è collegata a una specifica istanza, non può accedere a una variabile di istanza  e deve essere utilizzata solo per variabili `Shared`.  Quando `setX` imposta o modifica il valore di una variabile condivisa, il nuovo valore è disponibile per tutte le istanze della classe.  
  
 **ID errore:** BC30369  
  
### Per correggere l'errore  
  
1.  Stabilire se si desidera condividere un membro tra tutte le istanze della classe o mantenere un membro specifico per ciascuna istanza.  
  
2.  Per condividere un'unica copia del membro tra tutte le istanze, aggiungere la parola chiave `Shared` alla dichiarazione del membro.  Mantenere la parola chiave `Shared` nella dichiarazione della routine.  
  
3.  Per mantenere una specifica copia del membro per ciascuna istanza, non specificare `Shared` nella dichiarazione del membro.  Rimuovere la parola chiave `Shared` dalla dichiarazione della routine.  
  
## Vedere anche  
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)