---
title: '&lt;messaggio&gt; questo errore potrebbe inoltre essere dovuto all&quot;unione di un riferimento al file con un riferimento progetto all&quot;assembly &quot;&lt;assemblyname&gt;&quot; | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30971
- vbc30971
dev_langs:
- VB
helpviewer_keywords:
- BC30971
ms.assetid: 75d2e8b5-2fdc-4623-8b32-cba805dab7db
caps.latest.revision: 10
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
ms.openlocfilehash: a1806fd078fc05d966c718841e5b78c1323a43c2
ms.lasthandoff: 03/13/2017

---
# <a name="ltmessagegt-this-error-could-also-be-due-to-mixing-a-file-reference-with-a-project-reference-to-assembly-39ltassemblynamegt39"></a>&lt;messaggio&gt; questo errore potrebbe inoltre essere dovuto all'unione di un riferimento al file con un riferimento progetto all'assembly '&lt;assemblyname&gt;'
\<messaggio > questo errore potrebbe inoltre essere dovuto all'unione di un riferimento al file con un riferimento progetto all'assembly '\<assemblyname >. In questo caso, provare a sostituire il riferimento al file '\<assemblyfilename >' nel progetto '\<projectname1 >' con un riferimento al progetto '\<projectname2 >'.  
  
 Il codice del progetto accede a un membro di un altro progetto, ma non consente la configurazione della soluzione di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore per risolvere il riferimento.  
  
 Accedere a un tipo definito in un altro assembly, il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore deve avere un riferimento a tale assembly. Deve trattarsi di un riferimento unico, non ambiguo, che non generi riferimenti circolari tra i progetti.  
  
 **ID errore:** BC30971  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Determinare quale progetto produce l'assembly migliore per il progetto a cui fare riferimento. Per questa decisione si potrebbero usare criteri quali la facilità di accesso al file e la frequenza di aggiornamenti.  
  
2.  Nelle proprietà del progetto aggiungere un riferimento al progetto contenente l'assembly che definisce il tipo in uso.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione dei riferimenti in un progetto](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [Riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [NIB Procedura: Aggiungere o rimuovere riferimenti usando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [NIB procedura: modificare le proprietà del progetto e le impostazioni di configurazione](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Risoluzione dei problemi relativi ai riferimenti interrotti](https://docs.microsoft.com/visualstudio/ide/troubleshooting-broken-references)
