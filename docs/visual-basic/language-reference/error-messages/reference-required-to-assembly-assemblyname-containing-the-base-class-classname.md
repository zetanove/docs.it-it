---
title: Necessario riferimento all&quot;assembly &quot;&lt;assemblyname&gt;&quot;contenente la classe base&quot;&lt;classname&gt;&quot; | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30007
- vbc30007
dev_langs:
- VB
helpviewer_keywords:
- BC30007
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
caps.latest.revision: 9
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
ms.openlocfilehash: 2692478864007c787eb19367109e6ce01882ffb1
ms.lasthandoff: 03/13/2017

---
# <a name="reference-required-to-assembly-39ltassemblynamegt39-containing-the-base-class-39ltclassnamegt39"></a>Necessario riferimento all'assembly '&lt;assemblyname&gt;'contenente la classe base'&lt;classname&gt;'
Necessario riferimento all'assembly '\<assemblyname >' contenente la classe base\<classname >'. Aggiungerne uno al progetto.  
  
 La classe è definita in una libreria a collegamento dinamico (DLL) o in un assembly a cui non si fa direttamente riferimento nel progetto. Il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore richiede un riferimento per evitare ambiguità nel caso in cui la classe è definita in più di un file DLL o assembly.  
  
 **ID errore:** BC30007  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Includere il nome della DLL o dell'assembly senza riferimento nei riferimenti del progetto.  
  
## <a name="see-also"></a>Vedere anche  
 [NIB Procedura: Aggiungere o rimuovere riferimenti usando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [Gestione dei riferimenti in un progetto](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [Risoluzione dei problemi relativi ai riferimenti interrotti](https://docs.microsoft.com/visualstudio/ide/troubleshooting-broken-references)
