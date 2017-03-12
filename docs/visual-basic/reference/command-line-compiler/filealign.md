---
title: "/filealign | Microsoft Docs"
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
  - "sections compiler option [Visual Basic]"
  - "alignment compiler option [Visual Basic]"
  - "-filealign compiler option [Visual Basic]"
  - "section alignment"
  - "/filealign compiler option [Visual Basic]"
  - "filealign compiler option [Visual Basic]"
ms.assetid: cc61ec3d-ad38-4b28-9659-099d73cad099
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# /filealign
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica la posizione di allineamento per le sezioni del file di output.  
  
## Sintassi  
  
```  
/filealign:number  
```  
  
## Argomenti  
 `number`  
 Obbligatorio.  Rappresenta un valore che specifica l'allineamento delle sezioni del file di output.  I valori validi sono 512, 1024, 2048, 4096 e 8192.  I valori sono in byte.  
  
## Note  
 Con l'opzione `/filealign` è possibile specificare l'allineamento delle sezioni del file di output.  Le sezioni sono blocchi di memoria contigua presenti in un file eseguibile portabile \(PE, Portable Executable\) che contiene codice o dati.  L'opzione `/filealign` consente di compilare l'applicazione con un allineamento non standard. Per tale motivo, la maggior parte degli sviluppatori non ha necessità di utilizzarlo.  
  
 Ogni sezione viene allineata rispetto a un limite che rappresenta un multiplo del valore di `/filealign`.  Non esiste un'impostazione predefinita fissa.  Se il valore `/filealign` non è specificato, verrà scelto un valore predefinito in fase di compilazione.  
  
 Specificando le dimensioni delle sezioni è possibile modificare le dimensioni del file di output.  La modifica delle dimensioni delle sezioni può quindi rivelarsi utile per i programmi eseguiti su periferiche con capacità ridotta.  
  
> [!NOTE]
>  L'opzione `/filealign` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)