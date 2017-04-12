---
title: /sdkpath | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- sdkpath
- /sdkpath
dev_langs:
- VB
helpviewer_keywords:
- -sdkpath compiler option [Visual Basic]
- /sdkpath compiler option [Visual Basic]
- sdkpath compiler option [Visual Basic]
ms.assetid: fec8a3f1-b791-4a37-8af7-344859f8212d
caps.latest.revision: 15
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
ms.openlocfilehash: 3584daa49bca699f022a1afd34e3d450b8442060
ms.lasthandoff: 03/13/2017

---
# <a name="sdkpath"></a>/sdkpath
Specifica il percorso dei file Mscorlib.dll e Microsoft.VisualBasic.dll.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/sdkpath:path  
```  
  
## <a name="arguments"></a>Argomenti  
 `path`  
 La directory che contiene le versioni di mscorlib. dll e Microsoft.VisualBasic.dll da utilizzare per la compilazione. Questo percorso non viene verificato finché viene caricato. Racchiudere il nome della directory tra virgolette ("") se contiene uno spazio.  
  
## <a name="remarks"></a>Note  
 Questa opzione indica la [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore di caricare i file mscorlib. dll e Microsoft.VisualBasic.dll da un percorso non predefinito. Il `/sdkpath` opzione è stata progettata per essere utilizzato con [/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md). Il [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] vengono utilizzate versioni diverse di queste librerie di supporto per evitare l'utilizzo di tipi e le funzionalità di linguaggio non disponibili nei dispositivi.  
  
> [!NOTE]
>  Il `/sdkpath` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando. Il `/sdkpath` opzione viene impostata quando un [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] dispositivo progetto viene caricato.  
  
 È possibile specificare che il compilatore esegue la compilazione senza un riferimento alla libreria di Runtime di Visual Basic utilizzando il `/vbruntime` l'opzione del compilatore. Per ulteriori informazioni, vedere [/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md).  
  
## <a name="example"></a>Esempio  
 Il codice seguente Compila `Myfile.vb` con il [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)], con le versioni di mscorlib. dll e Microsoft.VisualBasic.dll trovato nella directory di installazione predefinita di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)] nell'unità C. In genere, si utilizzerà la versione più recente di [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)].  
  
```  
vbc /netcf /sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)   
 [/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)
