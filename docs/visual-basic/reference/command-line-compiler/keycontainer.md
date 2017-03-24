---
title: /keycontainer | Documenti di Microsoft
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
- -keycontainer compiler option [Visual Basic]
- keycontainer compiler option [Visual Basic]
- /keycontainer compiler option [Visual Basic]
ms.assetid: 6a9bc861-1752-4db1-9f64-b5252f0482cc
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
ms.openlocfilehash: 68fa09edce5c0c9af143197f9379d5a46afab52e
ms.lasthandoff: 03/13/2017

---
# <a name="keycontainer"></a>/keycontainer
Specifica il nome di un contenitore di chiavi per una coppia di chiavi allo scopo di assegnare a un assembly un nome sicuro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/keycontainer:container  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`container`|Obbligatorio. File contenitore che contiene la chiave. Racchiudere il nome del file tra virgolette ("") se il nome contiene uno spazio.|  
  
## <a name="remarks"></a>Note  
 Il compilatore crea il componente condivisibile inserendo una chiave pubblica nel manifesto dell'assembly e firmando l'assembly finale con la chiave privata. Per generare un file di chiave, digitare `sn -k``file` nella riga di comando. Il `-i` opzione installa la coppia di chiavi in un contenitore. Per altre informazioni, vedere [Sn.exe (Strong Name Tool)](https://msdn.microsoft.com/library/k5b5tt23).  
  
 Se si compila con `/target:module`, il nome del file di chiave verrà conservato nel modulo e incorporato nell'assembly che viene creato quando si compila un assembly con [/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md).  
  
 È possibile specificare questa opzione anche come attributo personalizzato (<xref:System.Reflection.AssemblyKeyNameAttribute>) nel codice sorgente per qualsiasi modulo di Microsoft intermediate language (MSIL).</xref:System.Reflection.AssemblyKeyNameAttribute>  
  
 È inoltre possibile passare le informazioni di crittografia per il compilatore con [/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md). Utilizzare [/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md) se si desidera che un assembly parzialmente firmato.  
  
 Vedere [creazione e uso degli assembly](https://msdn.microsoft.com/library/xwb8f617) per ulteriori informazioni su come firmare un assembly.  
  
> [!NOTE]
>  Il `/keycontainer` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente consente di compilare file di origine `Input.vb` e specifica un contenitore di chiavi.  
  
```  
vbc /keycontainer:key1 input.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gli assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
