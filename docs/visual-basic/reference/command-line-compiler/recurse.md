---
title: /recurse | Documenti di Microsoft
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
- /recurse compiler option [Visual Basic]
- -recurse compiler option [Visual Basic]
- recurse compiler option [Visual Basic]
ms.assetid: 84a0b670-33ae-44c4-a46a-b90388809317
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
ms.openlocfilehash: fbf7d67c7f70345e62ddbb03c8626b688b5c593b
ms.lasthandoff: 03/13/2017

---
# <a name="recurse"></a>/recurse
Compila i file di codice sorgente in tutte le directory figlio della directory specificata o della directory del progetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/recurse:[dir\]file  
```  
  
## <a name="arguments"></a>Argomenti  
 `dir`  
 Facoltativo. La directory in cui si desidera eseguire la ricerca. Se non specificato, la ricerca inizia nella directory del progetto.  
  
 `file`  
 Obbligatorio. I file da cercare. Caratteri jolly sono consentiti.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare caratteri jolly in un nome file per compilare tutti i file corrispondenti nella directory del progetto senza utilizzare `/recurse`. Se viene specificato alcun nome di file di output, il compilatore si basa il nome del file di output nel primo file di input elaborato. Si tratta in genere il primo file nell'elenco dei file compilati ordinati alfabeticamente. Per questo motivo, è consigliabile specificare un file di output utilizzando il `/out` (opzione).  
  
> [!NOTE]
>  Il `/recurse` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente consente di compilare tutti [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] file nella directory corrente.  
  
```  
vbc *.vb  
```  
  
 Il codice seguente consente di compilare tutti [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] file di `Test\ABC` directory e delle directory sottostanti, quindi genera `Test.ABC.dll`.  
  
```  
vbc /target:library /out:Test.ABC.dll /recurse:Test\ABC\*.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/out (Visual Basic)](../../../visual-basic/reference/command-line-compiler/out.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
