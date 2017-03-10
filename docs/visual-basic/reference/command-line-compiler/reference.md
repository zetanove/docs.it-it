---
title: "/reference (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/reference compiler option [Visual Basic]"
  - "r compiler option [Visual Basic]"
  - "-reference compiler option [Visual Basic]"
  - "/r compiler option [Visual Basic]"
  - "reference compiler option [Visual Basic]"
  - "-r compiler option [Visual Basic]"
ms.assetid: 66bdfced-bbf6-43d1-a554-bc0990315737
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /reference (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica al compilatore di rendere disponibili al progetto in corso di compilazione tutte le informazioni sui tipi presenti nei file specificati.  
  
## Sintassi  
  
```  
/reference:fileList  
' -or-  
/r:fileList  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`fileList`|Obbligatorio.  Elenco delimitato da virgole di nomi di file di assembly.  Se il nome del file contiene uno spazio, racchiuderlo tra virgolette.|  
  
## Note  
 I file importati devono contenere metadati assembly.  Solo i tipi pubblici sono visibili all'esterno dell'assembly.  L'opzione [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) consente di importare metadati da un modulo.  
  
 Se si fa riferimento a un assembly \(assembly A\) che fa a sua volta riferimento a un secondo assembly \(assembly B\), sarà necessario fare riferimento all'assembly B nei seguenti casi:  
  
-   Se un tipo dell'assembly A eredita da un tipo o implementa un'interfaccia dall'assembly B.  
  
-   Se viene richiamato un campo, una proprietà, un evento o un metodo che presenta un tipo restituito o un tipo di parametro proveniente dall'assembly B.  
  
 Per specificare la directory in cui si trovano uno o più riferimenti agli assembly, utilizzare [\/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md).  
  
 Per consentire al compilatore di riconoscere un tipo in un assembly e non in un modulo, è necessario imporre la risoluzione del tipo.  A tale scopo, è ad esempio possibile definire un'istanza del tipo.  Esistono altri modi per consentire al compilatore di risolvere i nomi dei tipi in un assembly.  Se si eredita da un tipo in un assembly, ad esempio, il nome del tipo diventa noto al compilatore.  
  
 Per impostazione predefinita, viene utilizzato il file di risposta Vbc.rsp che fa riferimento agli assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] comunemente utilizzati.  Se non si desidera che il compilatore utilizzi il file Vbc.rsp, specificare `/noconfig`.  
  
 La forma abbreviata di `/reference` è `/r`.  
  
## Esempio  
 Nel codice riportato di seguito viene compilato il file di origine I`nput.vb` e viene fatto riferimento agli assembly di M`etad1.dll` e M`etad2.dll` per generare O`ut.exe`.  
  
```  
vbc /reference:metad1.dll,metad2.dll /out:out.exe input.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)