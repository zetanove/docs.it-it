---
title: Istruzione Delegate | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Delegate
dev_langs:
- VB
helpviewer_keywords:
- delegate keyword
- Delegate statement
ms.assetid: f799c518-0817-40cc-ad0b-4da846fdba57
caps.latest.revision: 27
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 9ac9e28c82f8a6b5a9c1398961d831c956a649e0
ms.lasthandoff: 03/13/2017

---
# <a name="delegate-statement"></a>Istruzione Delegate
Utilizzata per dichiarare un delegato. Un delegato è un tipo di riferimento che fa riferimento a un `Shared` metodo di un tipo o a un metodo di istanza di un oggetto. Per creare un'istanza della classe delegata, è possibile utilizzare qualsiasi routine con parametri e tipi restituiti corrispondenti. La procedura può quindi successivamente richiamata tramite l'istanza del delegato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shadows ] Delegate [ Sub | Function ] name [( Of typeparamlist )] [([ parameterlist ])] [ As type ]  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`attrlist`|Facoltativo. Elenco di attributi che si applicano a questo delegato. Gli attributi sono separati da una virgola. È necessario racchiudere il [elenco attributi](../../../visual-basic/language-reference/statements/attribute-list.md) parentesi angolari ("`<`"e"`>`").|  
|`accessmodifier`|Facoltativo. Specifica il codice può accedere al delegato. Può essere uno dei seguenti:<br /><br /> -   [Pubblica](../../../visual-basic/language-reference/modifiers/public.md). Qualsiasi codice che può accedere all'elemento che dichiara il delegato può accedervi.<br />-   [Protetto](../../../visual-basic/language-reference/modifiers/protected.md). Solo il codice incluso nella classe del delegato o una classe derivata può accedervi.<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md). Solo codice all'interno dello stesso assembly può accedere al delegato.<br />-   [Privato](../../../visual-basic/language-reference/modifiers/private.md). Può accedere solo codice all'interno dell'elemento che dichiara il delegato.<br /><br /> È possibile specificare `Protected Friend` per abilitare l'accesso dal codice all'interno dello stesso assembly, una classe derivata o nella classe del delegato.|  
|`Shadows`|Facoltativo. Indica che il delegato ridichiara e nasconde un elemento di programmazione omonimo o un set di elementi in overload, una classe di base. È possibile nascondere qualsiasi tipo di elemento dichiarato con qualsiasi altro tipo.<br /><br /> Un elemento nascosto non è disponibile all'interno della classe derivata che lo nasconde, a meno che l'elemento di shadowing sia inaccessibile. Ad esempio, se un `Private` elemento nasconde un elemento di classe di base, il codice che non dispone dell'autorizzazione di accesso di `Private` elemento accede invece all'elemento della classe base.|  
|`Sub`|Parametro facoltativo, ma uno `Sub` o `Function` deve essere visualizzato. Dichiarare la routine come delegato `Sub` routine che restituisce un valore.|  
|`Function`|Parametro facoltativo, ma uno `Sub` o `Function` deve essere visualizzato. Dichiarare la routine come delegato `Function` procedure che restituisce un valore.|  
|`name`|Obbligatorio. Nome del tipo di delegato. segue le convenzioni di denominazione standard variabile.|  
|`typeparamlist`|Facoltativo. Elenco di parametri di tipo per questo delegato. Più parametri di tipo sono separati da virgole. Facoltativamente, ogni parametro di tipo può essere dichiarato variante mediante `In` e `Out` modificatori generici. È necessario racchiudere il [tipo elenco](../../../visual-basic/language-reference/statements/type-list.md) tra parentesi e introdurre con il `Of` (parola chiave).|  
|`parameterlist`|Facoltativo. Elenco di parametri passati alla routine quando viene chiamato. È necessario racchiudere il [elenco parametri](../../../visual-basic/language-reference/statements/parameter-list.md) tra parentesi.|  
|`type`|Necessario se si specifica un `Function` procedura. Tipo di dati del valore restituito.|  
  
## <a name="remarks"></a>Note  
 Il `Delegate` istruzione definisce i parametri e tipi restituiti di una classe delegata. Per creare un'istanza della classe delegata, è possibile utilizzare qualsiasi routine con parametri e tipi restituiti corrispondenti. La procedura può quindi successivamente essere richiamata tramite l'istanza del delegato, mediante la chiamata del delegato `Invoke` metodo.  
  
 I delegati possono essere dichiarati di spazio dei nomi, modulo, classe o struttura, ma non all'interno di una routine.  
  
 Ogni classe delegata definisce un costruttore a cui viene passata la specifica di un metodo dell'oggetto. Un argomento a un costruttore di delegato deve essere un riferimento a un metodo o un'espressione lambda.  
  
 Per specificare un riferimento a un metodo, utilizzare la sintassi seguente:  
  
 `AddressOf` [`expression`.]`methodname`  
  
 Il tipo in fase di compilazione di `expression` deve essere il nome di una classe o un'interfaccia che contiene un metodo con il nome specificato, la cui firma corrisponde alla firma della classe delegata. Il `methodname` può essere un metodo condiviso o un metodo di istanza. Il `methodname` non è facoltativo, anche se si crea un delegato per il metodo predefinito della classe.  
  
 Per specificare un'espressione lambda, utilizzare la sintassi seguente:  
  
 `Function`([`parm` As `type`, `parm2` As `type2`, ...])`expression`  
  
 La firma della funzione deve corrispondere a quello del tipo di delegato. Per altre informazioni sulle espressioni lambda, vedere [Espressioni lambda in C++](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 Per ulteriori informazioni sui delegati, vedere [delegati](../../../visual-basic/programming-guide/language-features/delegates/index.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `Delegate` istruzione per dichiarare un delegato per operazioni su due numeri e restituire un numero. Il `DelegateTest` metodo accetta un'istanza di questo tipo di delegato e lo utilizza per operare su coppie di numeri.  
  
 [!code-vb[VbVbalrDelegates&#14;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegate-statement_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [AddressOf (operatore)](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)   
 [Delegati](../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Procedura: utilizzare una classe generica](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Covarianza e controvarianza](http://msdn.microsoft.com/library/a58cc086-276f-4f91-a366-85b7f95f38b8)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [In uscita](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)
