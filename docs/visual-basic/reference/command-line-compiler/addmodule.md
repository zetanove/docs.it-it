---
title: /addmodule | Documenti di Microsoft
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
- /addmodule compiler option [Visual Basic]
- addmodule compiler option [Visual Basic]
- -addmodule compiler option [Visual Basic]
ms.assetid: fb4b89d4-4926-4f20-868d-427fa28497b2
caps.latest.revision: 14
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
ms.openlocfilehash: 949962905ec933dc42301bf8c21654e73dbe2f70
ms.lasthandoff: 03/13/2017

---
# <a name="addmodule"></a>/addmodule
Fa sì che il compilatore renda disponibili per il progetto in compilazione tutte le informazioni sui tipi presenti nei file specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/addmodule:fileList  
```  
  
## <a name="arguments"></a>Argomenti  
 `fileList`  
 Obbligatorio. Elenco delimitato da virgole di file che contengono metadati ma non contengono manifesti dell'assembly. I nomi di file contenenti spazi devono essere racchiusi tra virgolette ("").  
  
## <a name="remarks"></a>Note  
 I file elencati mediante il `fileList` parametro deve essere creato con il `/target:module` opzione o con equivalente del compilatore `/target:module`.  
  
 Tutti i moduli aggiunti con `/addmodule` deve essere nella stessa directory del file di output in fase di esecuzione. Ovvero, è possibile specificare un modulo in una directory in fase di compilazione, ma il modulo deve essere nella directory dell'applicazione in fase di esecuzione. In caso contrario, si ottiene un <xref:System.TypeLoadException>errore.</xref:System.TypeLoadException>  
  
 Se si specifica, in modo implicito o esplicito, qualsiasi[/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md) opzione diversa da `/target:module` con `/addmodule`, i file si passa a `/addmodule` diventano parte dell'assembly del progetto. Un assembly è necessario per eseguire un file di output che contiene uno o più file aggiunti con `/addmodule`.  
  
 Utilizzare [/reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md) per importare i metadati da un file contenente un assembly.  
  
> [!NOTE]
>  Il `/addmodule` opzione non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, è disponibile solo durante la compilazione dalla riga di comando.  
  
## <a name="example"></a>Esempio  
 Il codice seguente crea un modulo.  
  
 [!code-vb[VbVbalrCompiler&#47;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/addmodule_1.vb)]  
  
 Il codice seguente consente di importare i tipi del modulo.  
  
 [!code-vb[VbVbalrCompiler n.&48;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/addmodule_2.vb)]  
  
 Quando si esegue `t1`, viene restituito `802`.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [/Reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
