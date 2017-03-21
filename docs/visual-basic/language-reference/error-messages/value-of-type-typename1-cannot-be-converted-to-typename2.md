---
title: "Valore di tipo &quot;&lt;NomeTipo1&gt;&quot;non può essere convertito in&quot;&lt;in NomeTipo2&gt;&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30955
- bc30955
dev_langs:
- VB
helpviewer_keywords:
- BC30955
ms.assetid: 966b61eb-441e-48b0-bedf-ca95384ecb8b
caps.latest.revision: 12
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
ms.openlocfilehash: c973d5e2aa03d423e1dea8053946172655f08490
ms.lasthandoff: 03/13/2017

---
# <a name="value-of-type-39lttypename1gt39-cannot-be-converted-to-39lttypename2gt39"></a>Valore di tipo '&lt;NomeTipo1&gt;'non può essere convertito in'&lt;in NomeTipo2&gt;'
Valore di tipo '\<NomeTipo1 >' non può essere convertito in '\<in NomeTipo2 >'. Mancata corrispondenza del tipo potrebbe essere dovuto all'unione di un riferimento al file con un riferimento progetto all'assembly '\<assemblyname >'. Provare a sostituire il riferimento al file '\<filepath >' nel progetto '\<projectname1 >' con un riferimento al progetto '\<projectname2 >'.  
  
 In una situazione in cui un progetto contiene sia un riferimento al progetto un riferimento al file, il compilatore non garantisce che un tipo può essere convertito in un altro.  
  
 Il pseudo-codice seguente viene illustrata una situazione che può generare l'errore.  
  
 `' ================ Visual Basic project P1 ================`  
  
 `'        P1 makes a PROJECT REFERENCE to project P2`  
  
 `'        and a FILE REFERENCE to project P3.`  
  
 `Public commonObject As P3.commonClass`  
  
 `commonObject = P2.getCommonClass()`  
  
 `' ================ Visual Basic project P2 ================`  
  
 `'        P2 makes a PROJECT REFERENCE to project P3`  
  
 `Public Function getCommonClass() As P3.commonClass`  
  
 `Return New P3.commonClass`  
  
 `End Function`  
  
 `' ================ Visual Basic project P3 ================`  
  
 `Public Class commonClass`  
  
 `End Class`  
  
 Progetto `P1` rende un riferimento di progetto progetto indiretto `P2` al progetto `P3`e anche un riferimento al file diretto `P3`. La dichiarazione di `commonObject` utilizza il riferimento al file `P3`, mentre la chiamata a `P2.getCommonClass` utilizza il riferimento al progetto `P3`.  
  
 Il problema in questa situazione è che il riferimento al file specifica un percorso e il nome del file di output di `P3` (in genere P3), mentre i riferimenti al progetto identificano il progetto di origine (`P3`) in base al nome di progetto. Per questo motivo, il compilatore non garantisce che il tipo `P3.commonClass` proviene dallo stesso codice di origine tramite i due diversi riferimenti.  
  
 Questa situazione si verifica in genere quando i riferimenti di progetto e i riferimenti ai file vengono combinati. Nell'illustrazione precedente, il problema non si verificherà se `P1` effettuato un riferimento diretto `P3` anziché un riferimento al file.  
  
 **ID errore:** BC30955  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Modificare il riferimento al file a un riferimento al progetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Conversioni di tipi in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Gestione dei riferimenti in un progetto](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [Procedura: aggiungere o rimuovere riferimenti utilizzando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)
