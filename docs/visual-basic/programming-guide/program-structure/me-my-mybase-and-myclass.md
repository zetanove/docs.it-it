---
title: Me, My, MyBase e MyClass in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- MyClass
- vb.Me
- MyBase
- vb.MyBase
- Me
- vb.MyClass
- vb.This
- vb.My
dev_langs:
- VB
helpviewer_keywords:
- My object
- self-reference, Me keyword
- MyClass keyword, relationship to similar programming elements
- Me keyword, relationship to similar programming elements
- Me keyword, referring to the current instance of an object
- Me keyword
- self-reference
- current instance, Me keyword
- MyBase keyword, relationship to similar programming elements
ms.assetid: f8e241ae-b1ed-4886-9aa0-08c632154029
caps.latest.revision: 15
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 59dba8961712537367db9a60e8b8ba68bcb6a1ea
ms.lasthandoff: 03/13/2017

---
# <a name="me-my-mybase-and-myclass-in-visual-basic"></a>Me, My, MyBase e MyClass in Visual Basic
`Me`, `My`, `MyBase`, e `MyClass` in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] hanno nomi simili, ma scopi diversi. Viene descritta ciascuna di queste entità per distinguerli.  
  
## <a name="me"></a>Me  
 Il `Me` (parola chiave) fornisce un modo per fare riferimento all'istanza specifica di una classe o struttura in cui è attualmente in esecuzione il codice. `Me`si comporta come una variabile oggetto o una variabile di struttura che fa riferimento all'istanza corrente. Utilizzando `Me` è particolarmente utile per passare informazioni relative all'istanza attualmente in esecuzione di una classe o struttura a una routine in un'altra classe, struttura o un modulo.  
  
 Ad esempio, si supponga di che avere la seguente procedura in un modulo.  
  
```  
Sub ChangeFormColor(FormName As Form)  
   Randomize()  
   FormName.BackColor = Color.FromArgb(Rnd() * 256, Rnd() * 256, Rnd() * 256)  
End Sub  
```  
  
 È possibile chiamare la routine e passare l'istanza corrente della <xref:System.Windows.Forms.Form>classe come un argomento tramite l'istruzione seguente.</xref:System.Windows.Forms.Form>  
  
```  
ChangeFormColor(Me)  
```  
  
## <a name="my"></a>My  
 Il `My` funzionalità fornisce un accesso semplice e intuitivo per un numero di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] classi, consentendo il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] utente di interagire con il computer, applicazioni, impostazioni, risorse e così via.  
  
## <a name="mybase"></a>MyBase  
 Il `MyBase` (parola chiave) si comporta come una variabile oggetto che fa riferimento alla classe di base dell'istanza corrente di una classe. `MyBase`viene comunemente utilizzato per accedere ai membri di classe di base sottoposti a override o nascosti in una classe derivata. `MyBase.New`viene utilizzato per chiamare in modo esplicito un costruttore di classe di base da un costruttore di classe derivata.  
  
## <a name="myclass"></a>MyClass  
 Il `MyClass` (parola chiave) si comporta come una variabile oggetto che fa riferimento all'istanza corrente di una classe implementata originariamente. `MyClass`è simile a `Me`, ma tutte le chiamate al metodo su di essa sono trattate come se fosse il metodo `NotOverridable`.  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali sull'ereditarietà](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
