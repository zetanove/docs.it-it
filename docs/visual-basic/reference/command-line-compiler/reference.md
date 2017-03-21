---
title: /Reference (Visual Basic) | Documenti di Microsoft
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
- /reference compiler option [Visual Basic]
- r compiler option [Visual Basic]
- -reference compiler option [Visual Basic]
- /r compiler option [Visual Basic]
- reference compiler option [Visual Basic]
- -r compiler option [Visual Basic]
ms.assetid: 66bdfced-bbf6-43d1-a554-bc0990315737
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
ms.openlocfilehash: 12344dba82131d6be2c32127de287a6e9e3efa39
ms.lasthandoff: 03/13/2017

---
# <a name="reference-visual-basic"></a>/reference (Visual Basic)
Indica al compilatore di rendere disponibili per il progetto in corso di compilazione informazioni sui tipi negli assembly specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/reference:fileList  
' -or-  
/r:fileList  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`fileList`|Obbligatorio. Elenco delimitato da virgole di nomi di file di assembly. Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette.|  
  
## <a name="remarks"></a>Note  
 I file importati devono contenere i metadati dell'assembly. Solo i tipi pubblici sono visibili all'esterno dell'assembly. Il [/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) opzione Importa i metadati da un modulo.  
  
 Se si fa riferimento a un assembly (Assembly a) che a sua volta fa riferimento a un altro assembly (Assembly B), è necessario fare riferimento all'Assembly B se:  
  
-   Un tipo da Assembly A eredita da un tipo o implementa un'interfaccia dell'Assembly B.  
  
-   Un campo, proprietà, evento o metodo che presenta un tipo di parametro o tipo restituito dall'Assembly B viene richiamato.  
  
 Utilizzare [/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md) per specificare la directory in cui si trova una o più riferimenti agli assembly.  
  
 Per il compilatore di riconoscere un tipo in un assembly (non un modulo), è necessario imporre la risoluzione del tipo. Un esempio di come è possibile farlo consiste nel definire un'istanza del tipo. Esistono altri modi risolvere i nomi dei tipi in un assembly per il compilatore. Ad esempio, se si eredita da un tipo in un assembly, il nome del tipo quindi diventa noto al compilatore.  
  
 Il file di risposta Vbc. rsp, i riferimenti utilizzati comunemente [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] assembly, viene utilizzato per impostazione predefinita. Utilizzare `/noconfig` se non si desidera al compilatore di utilizzare vbc. rsp.  
  
 La versione abbreviata di `/reference` è `/r`.  
  
## <a name="example"></a>Esempio  
 Il seguente codice consente di compilare file di origine è`nput.vb` e fare riferimento agli assembly da M`etad1.dll` e M`etad2.dll` per generare O`ut.exe`.  
  
```  
vbc /reference:metad1.dll,metad2.dll /out:out.exe input.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Pubblica](../../../visual-basic/language-reference/modifiers/public.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
