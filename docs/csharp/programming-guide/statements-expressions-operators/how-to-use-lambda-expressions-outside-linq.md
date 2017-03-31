---
title: 'Procedura: Usare espressioni lambda al di fuori di LINQ (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- lambda expressions [C#], outside LINQ
ms.assetid: 2b519274-6ee4-4455-ab2e-aed67dbfd07c
caps.latest.revision: 12
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 54e1c54c0fe06847a5d36ca1e58b21884880bc3c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-lambda-expressions-outside-linq-c-programming-guide"></a>Procedura: utilizzare espressioni lambda al di fuori di LINQ (Guida per programmatori C#)
Le espressioni lambda non sono limitate alle query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)]. È possibile usarle dove è previsto un valore delegate, ovvero dove può essere usato un metodo anonimo. Nell'esempio seguente viene illustrato come usare un'espressione lambda in un gestore eventi Windows Forms. Si noti che i tipi degli input (<xref:System.Object> e <xref:System.Windows.Forms.MouseEventArgs>) vengono dedotti dal compilatore e non devono essere forniti in modo esplicito nei parametri di input delle espressioni lambda.  
  
## <a name="example"></a>Esempio  
  
```  
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
        // Use a lambda expression to define an event handler.  
       this.Click += (s, e) => { MessageBox.Show(((MouseEventArgs)e).Location.ToString());};  
    }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [LINQ (Language-Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)
