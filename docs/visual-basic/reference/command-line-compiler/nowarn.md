---
title: "/nowarn | Microsoft Docs"
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
  - "nowarn compiler option [Visual Basic]"
  - "/nowarn compiler option [Visual Basic]"
  - "-nowarn compiler option [Visual Basic]"
ms.assetid: 7ebf2106-0652-4fdc-bf60-70fc86465d83
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# /nowarn
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di inibire la capacità del compilatore di generare avvisi.  
  
## Sintassi  
  
```  
/nowarn[:numberList]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`numberList`|Parametro facoltativo.  Elenco delimitato da virgole contenente i numeri degli ID avviso che il compilatore deve eliminare.  Se gli ID avviso non vengono specificati, vengono eliminati tutti gli avvisi.|  
  
## Note  
 L'opzione `/nowarn` inibisce la generazione degli avvisi da parte del compilatore.  Per eliminare un singolo avviso, specificare l'ID avviso nell'opzione `/nowarn` dopo i due punti.  Separare più numeri di avviso mediante virgole.  
  
 È sufficiente specificare solo la parte numerica dell'identificatore dell'avviso.  Se, ad esempio, si desidera eliminare l'avviso BC42024 relativo alle variabili locali non utilizzate, specificare `/nowarn:42024`.  
  
 Per ulteriori informazioni sui numeri di ID degli avvisi, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
||  
|-|  
|Per impostare \/nowarn nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Selezionare la casella di controllo **Disabilita tutti gli avvisi** per disabilitare tutti gli avvisi.<br />     \- oppure \-<br />     Per disabilitare un particolare avviso, fare clic su **Nessuno** dall'elenco a discesa adiacente all'avviso.|  
  
## Esempio  
 Il codice seguente consente di compilare `T2.vb` senza visualizzare avvisi.  
  
```  
vbc /nowarn t2.vb  
```  
  
## Esempio  
 Il codice seguente consente di compilare `T2.vb` senza visualizzare gli avvisi per le variabili locali non utilizzate \(42024\).  
  
```  
vbc /nowarn:42024 t2.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic)