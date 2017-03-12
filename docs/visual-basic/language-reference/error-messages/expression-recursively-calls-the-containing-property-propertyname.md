---
title: "Expression recursively calls the containing property &#39;&lt;propertyname&gt;&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc42026"
  - "BC42026"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42026"
ms.assetid: 4fde9db6-3bf3-48dc-8e05-981bf08969da
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Expression recursively calls the containing property &#39;&lt;propertyname&gt;&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'istruzione nella routine `Set` di una definizione di proprietà archivia un valore nel nome della proprietà.  
  
 Per contenere il valore di una proprietà si consiglia di definire una variabile `Private` nel contenitore della proprietà e di utilizzarla sia nella routine `Get` sia nella routine `Set`.  La routine `Set` deve archiviare, quindi, il valore in entrata nella variabile `Private`.  
  
 La routine `Get` si comporta come una routine `Function`, quindi può assegnare un valore al nome della proprietà e restituire il controllo in corrispondenza dell'istruzione `End Get`.  Si consiglia, tuttavia, di includere la variabile `Private` come valore nell'istruzione [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md).  
  
 La routine `Set` si comporta come una routine `Sub`, che non restituisce alcun valore.  Di conseguenza, il nome della routine o della proprietà non ha un significato particolare all'interno di una routine `Set` e non è possibile archiviarvi alcun valore.  
  
 Nell'esempio seguente viene illustrato il tipo di approccio che può causare questo tipo di errore, seguito da quello consigliato.  
  
```  
Public Class illustrateProperties  
' The code in the following property causes this error.  
    Public Property badProp() As Char  
        Get  
            Dim charValue As Char  
            ' Insert code to update charValue.  
            badProp = charValue  
        End Get  
        Set(ByVal Value As Char)  
            ' The following statement causes this error.  
            badProp = Value  
            ' The value stored in the local variable badProp  
            ' is not used by the Get procedure in this property.  
        End Set  
    End Property  
' The following code uses the recommended approach.  
    Private propValue As Char  
    Public Property goodProp() As Char  
        Get  
            ' Insert code to update propValue.  
            Return propValue  
        End Get  
        Set(ByVal Value As Char)  
            propValue = Value  
        End Set  
    End Property  
End Class  
```  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42026  
  
### Per correggere l'errore  
  
-   Riscrivere la definizione di proprietà per utilizzare il metodo consigliato come illustrato nell'esempio precedente.  
  
## Vedere anche  
 [Routine Property](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Set Statement](../../../visual-basic/language-reference/statements/set-statement.md)