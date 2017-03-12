---
title: "/warnaserror (Visual Basic) | Microsoft Docs"
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
  - "warnaserror compiler option [Visual Basic]"
  - "/warnaserror compiler option [Visual Basic]"
  - "-warnaserror compiler option [Visual Basic]"
ms.assetid: 49819f1d-a1bd-4201-affe-5afe6d9712e1
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# /warnaserror (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Indica al compilatore di considerare la prima occorrenza di un avviso come un errore.  
  
## Sintassi  
  
```  
/warnaserror[+ | -][:numberList]  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|\+ &#124; \-|Parametro facoltativo.  Per impostazione predefinita, è attiva l'opzione `/warnaserror-`, pertanto gli avvisi non impediscono la generazione di un file di output.  Con l'opzione `/warnaserror` , che equivale a `/warnaserror+`, gli avvisi vengono invece considerati come errori.|  
|`numberList`|Parametro facoltativo.  Elenco delimitato da virgole di numeri di avviso a cui viene applicata l'opzione `/warnaserror`.  Se non vengono specificati ID di avviso, l'opzione `/warnaserror` si applica a tutti gli avvisi.|  
  
## Note  
 Specificando l'opzione `/warnaserror`, gli avvisi vengono considerati come errori.  Tutti i messaggi che, in condizioni normali, verrebbero presentati come avvisi vengono invece segnalati come errori.  Le occorrenze successive dello stesso avviso vengono segnalate come avvisi.  
  
 Per impostazione predefinita, l'opzione `/warnaserror-` è attiva, pertanto gli avvisi hanno scopo esclusivamente informativo.  Con l'opzione `/warnaserror` , che equivale a `/warnaserror+`, gli avvisi vengono invece considerati come errori.  
  
 Se si desidera che solo determinati avvisi vengano gestiti come errori, è possibile specificare un elenco delimitato da virgole contenente i numeri di avviso da considerare come tali.  
  
> [!NOTE]
>  L'opzione `/warnaserror` non controlla le modalità di visualizzazione degli avvisi.  Utilizzare l'opzione [\/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md) per disabilitare gli avvisi.  
  
||  
|-|  
|Per impostare \/warnaserror in modo che tutti gli avvisi vengano considerati come errori all'interno dell'IDE di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Verificare che la casella di controllo **Disabilita tutti gli avvisi** sia deselezionata.<br />4.  Selezionare la casella di controllo **Considera tutti gli avvisi come errori**.|  
  
||  
|-|  
|Per impostare \/warnaserror in modo che solo determinati avvisi vengano considerati come errori all'interno dell'IDE di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Verificare che la casella di controllo **Disabilita tutti gli avvisi** sia deselezionata.<br />4.  Verificare che la casella di controllo **Considera tutti gli avvisi come errori** sia deselezionata.<br />5.  Selezionare **Errore** dalla colonna **Notifica** adiacente all'avviso da considerare come errore.|  
  
## Esempio  
 Nel codice riportato di seguito viene compilato `In.vb` viene visualizzato un errore per la prima occorrenza di ogni avviso generato.  
  
```  
vbc /warnaserror in.vb  
```  
  
## Esempio  
 Nel codice riportato di seguito viene compilato `T2.vb` e viene considerato come errore solo l'avviso relativo alle variabili locali non utilizzate \(42024\).  
  
```  
vbc /warnaserror:42024 t2.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic)