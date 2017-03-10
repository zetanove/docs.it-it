---
title: "/quiet | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "/quiet"
  - "quiet"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-quiet compiler option [Visual Basic]"
  - "/quiet compiler option [Visual Basic]"
  - "quiet compiler option [Visual Basic]"
ms.assetid: 5d77fa23-4c50-4708-8535-649912b098e8
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# /quiet
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di impedire la visualizzazione del codice per avvisi ed errori relativi alla sintassi da parte del compilatore.  
  
## Sintassi  
  
```  
/quiet  
```  
  
## Note  
 Per impostazione predefinita, `/quiet` non è attiva.  Quando nel compilatore viene segnalato un errore o un avviso relativo alla sintassi, viene visualizzata anche la riga del codice sorgente.  Nel caso di applicazioni che analizzano l'output del compilatore, può essere preferibile visualizzare solo il testo della diagnostica.  
  
 Nell'esempio seguente `Module1` genera un errore che comprende il codice sorgente se compilato senza l'opzione `/quiet`.  
  
```  
Module Module1  
    Sub Main()  
        x()  
    End Sub  
End Module  
```  
  
 Output:  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
 `x`  
  
 `~`  
  
 Se la compilazione viene eseguita con l'opzione `/quiet`, verrà visualizzato solo quanto segue:  
  
 `E:\test\t2.vb(3) : error BC30451: Name 'x' is not declared.`  
  
> [!NOTE]
>  L'opzione `/quiet` non è disponibile all'interno dell'ambiente di sviluppo di Visual Studio, ma solo durante la compilazione dalla riga di comando.  
  
## Esempio  
 Il codice seguente consente di compilare `T2.vb` senza visualizzare il codice della diagnostica relativa alla sintassi:  
  
```  
vbc /quiet t2.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)