---
title: "Default property access is ambiguous between the inherited interface members &#39;&lt;defaultpropertyname&gt;&#39; of interface &#39;&lt;interfacename1&gt;&#39; and &#39;&lt;defaultpropertyname&gt;&#39; of interface &#39;&lt;interfacename2&gt;&#39; | Microsoft Docs"
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
  - "vbc30686"
  - "bc30686"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30686"
ms.assetid: 784fefec-ef57-48cf-b960-957df419b439
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Default property access is ambiguous between the inherited interface members &#39;&lt;defaultpropertyname&gt;&#39; of interface &#39;&lt;interfacename1&gt;&#39; and &#39;&lt;defaultpropertyname&gt;&#39; of interface &#39;&lt;interfacename2&gt;&#39;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'interfaccia eredita da due interfacce, ciascuna delle quali dichiara una proprietà predefinita con lo stesso nome.  Il compilatore non è in grado di risolvere un accesso alla proprietà predefinita senza qualificazione.  Questa condizione è illustrata nell'esempio che segue.  
  
```  
Public Interface Iface1  
    Default Property prop(ByVal arg As Integer) As Integer  
End Interface  
Public Interface Iface2  
    Default Property prop(ByVal arg As Integer) As Integer  
End Interface  
Public Interface Iface3  
    Inherits Iface1, Iface2  
End Interface  
Public Class testClass  
    Public Sub accessDefaultProperty()  
        Dim testObj As Iface3  
        Dim testInt As Integer = testObj(1)  
    End Sub  
End Class  
```  
  
 Quando si specifica `testObj(1)`, il compilatore tenta di risolverlo nella proprietà predefinita.  Poiché per la presenza delle interfacce ereditate sono presenti due possibili proprietà predefinite, il compilatore segnala l'errore.  
  
 **ID errore:** BC30686  
  
### Per correggere l'errore  
  
-   Evitare di ereditare membri con lo stesso nome.  Nell'esempio precedente, se `testObj` non richiede alcun membro di `Iface2`, è possibile dichiararlo nel modo seguente:  
  
    ```  
    Dim testObj As Iface1  
    ```  
  
     In alternativa  
  
-   Implementare l'interfaccia che eredita in una classe.  È quindi possibile implementare ciascuna delle proprietà ereditate con nomi diversi.  Solo una di tali proprietà, tuttavia, può essere specificata come proprietà predefinita della classe di implementazione.  Questa condizione è illustrata nell'esempio che segue.  
  
    ```  
    Public Class useIface3  
        Implements Iface3  
        Default Public Property prop1(ByVal arg As Integer) As Integer Implements Iface1.prop  
            ' Insert code to define Get and Set procedures for prop1.  
        End Property  
        Public Property prop2(ByVal arg As Integer) As Integer Implements Iface2.prop  
            ' Insert code to define Get and Set procedures for prop2.  
        End Property  
    End Class  
    ```  
  
## Vedere anche  
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)