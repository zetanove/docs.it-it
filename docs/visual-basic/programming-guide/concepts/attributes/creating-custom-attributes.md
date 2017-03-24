---
title: Creazione di attributi personalizzati (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 5c9ef584-6c7c-496b-92a9-6e42f8d9ca28
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1aa97a591fdbdfab931a8b5e4f70ec3c00762332
ms.lasthandoff: 03/13/2017

---
# <a name="creating-custom-attributes-visual-basic"></a>Creazione di attributi personalizzati (Visual Basic)
È possibile creare attributi personalizzati definendo una classe attribute, una classe che deriva direttamente o indirettamente da <xref:System.Attribute>, rendendo identificazione delle definizioni degli attributi nei metadati più facili e veloci.</xref:System.Attribute> Si supponga che si desidera contrassegnare i tipi con il nome del programmatore che ha creato il tipo. È possibile definire un oggetto personalizzato `Author` attributo classe:  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.Class Or   
                       System.AttributeTargets.Struct)>   
Public Class Author  
    Inherits System.Attribute  
    Private name As String  
    Public version As Double  
    Sub New(ByVal authorName As String)  
        name = authorName  
        version = 1.0  
    End Sub  
End Class  
```  
  
 Il nome della classe è il nome dell'attributo, `Author`. Deriva da `System.Attribute`, pertanto è una classe di attributi personalizzati. I parametri del costruttore sono parametri posizionali dell'attributo personalizzato. In questo esempio, `name` è un parametro posizionale. Qualsiasi proprietà o campi pubblici di lettura / scrittura sono parametri denominate. In questo caso, `version` è l'unico parametro denominato. Si noti l'utilizzo di `AttributeUsage` attributo per rendere il `Author` attributo valido solo sulla classe e `Structure` dichiarazioni.  
  
 È possibile utilizzare il nuovo attributo, come indicato di seguito:  
  
```vb  
<Author("P. Ackerman", Version:=1.1)>   
Class SampleClass  
    ' P. Ackerman's code goes here...  
End Class  
```  
  
 `AttributeUsage`ha un parametro denominato `AllowMultiple`, che consente di rendere multiuso un attributo personalizzato a utilizzo singolo o multiuso. Nell'esempio di codice seguente viene creato un attributo multiuso.  
  
```vb  
' multiuse attribute  
<System.AttributeUsage(System.AttributeTargets.Class Or   
                       System.AttributeTargets.Struct,   
                       AllowMultiple:=True)>   
Public Class Author  
    Inherits System.Attribute  
```  
  
 Nell'esempio di codice seguente, a una classe vengono applicati più attributi dello stesso tipo.  
  
```vb  
<Author("P. Ackerman", Version:=1.1),   
Author("R. Koch", Version:=1.2)>   
Class SampleClass  
    ' P. Ackerman's code goes here...  
    ' R. Koch's code goes here...  
End Class  
```  
  
> [!NOTE]
>  Se la classe di attributo contiene una proprietà, tale proprietà deve essere in lettura / scrittura.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Reflection></xref:System.Reflection>   
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)   
 [Scrittura di attributi personalizzati](http://msdn.microsoft.com/library/97216f69-bde8-49fd-ac40-f18c500ef5dc)   
 [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [Attributi (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)   
 [Accesso agli attributi tramite Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)   
 [AttributeUsage (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/attributeusage.md)
