---
title: /win32resource | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /win32resource
- win32resource
dev_langs:
- VB
helpviewer_keywords:
- /win32resource compiler option [Visual Basic]
- -win32resource compiler option [Visual Basic]
- win32resource compiler option [Visual Basic]
ms.assetid: e226946d-19ce-4cc9-91f5-aed24f77aa2b
caps.latest.revision: 13
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
ms.openlocfilehash: 37902590d5a05d7fdb2a521f3c3de2ad88c2c502
ms.lasthandoff: 03/13/2017

---
# <a name="win32resource"></a>/win32resource
Inserisce un file di risorse Win32 nel file di output.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/win32resource:filename  
```  
  
## <a name="arguments"></a>Argomenti  
 `filename`  
 Il nome del file di risorse da aggiungere al file di output. Racchiudere il nome del file tra virgolette ("") se contiene uno spazio.  
  
## <a name="remarks"></a>Note  
 È possibile creare un file di risorse Win32 con il compilatore di risorse (RC) di Microsoft Windows.  
  
 Una risorsa Win32 può contenere versione o informazioni bitmap (icona) che consente di identificare l'applicazione in **Esplora File**. Se non si specifica `/win32resource`, il compilatore genera informazioni di versione basate sulla versione dell'assembly. Il `/win32resource` e `/win32icon` opzioni si escludono a vicenda.  
  
 Vedere [/linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md) per fare riferimento a un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] file di risorse, o [/resource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md) per collegare un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] file di risorse.  
  
> [!NOTE]
>  Il `/win32resource` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `In.vb` e allegare un file di risorse Win32 `Rf.res`:  
  
```  
vbc /win32resource:rf.res in.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
