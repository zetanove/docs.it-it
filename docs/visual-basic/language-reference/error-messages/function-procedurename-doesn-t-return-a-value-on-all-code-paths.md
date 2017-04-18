---
title: Funzione &quot;&lt;NomeProcedura&gt;&quot; non restituisce un valore in tutti i percorsi di codice | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc42105
- vbc42105
dev_langs:
- VB
helpviewer_keywords:
- BC42105
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
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
ms.openlocfilehash: 288fdf7c4845b20283681d9eb3504ac314f1ddd2
ms.lasthandoff: 03/13/2017

---
# <a name="function-39ltprocedurenamegt39-doesn39t-return-a-value-on-all-code-paths"></a>Funzione '&lt;NomeProcedura&gt;' non restituisce un valore in tutti i percorsi di codice
Funzione '\<NomeProcedura >' non restituisce un valore in tutti i percorsi di codice. Manca un'istruzione 'Return'?  
  
 Oggetto `Function` procedura ha almeno un percorso possibile tramite il codice che non restituisce un valore.  
  
 È possibile restituire un valore da un `Function` procedura in uno dei modi seguenti:  
  
-   Includere il valore in un [istruzione Return](../../../visual-basic/language-reference/statements/return-statement.md).  
  
-   Assegnare il valore per il `Function` procedure un nome e quindi eseguire un `Exit Function` istruzione.  
  
-   Assegnare il valore per il `Function` procedure un nome e quindi eseguire il `End Function` istruzione.  
  
 Se il controllo passa al `Exit Function` o `End Function` e non è stato assegnato alcun valore per il nome della procedura, la procedura restituisce il valore predefinito del tipo di dati restituito. Per ulteriori informazioni, vedere "Comportamento" in [istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md).  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42105  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Controllare la logica del flusso di controllo e assicurarsi di assegnare un valore prima di ogni istruzione che provoca una restituzione.  
  
     È più semplice garantire che ogni restituito dalla routine restituisce un valore se si utilizza sempre il `Return` istruzione. In questo caso, l'ultima istruzione prima `End Function` deve essere un `Return` istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Routine di funzione](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Pagina Compilazione, Creazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
