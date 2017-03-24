---
title: Routine Property (Visual Basic) | Documenti di Microsoft
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
- Set statement, Property procedures
- Visual Basic code, procedures
- return values, Property procedures
- syntax, Property procedures
- procedures, property
- Visual Basic code, properties
- procedures, calling
- properties [Visual Basic], custom
- property procedures
- Get statement, property procedures
ms.assetid: 46a98379-e1a2-45dd-a48c-b51213f5ab07
caps.latest.revision: 22
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: f21d4c7d9bd8f14bbe7284bc08399e7ba6b466c3
ms.lasthandoff: 03/13/2017

---
# <a name="property-procedures-visual-basic"></a>Routine Property (Visual Basic)
Una routine di proprietà è una serie di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] istruzioni che modificano una proprietà personalizzata di un modulo, classe o struttura. Routine Property sono anche noti come *accesso della proprietà*.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce le routine della proprietà seguente:  
  
-   Oggetto `Get` procedura restituisce il valore di una proprietà. Viene chiamato quando si accede alla proprietà in un'espressione.  
  
-   Oggetto `Set` routine imposta una proprietà su un valore, incluso un riferimento all'oggetto. Viene chiamato quando si assegna un valore alla proprietà.  
  
 Le routine di proprietà viene in genere definito in coppie, mediante il `Get` e `Set` istruzioni, ma è possibile definire una routine singolarmente se la proprietà è di sola lettura ([istruzione Get](../../../../visual-basic/language-reference/statements/get-statement.md)) o di sola scrittura ([istruzione Set](../../../../visual-basic/language-reference/statements/set-statement.md)).  
  
 È possibile omettere il `Get` e `Set` procedura quando si utilizza una proprietà implementata automaticamente. Per ulteriori informazioni, vedere [proprietà implementate automaticamente](./auto-implemented-properties.md).  
  
 È possibile definire le proprietà nelle classi, strutture e moduli. Le proprietà sono `Public` per impostazione predefinita, il che significa che è possibile chiamarle da qualsiasi punto dell'applicazione che possono accedere al contenitore della proprietà.  
  
 Per un confronto tra proprietà e variabili, vedere [le differenze tra proprietà e variabili in Visual Basic](./differences-between-properties-and-variables.md).  
  
## <a name="declaration-syntax"></a>Sintassi di dichiarazione  
 Una proprietà è definita da un blocco di codice incluso all'interno di [istruzione Property](../../../../visual-basic/language-reference/statements/property-statement.md) e `End Property` istruzione. All'interno del blocco, ogni routine di proprietà viene visualizzata come un blocco interno racchiuso tra un'istruzione di dichiarazione (`Get` o `Set`) e il corrispondente `End` dichiarazione.  
  
 La sintassi per dichiarare una proprietà e le relative procedure è come segue:  
  
```  
[Default] [Modifiers] Property PropertyName[(ParameterList)] [As DataType]  
    [AccessLevel] Get  
        ' Statements of the Get procedure.  
        ' The following statement returns an expression as the property's value.  
        Return Expression  
    End Get  
    [AccessLevel] Set[(ByVal NewValue As DataType)]  
        ' Statements of the Set procedure.  
        ' The following statement assigns newvalue as the property's value.  
        LValue = NewValue  
    End Set  
End Property  
- or -  
[Default] [Modifiers] Property PropertyName [(ParameterList)] [As DataType]  
```  
  
 Il `Modifiers` possibile specificare il livello di accesso e informazioni su overload, override, condivisione e shadowing, anche se la proprietà è di sola lettura o in sola lettura. Il `AccessLevel` sul `Get` o `Set` procedura può essere qualsiasi livello più restrittivo rispetto al livello di accesso specificato per la proprietà stessa. Per ulteriori informazioni, vedere [proprietà istruzione](../../../../visual-basic/language-reference/statements/property-statement.md).  
  
### <a name="data-type"></a>Tipo di dati  
 Tipo di dati della proprietà e il livello di accesso dell'entità sono definiti nel `Property` istruzione, non nelle routine della proprietà. Una proprietà può avere solo un tipo di dati. Ad esempio, è possibile definire una proprietà per archiviare un `Decimal` valore ma recuperare un `Double` valore.  
  
### <a name="access-level"></a>Livello di accesso  
 Tuttavia, è possibile definire un livello di accesso dell'entità per una proprietà e limitare ulteriormente il livello di accesso in una delle routine della proprietà. Ad esempio, è possibile definire un `Public` proprietà e quindi definire un `Private Set` procedura. Il `Get` procedura rimane `Public`. È possibile modificare il livello di accesso in sola delle routine della proprietà, e sarà possibile solo renderla più restrittivo rispetto al livello di accesso dell'entità. Per ulteriori informazioni, vedere [procedura: dichiarare una proprietà con livelli di accesso misti](./how-to-declare-a-property-with-mixed-access-levels.md).  
  
## <a name="parameter-declaration"></a>Dichiarazione di parametro  
 Ciascun parametro viene dichiarato esattamente come avviene per [Sub (routine)](./sub-procedures.md), ad eccezione del fatto che il meccanismo di passaggio deve essere `ByVal`.  
  
 La sintassi per ogni parametro nell'elenco dei parametri è come segue:  
  
 `[Optional] ByVal [ParamArray] parametername As datatype`  
  
 Se il parametro è facoltativo, è necessario fornire anche un valore predefinito come parte della relativa dichiarazione. La sintassi per specificare un valore predefinito è come segue:  
  
 `Optional ByVal parametername As datatype = defaultvalue`  
  
## <a name="property-value"></a>Valore proprietà  
 In un `Get` procedura, il valore restituito viene fornito all'espressione chiamante come valore della proprietà.  
  
 In un `Set` procedura, il nuovo valore della proprietà viene passato al parametro di `Set` istruzione. Se si dichiara in modo esplicito un parametro, è necessario dichiararla con lo stesso tipo di dati della proprietà. Se si dichiara un parametro, il compilatore utilizza il parametro implicito `Value` per rappresentare il nuovo valore da assegnare alla proprietà.  
  
## <a name="calling-syntax"></a>Sintassi di chiamata  
 Richiamare una routine di proprietà in modo implicito facendo riferimento alla proprietà. Si utilizza il nome della proprietà esattamente come si utilizzerebbe il nome di una variabile, ad eccezione del fatto che è necessario fornire valori per tutti gli argomenti che non sono facoltativi e racchiudere l'elenco di argomenti racchiuso tra parentesi. Se viene fornito alcun argomento, è possibile omettere le parentesi.  
  
 La sintassi per una chiamata implicita a un `Set` è la seguente procedura:  
  
 `propertyname[(argumentlist)] = expression`  
  
 La sintassi per una chiamata implicita a un `Get` è la seguente procedura:  
  
 `lvalue = propertyname[(argumentlist)]`  
  
 `Do While (propertyname[(argumentlist)] > expression)`  
  
### <a name="illustration-of-declaration-and-call"></a>Illustrazione di dichiarazione e chiamata  
 La seguente proprietà memorizza un nome completo come due nomi costitutivi, il nome e il cognome. Quando il codice chiamante legge `fullName`, `Get` procedura combina le due parti costitutive e restituisce il nome completo. Quando il codice chiamante assegna un nuovo nome completo, il `Set` procedura tenta di suddividerla in due parti costitutive. Se non viene trovato uno spazio, lo archivia tutti gli elementi come il nome.  
  
 [!code-vb[VbVbcnProcedures n.&8;](./codesnippet/VisualBasic/property-procedures_1.vb)]  
  
 L'esempio seguente mostra le chiamate tipiche alle routine delle proprietà `fullName`.  
  
 [!code-vb[9 VbVbcnProcedures](./codesnippet/VisualBasic/property-procedures_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Routine di funzione](./function-procedures.md)   
 [Routine di operatore](./operator-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Differenze tra proprietà e variabili in Visual Basic](./differences-between-properties-and-variables.md)   
 [Procedura: creare una proprietà](./how-to-create-a-property.md)   
 [Procedura: chiamare una routine di proprietà](./how-to-call-a-property-procedure.md)   
 [Procedura: dichiarare e chiamare una proprietà predefinita in Visual Basic](./how-to-declare-and-call-a-default-property.md)   
 [Procedura: inserire un valore in una proprietà](./how-to-put-a-value-in-a-property.md)   
 [Procedura: Ottenere un valore da una proprietà](./how-to-get-a-value-from-a-property.md)
