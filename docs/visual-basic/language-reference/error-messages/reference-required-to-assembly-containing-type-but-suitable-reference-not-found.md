---
title: "Necessario riferimento all&quot;assembly &quot;&lt;assemblyidentity&gt;&quot;contenente il tipo&quot;&lt;typename&gt;&quot;, ma non è stato possibile trovare un riferimento a causa dell&quot;ambiguità tra i progetti&lt;projectname1&gt;&quot;e&quot;&lt;projectname2&gt;&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30969
- vbc30969
dev_langs:
- VB
helpviewer_keywords:
- BC30969
ms.assetid: 1b29dbc5-8268-45fe-bfc2-b2070a5c845c
caps.latest.revision: 11
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
ms.openlocfilehash: 38f016b9d0de053c9a95a6d4a4d810d55af903e9
ms.lasthandoff: 03/13/2017

---
# <a name="reference-required-to-assembly-39ltassemblyidentitygt39-containing-type-39lttypenamegt39-but-a-suitable-reference-could-not-be-found-due-to-ambiguity-between-projects-39ltprojectname1gt39-and-39ltprojectname2gt39"></a>Necessario riferimento all'assembly '&lt;assemblyidentity&gt;'contenente il tipo'&lt;typename&gt;', ma non è stato possibile trovare un riferimento a causa dell'ambiguità tra i progetti&lt;projectname1&gt;'e'&lt;projectname2&gt;'
In un'espressione viene usato un tipo, ad esempio una classe, una struttura, un'interfaccia, un'enumerazione o un delegato, definito all'esterno del progetto. Tuttavia, sono presenti riferimenti di progetto a più assembly che definiscono quel tipo.  
  
 I progetti citati generano assembly con lo stesso nome. Pertanto, il compilatore non può determinare l'assembly da usare per il tipo a cui si accede.  
  
 Accedere a un tipo definito in un altro assembly, il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore deve avere un riferimento a tale assembly. Deve trattarsi di un riferimento unico, non ambiguo, che non generi riferimenti circolari tra i progetti.  
  
 **ID errore:** BC30969  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Determinare quale progetto produce l'assembly migliore per il progetto a cui fare riferimento. Per questa decisione si potrebbero usare criteri quali la facilità di accesso al file e la frequenza di aggiornamenti.  
  
2.  Nelle proprietà del progetto aggiungere un riferimento al file contenente l'assembly che definisce il tipo in uso.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione dei riferimenti in un progetto](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [Riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [NIB Procedura: Aggiungere o rimuovere riferimenti usando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [NIB procedura: modificare le proprietà del progetto e le impostazioni di configurazione](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Risoluzione dei problemi relativi ai riferimenti interrotti](https://docs.microsoft.com/visualstudio/ide/troubleshooting-broken-references)
