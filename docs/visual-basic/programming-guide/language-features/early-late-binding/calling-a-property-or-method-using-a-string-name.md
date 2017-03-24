---
title: "Chiamata di una proprietà o metodo utilizzando un nome di stringa (Visual Basic) | Documenti di Microsoft"
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
- passing operators
- strings [Visual Basic], passing new operators as
- objects [Visual Basic], setting properties
- setting properties, object properties at run time
- method calls, strings
- methods [Visual Basic], calling with string names
- calling methods, string names
- properties [Visual Basic], setting at run time
- CallByName function
ms.assetid: 79a7b8b4-b8c7-4ad8-aca8-12a9a2b32f03
caps.latest.revision: 17
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
ms.openlocfilehash: 87af2816ba42e2901c53bec5e9c19f34c676ed5c
ms.lasthandoff: 03/13/2017

---
# <a name="calling-a-property-or-method-using-a-string-name-visual-basic"></a>Chiamata di una proprietà o di un metodo mediante un nome di stringa (Visual Basic)
Nella maggior parte dei casi, è possibile individuare le proprietà e metodi di un oggetto in fase di progettazione e scrivere codice per gestirli. Tuttavia, in alcuni casi potrebbe non sapere sulle proprietà e metodi di un oggetto in anticipo o si potrebbe volere la flessibilità di un utente finale di specificare le proprietà o eseguire i metodi in fase di esecuzione.  
  
## <a name="callbyname-function"></a>CallByName (funzione)  
 Si consideri, ad esempio, un'applicazione client che valuta espressioni immesse dall'utente mediante il passaggio di un operatore a un componente COM. Si supponga che si siano aggiungendo nuove funzioni costantemente il componente che richiedono nuovi operatori. Quando si utilizzano tecniche di accesso agli oggetti standard, è necessario ricompilare e ridistribuire l'applicazione client prima di utilizzare i nuovi operatori. Per evitare questo problema, è possibile utilizzare il `CallByName` funzione per passare i nuovi operatori come stringhe, senza modificare l'applicazione.  
  
 Il `CallByName` funzione consente di utilizzare una stringa per specificare una proprietà o metodo in fase di esecuzione. La firma per il `CallByName` funzione è simile al seguente:  
  
 *Result* = `CallByName`(*Object*, *ProcedureName*, *CallType*, *Arguments*())  
  
 Il primo argomento, *oggetto*, accetta il nome dell'oggetto di cui si desidera agire. Il *NomeProcedura* argomento accetta una stringa che contiene il nome del metodo o proprietà della routine da richiamare. Il *CallType* argomento accetta una costante che rappresenta il tipo di routine da richiamare: un metodo (`Microsoft.VisualBasic.CallType.Method`), una proprietà di lettura (`Microsoft.VisualBasic.CallType.Get`), o un insieme di proprietà (`Microsoft.VisualBasic.CallType.Set`). Il *argomenti* argomento è facoltativo, prende una matrice di tipo `Object` che contiene gli argomenti per la procedura.  
  
 È possibile utilizzare `CallByName` con le classi nella soluzione corrente, ma che vengono spesso utilizzati per accedere agli oggetti COM o oggetti da [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] assembly.  
  
 Si supponga di aggiunta un riferimento a un assembly che contiene una classe denominata `MathClass`, che dispone di una nuova funzione denominata `SquareRoot`, come illustrato nel codice seguente:  
  
 [!code-vb[VbVbalrOOP&#53;](../../../../visual-basic/misc/codesnippet/VisualBasic/calling-a-property-or-method-using-a-string-name_1.vb)]  
  
 L'applicazione è possibile utilizzare le caselle di testo al controllo verrà chiamato il metodo e i relativi argomenti. Ad esempio, se `TextBox1` contiene l'espressione da valutare e `TextBox2` viene utilizzata per immettere il nome della funzione, è possibile utilizzare il codice seguente per richiamare il `SquareRoot` funzione nell'espressione nel `TextBox1`:  
  
 [!code-vb[&#54; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/calling-a-property-or-method-using-a-string-name_2.vb)]  
  
 Se si immette "64" in `TextBox1`, "SquareRoot" in `TextBox2`e quindi chiamare il `CallMath` procedura, la radice quadrata del numero in `TextBox1` viene valutato. Il codice di esempio richiama il `SquareRoot` funzione (che accetta una stringa che contiene l'espressione da valutare come un argomento obbligatorio) e restituisce "8" `TextBox1` (la radice quadrata di 64). Naturalmente, se l'utente immette una stringa non valida in `TextBox2`, se la stringa contiene il nome di una proprietà anziché un metodo oppure se il metodo richiede un ulteriore argomento, si verifica un errore di run-time. È necessario aggiungere codice di gestione degli errori affidabile quando si utilizza `CallByName` per prevenire questo o altri errori.  
  
> [!NOTE]
>  Mentre il `CallByName` funzione potrebbe essere utile in alcuni casi, è necessario valutare dell'utilità, anche le implicazioni sulle prestazioni, utilizzando `CallByName` per richiamare una routine risulta leggermente più lento rispetto a una chiamata ad associazione tardiva. Se si richiamano una funzione che viene poi chiamata più volte, ad esempio all'interno di un ciclo, `CallByName` può avere un impatto notevole sulle prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.CallByName%2A></xref:Microsoft.VisualBasic.Interaction.CallByName%2A>   
 [Determinazione del tipo di un oggetto](../../../../visual-basic/programming-guide/language-features/early-late-binding/determining-object-type.md)
