---
title: "Namespace o il tipo specificato nelle importazioni a livello di progetto&lt;qualifiedelementname&gt;&quot; non contiene alcun membro pubblico o non è possibile trovare | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40057
- bc40057
dev_langs:
- VB
helpviewer_keywords:
- BC40057
ms.assetid: 4ae3506e-2ebe-4ff3-995d-14ac60db5e9f
caps.latest.revision: 10
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
ms.openlocfilehash: 5dae6f92f573a57d0974c860500bc7420f55a94f
ms.lasthandoff: 03/13/2017

---
# <a name="namespace-or-type-specified-in-the-project-level-imports-39ltqualifiedelementnamegt39-doesn39t-contain-any-public-member-or-cannot-be-found"></a>Namespace o il tipo specificato nelle importazioni a livello di progetto&lt;qualifiedelementname&gt;' non contiene alcun membro pubblico o non trovato
Namespace o il tipo specificato nelle importazioni a livello di progetto\<qualifiedelementname >' non contiene alcun membro pubblico o non viene trovato. Assicurarsi che lo spazio dei nomi o il tipo è definito e contiene almeno un membro pubblico. Assicurarsi che il nome di alias non contenga altri alias.  
  
 Una proprietà di importazione di un progetto specifica un elemento contenitore che può essere trovato o non definisce alcun `Public` membri.  
  
 Oggetto *contenente l'elemento* può essere un spazio dei nomi, classe, struttura, modulo, interfaccia o enumerazione. Contiene membri, ad esempio variabili, le procedure o altri elementi che lo contiene.  
  
 Lo scopo dell'importazione è di consentire al codice per accedere ai membri dello spazio dei nomi o tipo senza la necessità di fornire il nome completo. Il progetto potrebbe essere necessario anche aggiungere un riferimento al tipo o dello spazio dei nomi. Per ulteriori informazioni, vedere "Importazione di elementi contenitore" in [riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
 Se il compilatore non trova l'elemento contenitore specificato, non sarà possibile risolvere i riferimenti che lo utilizzano. Se viene trovato l'elemento, ma l'elemento non espone alcun `Public` membri, quindi nessun riferimento può avere esito positivo. In entrambi i casi è significativo per importare l'elemento.  
  
 Utilizzare il **progettazione** per specificare gli elementi da importare. Utilizzare il **spazi dei nomi importati** sezione la **riferimenti** pagina. È possibile ottenere il **Progettazione progetti** facendo doppio clic su di **progetto** icona in **Esplora**.  
  
 **ID errore:** BC40057  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Aprire il **Progettazione progetti** e passare il **riferimento** pagina.  
  
2.  Nel **spazi dei nomi importati** sezione, verificare che l'elemento contenitore è accessibile dal progetto.  
  
3.  Verificare che l'elemento contenitore esponga almeno `Public` membro.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti (pagina), Creazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)   
 [NIB procedura: modificare le proprietà del progetto e le impostazioni di configurazione](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Pubblica](../../../visual-basic/language-reference/modifiers/public.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
