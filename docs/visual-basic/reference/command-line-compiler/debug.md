---
title: "/debug (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "debug compiler switches"
  - "/debug compiler option [Visual Basic]"
  - "-debug compiler option [Visual Basic]"
  - "debug compiler option [Visual Basic]"
ms.assetid: c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /debug (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nel corso della compilazione consente la generazione di informazioni di debug che verranno quindi inserite nei file di output.  
  
## Sintassi  
  
```  
/debug[+ | -]  
' -or-  
/debug:[full | pdbonly]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`+`  &#124; `-`|Parametro facoltativo.  Se si specifica l'argomento `+` o `/debug`, verranno generate informazioni di debug che saranno inserite dal compilatore in un file PDB.  Specificare `-` produce gli stessi effetti della mancata specifica di `/debug`.|  
|`full`  &#124; `pdbonly`|Parametro facoltativo.  Determina il tipo di informazioni di debug generate dal compilatore.  Se non si specifica `/debug:pdbonly`, l'impostazione predefinita sarà `full`, che consente di collegare un debugger al programma in esecuzione.  L'argomento `pdbonly` consente il debug del codice sorgente quando il programma viene avviato nel debugger, ma l'assembler viene visualizzato solo quando il programma in esecuzione è collegato al debugger.|  
  
## Note  
 Utilizzare questa opzione per creare build di debug.  Se non si specifica `/debug`, `/debug+` o `/debug:full`, non sarà possibile effettuare il debug del file di output del programma.  
  
 Per impostazione predefinita, le informazioni di debug non vengono generate \(`/debug-`\).  Per generare informazioni di debug, specificare `/debug` o `/debug+`.  
  
 Per informazioni sulla modalità di configurazione delle prestazioni di debug di un'applicazione, vedere [Semplificazione del debug di un'immagine](../Topic/Making%20an%20Image%20Easier%20to%20Debug.md).  
  
||  
|-|  
|Per impostare \/debug nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Con un progetto selezionato in **Esplora soluzioni**, scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Fare clic su **Opzioni di compilazione avanzate**.<br />4.  Modificare il valore nella casella **Genera informazioni di debug**.|  
  
## Esempio  
 Nell'esempio riportato di seguito le informazioni di debug vengono inserite nel file di output `App.exe`.  
  
```  
vbc /debug /out:app.exe test.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)