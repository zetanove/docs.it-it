---
title: "How to: Determine What Type an Object Variable Refers To (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "TypeOf operator [Visual Basic], determining object variable type"
  - "variables [Visual Basic], object"
  - "object variables, determining type"
ms.assetid: 6f6a138d-58a4-40d1-9f4e-0a3c598eaf81
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# How to: Determine What Type an Object Variable Refers To (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una variabile oggetto contiene un puntatore a dati archiviati in un'altra posizione.  Il tipo di questi dati può cambiare in fase di esecuzione.  In qualsiasi momento, è possibile utilizzare il metodo <xref:System.Type.GetTypeCode%2A> per individuare il tipo corrente in fase di esecuzione o l'[TypeOf Operator](../../../../visual-basic/language-reference/operators/typeof-operator.md) per determinare se tale tipo è compatibile con un tipo specificato.  
  
### Per determinare il tipo esatto a cui fa attualmente riferimento una variabile oggetto  
  
1.  Nella variabile oggetto chiamare il metodo <xref:System.Object.GetType%2A> per recuperare un oggetto <xref:System.Type?displayProperty=fullName>.  
  
    ```  
    Dim myObject As Object  
    myObject.GetType()  
    ```  
  
2.  Nella classe <xref:System.Type?displayProperty=fullName> chiamare il metodo condiviso <xref:System.Type.GetTypeCode%2A> per recuperare il valore di enumerazione <xref:System.TypeCode> per il tipo dell'oggetto.  
  
    ```  
    Dim myObject As Object  
    Dim datTyp As Integer = Type.GetTypeCode(myObject.GetType())  
    MsgBox("myObject currently has type code " & CStr(datTyp))  
    ```  
  
     È possibile testare il valore di enumerazione <xref:System.TypeCode> rispetto a un qualsiasi membro di enumerazione, ad esempio `Double`.  
  
### Per determinare se il tipo di una variabile oggetto è compatibile con un tipo specificato  
  
-   Utilizzare l'operatore `TypeOf` insieme all'[Is Operator](../../../../visual-basic/language-reference/operators/is-operator.md) per testare l'oggetto con un'espressione `TypeOf`...`Is`.  
  
    ```  
    If TypeOf objA Is System.Windows.Forms.Control Then  
        MsgBox("objA is compatible with the Control class")  
    End If  
    ```  
  
     L'espressione `TypeOf`...`Is` restituisce `True` se il tipo in fase di esecuzione dell'oggetto è compatibile con il tipo specificato.  
  
     Il criterio per la compatibilità varia a seconda che il tipo specificato sia una classe, una struttura o un'interfaccia.  In generale, i tipi sono compatibili se il tipo dell'oggetto corrisponde al tipo specificato oppure se l'oggetto eredita o implementa il tipo specificato.  Per ulteriori informazioni, vedere [TypeOf Operator](../../../../visual-basic/language-reference/operators/typeof-operator.md).  
  
## Compilazione del codice  
 Tenere presente che il tipo specificato non può essere una variabile o un'espressione,  ma deve essere il nome di un tipo definito, ad esempio una classe, una struttura o un'interfaccia,  inclusi i tipi intrinseci quali `Integer` e `String`.  
  
## Vedere anche  
 <xref:System.Object.GetType%2A>   
 <xref:System.Type?displayProperty=fullName>   
 <xref:System.Type.GetTypeCode%2A>   
 <xref:System.TypeCode>   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Values](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)