---
title: "/addmodule | Microsoft Docs"
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
  - "/addmodule compiler option [Visual Basic]"
  - "addmodule compiler option [Visual Basic]"
  - "-addmodule compiler option [Visual Basic]"
ms.assetid: fb4b89d4-4926-4f20-868d-427fa28497b2
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# /addmodule
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Permette al compilatore di rendere disponibili al progetto in corso di compilazione tutte le informazioni sui tipi presenti nei file specificati.  
  
## Sintassi  
  
```  
/addmodule:fileList  
```  
  
## Argomenti  
 `fileList`  
 Obbligatorio.  Elenco delimitato da virgole dei file che contengono metadati ma non manifesti degli assembly.  I nomi dei file che contengono spazi devono essere racchiusi tra virgolette \(" "\).  
  
## Note  
 I file elencati mediante il parametro `fileList` devono essere creati con l'opzione `/target:module` o con un'altra opzione del compilatore equivalente.  
  
 Tutti i moduli aggiunti con `/addmodule` dovranno trovarsi nella stessa directory del file di output in fase di esecuzione.  In fase di compilazione, è pertanto possibile specificare un modulo in una directory qualsiasi purché esso si trovi nella directory dell'applicazione in fase di esecuzione.  In caso contrario, verrà generato un errore <xref:System.TypeLoadException>.  
  
 Se si specifica, in modo implicito o esplicito, un'opzione [\/target](../../../visual-basic/reference/command-line-compiler/target.md) diversa da `/target:module` con `/addmodule`, i file passati ad `/addmodule` verranno inclusi nell'assembly del progetto.  Per eseguire un file di output a cui sono stati aggiunti uno o più file con `/addmodule` è necessario un assembly.  
  
 Utilizzare [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md) per importare metadati da un file contenente un assembly.  
  
> [!NOTE]
>  L'opzione `/addmodule` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice riportato di seguito crea un modulo.  
  
 [!code-vb[VbVbalrCompiler#47](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/addmodule_1.vb)]  
  
 Il codice riportato di seguito importa i tipi del modulo.  
  
 [!code-vb[VbVbalrCompiler#48](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/addmodule_2.vb)]  
  
 Quando si esegue `t1`, viene restituito `802`.  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)