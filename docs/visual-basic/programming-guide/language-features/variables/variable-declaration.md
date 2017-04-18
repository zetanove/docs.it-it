---
title: Dichiarazione di variabili in Visual Basic | Documenti di Microsoft
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
helpviewer_keywords:
- variables [Visual Basic], declaring
- member variables, declarations
- Dim statement, variable declaration
- declaring variables
- variables [Visual Basic], scope
- variables [Visual Basic], data types
- data types [Visual Basic], variable declarations
- lifetime, variables
- variables [Visual Basic], lifetime
- access levels, variables
- scope, declaration statements
- variables [Visual Basic], access level
- local variables, declarations
- scope, variables
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
caps.latest.revision: 31
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8cabb2d319288653c80099c816e46e822429d6ec
ms.lasthandoff: 03/13/2017

---
# <a name="variable-declaration-in-visual-basic"></a>Dichiarazione di variabili in Visual Basic
Si dichiara una variabile per specificare il nome e le caratteristiche. Istruzione di dichiarazione delle variabili è il [Dim (istruzione)](../../../../visual-basic/language-reference/statements/dim-statement.md). La posizione e il contenuto determinano le caratteristiche della variabile.  
  
 Per considerazioni e le regole di denominazione variabili, vedere [nomi di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## <a name="declaration-levels"></a>Livelli di dichiarazione  
  
### <a name="local-and-member-variables"></a>Locale e le variabili membro  
 Oggetto *variabile locale* è una variabile dichiarata all'interno di una routine. Oggetto *variabile membro* è un membro di un [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] di tipo viene dichiarato a livello di modulo, all'interno di una classe, struttura o un modulo, ma non all'interno di qualsiasi routine interne di tale classe, struttura o un modulo.  
  
### <a name="shared-and-instance-variables"></a>Condivisi e le variabili di istanza  
 In una classe o struttura, la categoria di una variabile membro dipende o meno è condiviso. Se viene dichiarata con la [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) (parola chiave), è un *variabile condivisa*, ed esiste una sola copia condivisa tra tutte le istanze della classe o struttura.  
  
 In caso contrario è un *variabile di istanza*, e viene creata una copia separata per ogni istanza della classe o struttura. È disponibile solo per l'istanza della classe o struttura in cui è stata creata una copia specifica di una variabile di istanza. È indipendente da una copia della variabile di istanza in qualsiasi altra istanza della classe o struttura.  
  
## <a name="declaring-data-type"></a>Dichiarazione del tipo di dati  
 Il [come](../../../../visual-basic/language-reference/statements/as-clause.md) clausola nell'istruzione di dichiarazione consente di definire il tipo di dati o un tipo di oggetto della variabile che si sta dichiarando. È possibile specificare uno dei seguenti tipi per una variabile:  
  
-   Digitare un dati elementari, ad esempio `Boolean`, `Long`, o`Decimal`  
  
-   Un tipo di dati composito, come una matrice o una struttura  
  
-   Un tipo di oggetto o una classe, definita nell'applicazione o in un'altra applicazione  
  
-   Oggetto [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] classe, ad esempio <xref:System.Windows.Forms.Label>o <xref:System.Windows.Forms.TextBox></xref:System.Windows.Forms.TextBox> </xref:System.Windows.Forms.Label>  
  
-   Tipo di un'interfaccia, ad esempio <xref:System.IComparable>o <xref:System.IDisposable></xref:System.IDisposable> </xref:System.IComparable>  
  
 È possibile dichiarare più variabili in un'unica istruzione senza dover ripetere il tipo di dati. Nelle istruzioni seguenti, le variabili `i`, `j`, e `k` vengono dichiarati come tipo `Integer`, `l` e `m` come `Long`, e `x` e `y` come `Single`:  
  
```  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 Per ulteriori informazioni sui tipi di dati, vedere [tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md). Per ulteriori informazioni sugli oggetti, vedere [oggetti e classi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md) e [programmazione con i componenti](http://msdn.microsoft.com/library/d4d4fcb4-e0b8-46b3-b679-7ee0026eb9e3).  
  
## <a name="local-type-inference"></a>Inferenza del tipo di variabile locale  
 *Inferenza del tipo* viene utilizzato per determinare i tipi di dati delle variabili locali dichiarate senza un `As` clausola. Il compilatore deduce il tipo della variabile dal tipo dell'espressione di inizializzazione. In questo modo è possibile dichiarare variabili senza dichiarare in modo esplicito un tipo. Nell'esempio seguente, entrambi `num1` e `num2` sono fortemente tipizzati come integer.  
  
 [!code-vb[VbVbalrTypeInference n.&1;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/variable-declaration_1.vb)]  
  
 Se si desidera utilizzare l'inferenza del tipo locale, `Option Infer` deve essere impostato su `On`. Per ulteriori informazioni, vedere [l'inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) e [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
## <a name="characteristics-of-declared-variables"></a>Caratteristiche delle variabili dichiarate  
 Il *durata* di una variabile è il periodo di tempo durante il quale essa è disponibile per l'utilizzo. In generale, esiste una variabile, purché l'elemento che lo dichiara (ad esempio, una procedura o una classe) continua a esistere. Se la variabile non è necessario continuare oltre la durata dell'elemento contenitore esistente, non occorre eseguire alcuna azione speciale nella dichiarazione. Se la variabile deve continuare a esistere più rispetto all'elemento contenitore, è possibile includere il `Static` o `Shared` (parola chiave) nel relativo `Dim` istruzione. Per ulteriori informazioni, vedere [durata in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md).  
  
 Il *ambito* è il set di tutto il codice che è possibile farvi riferimento senza la qualifica del nome di una variabile. Ambito di una variabile è determinato in cui è dichiarata. Il codice di una determinata area è possibile utilizzare le variabili definite in tale area senza la necessità di qualificare i nomi. Per ulteriori informazioni, vedere [ambito in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md).  
  
 Una variabile *livello di accesso* è l'ambito del codice che dispone dell'autorizzazione per accedervi. Ciò è determinato dal modificatore di accesso (ad esempio [pubblica](../../../../visual-basic/language-reference/modifiers/public.md) o [privata](../../../../visual-basic/language-reference/modifiers/private.md)) utilizzato nel `Dim` istruzione. Per ulteriori informazioni, vedere [livelli di accesso in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: creare una nuova variabile](../../../../visual-basic/programming-guide/language-features/variables/how-to-create-a-new-variable.md)   
 [Procedura: spostare i dati in e da una variabile](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)   
 [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Protetto](../../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)   
 [Statico](../../../../visual-basic/language-reference/modifiers/static.md)   
 [Caratteristiche di elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [Inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Istruzione Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
