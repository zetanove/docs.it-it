---
title: 'Procedura: creare un&quot;unione C C++ tramite attributi (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 9352a7e4-c0da-4d07-aa14-55ed43736fcb
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3ff1686328630b233b25839c79d0009d48aab5ab
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-cc-union-by-using-attributes-visual-basic"></a>Procedura: creare un'unione C/C++ tramite attributi (Visual Basic)
Utilizzando gli attributi è possibile personalizzare come struct sono disposti nella memoria. Ad esempio, è possibile creare ciò che viene definito un operatore union in C/C++ tramite il `StructLayout(LayoutKind.Explicit)` e `FieldOffset` gli attributi.  
  
## <a name="example"></a>Esempio  
 In questo segmento di codice, tutti i campi di `TestUnion` start nella stessa posizione in memoria.  
  
```vb  
' Add an Imports statement for System.Runtime.InteropServices.  
  
<System.Runtime.InteropServices.StructLayout(   
      System.Runtime.InteropServices.LayoutKind.Explicit)>   
Structure TestUnion  
    <System.Runtime.InteropServices.FieldOffset(0)>   
    Public i As Integer  
  
    <System.Runtime.InteropServices.FieldOffset(0)>   
    Public d As Double  
  
    <System.Runtime.InteropServices.FieldOffset(0)>   
    Public c As Char  
  
    <System.Runtime.InteropServices.FieldOffset(0)>   
    Public b As Byte  
End Structure  
```  
  
## <a name="example"></a>Esempio  
 Di seguito è un altro esempio in cui campi iniziano in diversi imposta in modo esplicito i percorsi.  
  
```vb  
' Add an Imports statement for System.Runtime.InteropServices.  
  
 <System.Runtime.InteropServices.StructLayout(   
      System.Runtime.InteropServices.LayoutKind.Explicit)>   
Structure TestExplicit  
     <System.Runtime.InteropServices.FieldOffset(0)>   
     Public lg As Long  
  
     <System.Runtime.InteropServices.FieldOffset(0)>   
     Public i1 As Integer  
  
     <System.Runtime.InteropServices.FieldOffset(4)>   
     Public i2 As Integer  
  
     <System.Runtime.InteropServices.FieldOffset(8)>   
     Public d As Double  
  
     <System.Runtime.InteropServices.FieldOffset(12)>   
     Public c As Char  
  
     <System.Runtime.InteropServices.FieldOffset(14)>   
     Public b As Byte  
 End Structure  
```  
  
 I due campi integer, `i1` e `i2`, condividono le stesse posizioni di memoria di `lg`. Questo tipo di controllo sul layout struttura è utile quando si utilizza la chiamata di piattaforma.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection></xref:System.Reflection>   
 <xref:System.Attribute></xref:System.Attribute>   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)   
 [Attributi](https://msdn.microsoft.com/library/5x6cd29c)   
 [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [Attributi (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)   
 [Creazione di attributi personalizzati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md)   
 [Accesso agli attributi tramite Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
