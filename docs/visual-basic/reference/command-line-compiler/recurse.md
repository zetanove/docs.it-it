---
title: "/recurse | Microsoft Docs"
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
  - "/recurse compiler option [Visual Basic]"
  - "-recurse compiler option [Visual Basic]"
  - "recurse compiler option [Visual Basic]"
ms.assetid: 84a0b670-33ae-44c4-a46a-b90388809317
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# /recurse
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di compilare file di codice sorgente in tutte le directory figlio della directory specificata o della directory del progetto.  
  
## Sintassi  
  
```  
/recurse:[dir\]file  
```  
  
## Argomenti  
 `dir`  
 Parametro facoltativo.  Rappresenta la directory in cui si desidera che abbia inizio la ricerca.  Se non viene specificata alcuna directory, la ricerca avrà inizio nella directory del progetto.  
  
 `file`  
 Obbligatorio.  Rappresenta uno o più file da cercare.  È consentito l'utilizzo dei caratteri jolly.  
  
## Note  
 È possibile utilizzare caratteri jolly in un nome file per compilare tutti i file corrispondenti della directory del progetto senza utilizzare `/recurse`.  Se non viene specificato il nome di un file di output, a questo scopo verrà utilizzato il nome del primo file di input elaborato.  In genere si tratta del primo file dell'elenco dei file compilati ordinati alfabeticamente.  Per questo motivo, è consigliabile specificare un file di output utilizzando l'opzione `/out`.  
  
> [!NOTE]
>  L'opzione `/recurse` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice seguente consente di compilare tutti i file [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] della directory corrente.  
  
```  
vbc *.vb  
```  
  
 Il codice seguente consente di compilare tutti i file [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] della directory `Test\ABC` e delle directory sottostanti, generando il file `Test.ABC.dll`.  
  
```  
vbc /target:library /out:Test.ABC.dll /recurse:Test\ABC\*.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/out](../../../visual-basic/reference/command-line-compiler/out.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)