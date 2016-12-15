---
title: "@ (Specify Response File) (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "@ (Specify Response File) compiler option [Visual Basic]"
ms.assetid: a6847eaa-e5f9-4303-9421-45b55484b9ca
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# @ (Specify Response File) (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica un file contenente le opzioni del compilatore e i file di codice sorgente da compilare.  
  
## Sintassi  
  
```  
@response_file  
```  
  
## Argomenti  
 `response_file`  
 Obbligatorio.  Rappresenta un file in cui sono elencate le opzioni del compilatore o i file di codice sorgente da compilare.  Racchiudere il nome file tra virgolette \(""\) se contiene uno spazio.  
  
## Note  
 Mediante il compilatore vengono elaborati le opzioni del compilatore e i file di codice sorgente specificati in un file di risposta come se fossero stati specificati sulla riga di comando.  
  
 Per specificare più file di risposta in una compilazione, definire più opzioni di file di risposta, come nel caso riportato di seguito.  
  
```  
@file1.rsp @file2.rsp  
```  
  
 In un file di risposta possono essere presenti, su una stessa riga, più opzioni del compilatore e più file di codice sorgente.  La specifica di una singola opzione del compilatore deve essere contenuta in un'unica riga e non può occupare più righe.  I file di risposta possono contenere commenti che iniziano con il simbolo `#`.  
  
 È possibile combinare opzioni specificate nella riga di comando con opzioni definite in uno o più file di risposta.  Le opzioni di comando verranno elaborate quando vengono rilevate dal compilatore.  È pertanto possibile che argomenti della riga di comando si sovrappongano alle opzioni specificate in precedenza nei file di risposta.  Per contro, le opzioni definite in un file di risposta sostituiranno quelle specificate in precedenza sulla riga di comando o in altri file di risposta.  
  
 In Visual Basic è disponibile il file Vbc.rsp, nella stessa directory in cui si trova il file Vbc.exe.  Tale file viene incluso per impostazione predefinita, a meno che non venga utilizzata l'opzione `/noconfig`.  Per ulteriori informazioni, vedere [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md).  
  
> [!NOTE]
>  L'opzione `@` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Le righe che seguono sono tratte da un file di risposta di esempio.  
  
```  
# build the first output file  
/target:exe   
/out:MyExe.exe  
source1.vb   
source2.vb  
```  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'opzione `@` con il file di risposta denominato `File1.rsp`.  
  
```  
vbc @file1.rsp  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)