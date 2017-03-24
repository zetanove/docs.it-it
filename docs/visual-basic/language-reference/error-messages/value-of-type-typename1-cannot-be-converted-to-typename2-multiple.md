---
title: "Valore di tipo &quot;&lt;NomeTipo1&gt;&quot;non può essere convertito in&quot;&lt;in NomeTipo2&gt;&quot; (più riferimenti a file) | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30961
- bc30961
dev_langs:
- VB
helpviewer_keywords:
- BC30961
ms.assetid: 8be5aa0d-d236-4ac3-aa9c-5044f9f6562b
caps.latest.revision: 9
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
ms.openlocfilehash: 732291ce9c4b83bb9fc7e83fbbc2a8da9748db59
ms.lasthandoff: 03/13/2017

---
# <a name="value-of-type-39lttypename1gt39-cannot-be-converted-to-39lttypename2gt39-multiple-file-references"></a>Valore di tipo '&lt;NomeTipo1&gt;'non può essere convertito in'&lt;in NomeTipo2&gt;' (più riferimenti a file)
Valore di tipo '\<NomeTipo1 >' non può essere convertito in '\<in NomeTipo2 >'. Mancata corrispondenza del tipo potrebbe essere dovuto all'unione di un riferimento al file '\<filepath1 >' nel progetto '\<projectname1 >' con un riferimento al file '\<filepath2 >' nel progetto '\<projectname2 >'. Se gli assembly sono identici, provare a definire lo stesso percorso per entrambi i riferimenti.  
  
 In una situazione in cui un progetto contiene più di un riferimento al file a un assembly, il compilatore non garantisce che un tipo può essere convertito in un altro.  
  
 Ogni riferimento a file specifica un percorso e il nome del file di output di un progetto (in genere un file DLL). Il compilatore non garantisce che i file di output provengano dalla stessa origine o che rappresentano la stessa versione dello stesso assembly. Pertanto non garantisce che i tipi di riferimenti diversi sono dello stesso tipo, o anche che una può essere convertita a altro.  
  
 Se si conosce che gli assembly di riferimento hanno la stessa identità di assembly, è possibile utilizzare un riferimento a file singolo. L' *identità dell'assembly* include il nome, la versione, la chiave pubblica e le eventuali impostazioni cultura dell'assembly. Queste informazioni identificano l'assembly in modo univoco.  
  
 **ID errore:** BC30961  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Se gli assembly di riferimento hanno la stessa identità di assembly, rimuovere o sostituire uno dei riferimenti di file in modo che sia presente solo un riferimento a file singolo.  
  
-   Se gli assembly di riferimento non hanno la stessa identità dell'assembly, quindi modificare il codice in modo che non effettua il tentativo di convertire un tipo in uno a un tipo in altro.  
  
## <a name="see-also"></a>Vedere anche  
 [Conversioni di tipi in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Gestione dei riferimenti in un progetto](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [Procedura: aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)
