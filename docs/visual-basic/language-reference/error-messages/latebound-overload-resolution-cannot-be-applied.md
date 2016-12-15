---
title: "Latebound overload resolution cannot be applied to &#39;&lt;procedurename&gt;&#39; because the accessing instance is an interface type | Microsoft Docs"
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
  - "vbc30933"
  - "bc30933"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "overload resolution, with late-bound argument"
  - "BC30933"
ms.assetid: 8182eea0-dd34-4d6e-9ca0-41d8713e9dc4
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Latebound overload resolution cannot be applied to &#39;&lt;procedurename&gt;&#39; because the accessing instance is an interface type
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il compilatore sta tentando di risolvere un riferimento a una proprietà o una routine in overload, ma il riferimento non ha esito positivo perché un argomento è di tipo `Object` e l'oggetto che fa riferimento ha il tipo di dati di un'interfaccia.  L'argomento `Object` induce il compilatore a risolvere il riferimento come elemento ad associazione tardiva.  
  
 In queste condizioni, il compilatore risolve l'overload attraverso la classe di implementazione anziché attraverso l'interfaccia sottostante.  Se la classe rinomina una delle versioni in overload, il compilatore non considera quella versione come overload perché il suo nome è diverso.  Di conseguenza, il compilatore ignora la versione rinominata quando invece sarebbe stato opportuno elaborarla per risolvere il riferimento.  
  
 **ID errore:** BC30933  
  
### Per correggere l'errore  
  
-   Utilizzare `CType` per eseguire il cast dell'argomento da `Object` al tipo specificato dalla firma dell'overload da chiamare.  
  
     Si noti che non serve eseguire il cast dell'oggetto che fa riferimento sull'interfaccia sottostante.  È necessario eseguire il cast dell'argomento per evitare questo errore.  
  
## Esempio  
 Nell'esempio seguente viene illustrata una chiamata a una routine `Sub` in overload che genera questo errore in fase di compilazione.  
  
```  
Module m1  
    Interface i1  
        Sub s1(ByVal p1 As Integer)  
        Sub s1(ByVal p1 As Double)  
    End Interface  
    Class c1  
        Implements i1  
        Public Overloads Sub s1(ByVal p1 As Integer) Implements i1.s1  
        End Sub  
        Public Overloads Sub s2(ByVal p1 As Double) Implements i1.s1  
        End Sub  
    End Class  
    Sub Main()  
        Dim refer As i1 = New c1  
        Dim o1 As Object = 3.1415  
        ' The following reference is INVALID and causes a compiler error.  
        refer.s1(o1)   
    End Sub  
End Module  
```  
  
 Nell'esempio precedente, se il compilatore consentisse la chiamata a `s1` come è scritto, la risoluzione avverrebbe attraverso la classe `c1` anziché attraverso l'interfaccia `i1`.  Di conseguenza il compilatore non prenderebbe in considerazione `s2` in quanto ha un nome diverso in `c1`, anche se sarebbe la scelta corretta secondo quanto definito da `i1`.  
  
 È possibile correggere l'errore modificando la chiamata a una delle seguenti righe di codice:  
  
```  
refer.s1(CType(o1, Integer))  
refer.s1(CType(o1, Double))  
```  
  
 Ciascuna delle righe di codice precedenti esegue esplicitamente il cast della variabile `Object` `o1` su uno dei tipi di parametro definiti per gli overload.  
  
## Vedere anche  
 [Procedure Overloading](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Overload Resolution](../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [Funzione CType](../../../visual-basic/language-reference/functions/ctype-function.md)