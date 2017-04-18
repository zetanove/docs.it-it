---
title: "Overload di metodi e proprietà (Visual Basic) | Documenti di Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- properties [Visual Basic], overloading
- methods [Visual Basic], overloading
- shadowing
- names, multiple procedures with same
- procedures, mulltiples with same name
- classes [Visual Basic], properties
- classes [Visual Basic], methods
- method overloading
- Overloads keyword, overloaded members
ms.assetid: b686fb97-e7d7-4001-afaa-6650cba08f0d
caps.latest.revision: 12
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
ms.openlocfilehash: 6f379f04ca9b75161baf2bf2c33e87f05a9edf97
ms.lasthandoff: 03/13/2017

---
# <a name="overloaded-properties-and-methods-visual-basic"></a>Metodi e proprietà di overload (Visual Basic)
Eseguire l'overload è la creazione di più routine, un costruttore di istanza o proprietà in una classe con lo stesso nome ma con diversi tipi di argomento.  
  
## <a name="overloading-usage"></a>Utilizzo dell'overload  
 L'overload è particolarmente utile quando il modello a oggetti impone l'utilizzo di nomi identici per routine che operano sui tipi di dati diversi. Ad esempio, una classe che è possibile visualizzare diversi tipi di dati può presentare `Display` procedure simili al seguente:  
  
 [!code-vb[&#64; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_1.vb)]  
  
 Senza l'overload, sarebbe necessario creare nomi distinti per ogni procedura, anche se si eseguono la stessa operazione, come indicato di seguito:  
  
 [!code-vb[VbVbalrOOP&#65;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_2.vb)]  
  
 L'overload, è facile utilizzare metodi o proprietà in quanto fornisce una scelta dei tipi di dati che può essere utilizzato. Ad esempio, il metodo di overload `Display` metodo descritto in precedenza può essere chiamato con una qualsiasi delle righe di codice seguenti:  
  
 [!code-vb[VbVbalrOOP&#66;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_3.vb)]  
  
 In fase di esecuzione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] specifichino la procedura corretta in base ai tipi di dati dei parametri è.  
  
## <a name="overloading-rules"></a>Regole di overload  
 Creare un membro di overload per una classe mediante l'aggiunta di due o più proprietà o metodi con lo stesso nome. Ad eccezione dei membri derivati, ogni membro di overload deve avere elenchi di parametri diversi e gli elementi seguenti non possono essere utilizzati come caratteristica di differenziazione quando l'overload di una proprietà o routine:  
  
-   Modificatori, ad esempio `ByVal` o `ByRef`, che si applicano a un membro o i parametri del membro.  
  
-   Nomi dei parametri  
  
-   Tipi restituiti di procedure  
  
 Il `Overloads` parola chiave è facoltativa quando l'overload, ma eventuali overload membro utilizza il `Overloads` (parola chiave), quindi tutti gli altri membri in overload con lo stesso nome devono inoltre specificare questa parola chiave.  
  
 Le classi derivate possono eseguire l'overload di membri ereditati con membri che hanno parametri identici e tipi di parametro, un processo noto come *shadowing in base al nome e la firma*. Se il `Overloads` parola chiave viene utilizzata quando shadowing in base al nome e la firma, implementazione della classe derivata del membro sarà usato al posto di implementazione nella classe di base e tutti gli altri overload per tale membro sarà disponibile per le istanze della classe derivata.  
  
 Se il `Overloads` parola chiave viene omessa quando l'overload di un membro ereditato con un membro che dispone di parametri identici e tipi di parametro, quindi viene chiamato l'overload *shadowing in base al nome*. Shadowing in base al nome sostituisce l'implementazione ereditata di un membro e rende disponibili per le istanze della classe derivata e i relativi discendenti tutti gli altri overload.  
  
 Il `Overloads` e `Shadows` i modificatori non utilizzati con lo stesso metodo o proprietà.  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente consente di creare metodi di overload che accettano un un `String` o `Decimal` rappresentazione di un importo in dollari e restituiscono una stringa contenente l'IVA.  
  
##### <a name="to-use-this-example-to-create-an-overloaded-method"></a>Utilizzare questo esempio per creare un metodo di overload  
  
1.  Aprire un nuovo progetto e aggiungere una classe denominata `TaxClass`.  
  
2.  Aggiungere il codice seguente alla classe `TaxClass`.  
  
     [!code-vb[VbVbalrOOP&#67;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_4.vb)]  
  
3.  Aggiungere la seguente procedura per il form.  
  
     [!code-vb[VbVbalrOOP&#68;](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_5.vb)]  
  
4.  Aggiungere un pulsante al form e chiamare il `ShowTax` procedura il `Button1_Click` evento del pulsante.  
  
5.  Eseguire il progetto e fare clic sul pulsante nel form per testare il metodo di overload `ShowTax` procedura.  
  
 In fase di esecuzione, il compilatore sceglie la funzione di overload appropriata che corrisponde ai parametri utilizzati. Quando si fa clic sul pulsante, il metodo di overload viene innanzitutto chiamato con un `Price` parametro che è una stringa e il messaggio "prezzo è una stringa. L'imposta è $5.12" viene visualizzato. `TaxAmount`viene chiamato con un `Decimal` valore per la seconda volta e il messaggio, "prezzo è un numero decimale. L'imposta è $5.12" viene visualizzato.  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti e classi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Shadowing in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Sub (istruzione)](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Nozioni fondamentali sull'ereditarietà](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [Ombreggiature](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)   
 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)   
 [Overload](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
