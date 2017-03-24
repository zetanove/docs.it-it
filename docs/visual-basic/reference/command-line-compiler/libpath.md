---
title: /LIBPATH | Documenti di Microsoft
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
- libpath compiler option [Visual Basic]
- /libpath compiler option [Visual Basic]
- -libpath compiler option [Visual Basic]
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
caps.latest.revision: 16
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
ms.openlocfilehash: cc534e782cff34f0c4882f3da2af973fed69ff80
ms.lasthandoff: 03/13/2017

---
# <a name="libpath"></a>/libpath
Specifica il percorso degli assembly di riferimento.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/libpath:dirList  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`dirList`|Obbligatorio. Elenco delimitato da punto e virgola di directory per il compilatore la ricerca se un assembly di riferimento non viene trovato nella directory di lavoro corrente (la directory da cui si richiama il compilatore) o la directory di sistema di common language runtime. Se il nome della directory contiene uno spazio, racchiudere il nome tra virgolette ("").|  
  
## <a name="remarks"></a>Note  
 Il `/libpath` opzione specifica il percorso degli assembly a cui fa riferimento il [/Reference](../../../visual-basic/reference/command-line-compiler/reference.md) (opzione).  
  
 Il compilatore cerca riferimenti ad assembly che non sono completi nell'ordine seguente:  
  
1.  Directory di lavoro corrente. Si tratta della directory da cui viene richiamato il compilatore.  
  
2.  Common language runtime directory system.  
  
3.  Directory specificate dalle `/libpath`.  
  
4.  Directory specificate dalla variabile di ambiente LIB.  
  
 Il `/libpath` è additivi; specifica che più di una volta aggiunto a eventuali valori precedenti.  
  
 Utilizzare `/reference` per specificare un riferimento all'assembly.  
  
|Per impostare /libpath in Visual Studio ambiente di sviluppo integrato|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic su di **riferimenti** scheda.<br />3.  Fare clic sui **fanno riferimento a percorsi... ** pulsante.<br />4.  Nel **Percorsi riferimento** finestra di dialogo, immettere il nome della directory nel **cartella:** casella.<br />5.  Fare clic su **aggiungere la cartella**.|  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `T2.vb` per creare un file .exe. Il compilatore cerca nella directory di lavoro, nella directory radice dell'unità c e nella directory New Assemblies dell'unità c: i riferimenti all'assembly.  
  
```  
vbc /libpath:c:\;"c:\New Assemblies" /reference:t2.dll t2.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gli assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
