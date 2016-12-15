---
title: "/verbose | Microsoft Docs"
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
  - "verbose compiler option [Visual Basic]"
  - "-verbose compiler option [Visual Basic]"
  - "/verbose compiler option [Visual Basic]"
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /verbose
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Determina la generazione di messaggi di stato e di errore dettagliati.  
  
## Sintassi  
  
```  
/verbose[+ | -]  
```  
  
## Argomenti  
 `+` &#124; `-`  
 Parametro facoltativo.  L'opzione `/verbose` equivale all'opzione `/verbose+`, che determina la visualizzazione di messaggi dettagliati.  Il valore predefinito per questa opzione è `/verbose-`.  
  
## Note  
 L'opzione  `/verbose` consente di visualizzare informazioni sul numero totale di errori generati dal compilatore, sugli assembly che vengono caricati da un modulo e sui file attualmente in fase di compilazione.  
  
> [!NOTE]
>  L'opzione `/verbose` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio. È disponibile soltanto durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice riportato di seguito compila `In.vb` e richiede al compilatore di visualizzare informazioni dettagliate sullo stato.  
  
```  
vbc /verbose in.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)