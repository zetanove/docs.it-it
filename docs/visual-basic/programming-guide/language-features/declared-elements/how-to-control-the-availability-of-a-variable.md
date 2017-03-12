---
title: "How to: Control the Availability of a Variable (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "access levels, declared elements"
  - "Private keyword, accessing variables"
  - "access levels, variables"
  - "Public keyword, accessing variables"
  - "Friend keyword, accessing variables"
  - "variables [Visual Basic], access level"
  - "declared elements, access level"
  - "Protected keyword, accessing variables"
ms.assetid: eaf4f073-7922-43ce-ae1e-90ff376ae947
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Control the Availability of a Variable (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile controllare la disponibilità di una variabile specificando il relativo *livello di accesso*.  Il livello di accesso determina quali parti di codice dispongono delle autorizzazioni di lettura e scrittura sulla variabile.  
  
-   Le *variabili membro* \(definite a livello di modulo e all'esterno di una qualsiasi routine\) vengono impostate automaticamente sull'accesso pubblico. Questo significa che tali variabili sono accessibili da qualsiasi codice in cui sono visibili.  Per modificare questa impostazione è possibile specificare un modificatore di accesso.  
  
-   Le *variabili locali* \(definite all'interno di una routine\) dovrebbero avere accesso pubblico, ma in realtà sono accessibili soltanto dal codice all'interno della routine in cui sono dichiarate.  Non è possibile modificare il livello di accesso di una variabile locale, ma è possibile modificare quello della routine che la contiene.  
  
 Per ulteriori informazioni, vedere [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## Accesso pubblico e privato  
  
#### Per rendere una variabile accessibile soltanto dall'interno del modulo, della classe o della struttura in cui è dichiarata  
  
1.  Inserire l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) relativa alla variabile all'interno del modulo, della classe o della struttura ma all'esterno di una qualsiasi routine.  
  
2.  Includere la parola chiave [Private](../../../../visual-basic/language-reference/modifiers/private.md) nell'istruzione `Dim`.  
  
     È possibile fare riferimento alla variabile da qualsiasi punto all'interno del modulo, della classe o della struttura, ma non dall'esterno.  
  
#### Per rendere una variabile accessibile da qualsiasi codice in cui è visibile  
  
1.  Per una variabile membro, inserire l'istruzione `Dim` relativa alla variabile all'interno di un modulo, di una classe o di una struttura, ma all'esterno di una qualsiasi routine.  
  
2.  Includere la parola chiave [Public](../../../../visual-basic/language-reference/modifiers/public.md) nell'istruzione `Dim`.  
  
     È possibile fare riferimento alla variabile da qualsiasi codice che interagisca con l'assembly in uso.  
  
 In alternativa  
  
1.  Per una variabile locale, inserire l'istruzione `Dim` relativa alla variabile all'interno di una routine.  
  
2.  Non includere la parola chiave `Public` nell'istruzione `Dim`.  
  
     È possibile fare riferimento alla variabile da qualsiasi punto all'interno della routine, ma non dall'esterno.  
  
## Accesso Protected e Friend  
 È possibile limitare il livello di accesso di una variabile alla relativa classe e alle eventuali classi derivate oppure al relativo assembly.  È anche possibile specificare entrambe queste limitazioni, in modo da consentire l'accesso da qualsiasi classe derivata o da qualsiasi altro punto nello stesso assembly.  A questo scopo è necessario combinare le parole chiave `Protected` e `Friend` nella stessa dichiarazione.  
  
#### Per rendere una variabile accessibile soltanto dall'interno della relativa classe e da eventuali classi derivate  
  
1.  Inserire l'istruzione `Dim` relativa alla variabile all'interno di una classe, ma all'esterno di una qualsiasi routine.  
  
2.  Includere la parola chiave [Protected](../../../../visual-basic/language-reference/modifiers/protected.md) nell'istruzione `Dim`.  
  
     È possibile fare riferimento alla variabile da qualsiasi punto all'interno della classe nonché da qualsiasi classe derivata, ma non dall'esterno di una classe inclusa nella catena di derivazione.  
  
#### Per rendere accessibile una variabile soltanto dall'interno dello stesso assembly  
  
1.  Inserire l'istruzione `Dim` relative alla variabile all'interno di un modulo, di una classe o di una struttura, ma all'esterno di una qualsiasi routine.  
  
2.  Includere la parola chiave [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) nell'istruzione `Dim`.  
  
     È possibile fare riferimento alla variabile da qualsiasi punto all'interno del modulo, della classe o della struttura, nonché da qualsiasi codice nello stesso assembly, ma non dall'esterno dell'assembly.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrate alcune dichiarazioni di variabili con livelli di accesso `Public`, `Protected`, `Friend`, `Protected Friend` e `Private`.  Quando l'istruzione `Dim` specifica un livello di accesso, non è necessario includere la parola chiave `Dim`.  
  
```  
Public Class classForEverybody  
Protected Class classForMyHeirs  
Friend stringForThisProject As String  
Protected Friend stringForProjectAndHeirs As String  
Private numberForMeOnly As Integer  
```  
  
## Sicurezza di .NET Framework  
 Più restrittivo è il livello di accesso di una variabile, minori saranno le probabilità che la variabile possa essere utilizzata in modo improprio da un codice dannoso.  
  
## Vedere anche  
 [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Public](../../../../visual-basic/language-reference/modifiers/public.md)   
 [Protected](../../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../../visual-basic/language-reference/modifiers/private.md)