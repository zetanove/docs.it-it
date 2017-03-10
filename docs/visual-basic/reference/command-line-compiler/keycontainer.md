---
title: "/keycontainer | Microsoft Docs"
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
  - "-keycontainer compiler option [Visual Basic]"
  - "keycontainer compiler option [Visual Basic]"
  - "/keycontainer compiler option [Visual Basic]"
ms.assetid: 6a9bc861-1752-4db1-9f64-b5252f0482cc
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# /keycontainer
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica il nome di un contenitore di chiavi per una coppia di chiavi allo scopo di assegnare a un assembly un nome sicuro.  
  
## Sintassi  
  
```  
/keycontainer:container  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`container`|Obbligatorio.  File contenitore contenente la chiave.  Racchiudere il nome file tra virgolette \(""\) se il nome contiene uno spazio.|  
  
## Note  
 Il componente viene reso condivisibile mediante l'inserimento di una chiave pubblica nel manifesto dell'assembly e la firma dell'assembly finale con la chiave privata.  Per generare un file di chiave, immettere `sn -k` `file` nella riga di comando.  L'opzione `-i` consente di installare la coppia di chiavi in un contenitore.  Per ulteriori informazioni, vedere [Sn.exe \(Strong Name Tool\)](../Topic/Sn.exe%20\(Strong%20Name%20Tool\).md).  
  
 Se si esegue la compilazione con l'opzione `/target:module`, il nome del file di chiavi verrà conservato nel modulo e incorporato nell'assembly che viene creato quando si compila un assembly con l'opzione [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md).  
  
 Questa opzione può essere specificata anche come attributo personalizzato \(<xref:System.Reflection.AssemblyKeyNameAttribute>\) nel codice sorgente di qualsiasi modulo MSIL \(Microsoft Intermediate Language\).  
  
 È anche possibile passare al compilatore le informazioni di crittografia mediante [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md).  Utilizzare [\/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md) se si desidera che l'assembly sia parzialmente firmato.  
  
 Per ulteriori informazioni sulla firma di un assembly, vedere [Creazione e utilizzo degli assembly con nome sicuro](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md).  
  
> [!NOTE]
>  L'opzione `/keycontainer` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice che segue consente di compilare il file di origine `Input.vb` e specificare un contenitore di chiavi.  
  
```  
vbc /keycontainer:key1 input.vb  
```  
  
## Vedere anche  
 [Assembly e Global Assembly Cache](../Topic/Assemblies%20and%20the%20Global%20Assembly%20Cache%20\(C%23%20and%20Visual%20Basic\).md)   
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)