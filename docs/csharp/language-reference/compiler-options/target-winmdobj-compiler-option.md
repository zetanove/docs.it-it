---
title: "/target:winmdobj (opzioni del compilatore C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: 1819a045-659d-498a-9457-c466e902986f
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /target:winmdobj (opzioni del compilatore C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Se si utilizza l'opzione del compilatore **\/target:winmdobj**, verrà creato un file intermedio con estensione winmdobj che è possibile convertire in un file binario Windows Runtime \(winmd\).  Il file con estensione winmd può quindi essere utilizzato dai programmi C\+\+ e JavaScript, oltre ai programmi di linguaggi gestiti.  
  
## Sintassi  
  
```  
/target:winmdobj  
```  
  
## Note  
 L'impostazione **winmdobj** segnala al compilatore che è richiesto un modulo intermedio.  In risposta, Visual Studio consente di compilare la libreria di classi C\# come file con estensione winmdobj.  Il file con estensione winmdobj può quindi essere inserito dallo strumento di esportazione <xref:Microsoft.Build.Tasks.WinMDExp> per produrre un file di metadati Windows \(winmd\).  Il file con estensione winmd contiene il codice della libreria originale e i metadati di WinMD utilizzati da JavaScript o C\+\+ e da Windows Runtime.  
  
 L'output di un file compilato utilizzando l'opzione del compilatore **\/target:winmdobj** è progettato per essere utilizzato solo come input dell'utilità di esportazione WimMDExp. Al file con estensione winmdobj non viene fatto riferimento direttamente.  
  
 A meno che non si utilizzi l'opzione [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), il nome del file di output corrisponderà al nome del primo file di input.  Non è richiesto un metodo [principale](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md).  
  
 Se si specifica l'opzione \/target:winmdobj da un prompt dei comandi, tutti i file fino alla successiva opzione **\/out** o [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) vengono utilizzati per creare il programma per Windows.  
  
### Per impostare l'opzione del compilatore nell'IDE di Visual Studio per un'applicazione Windows Store  
  
1.  In **Esplora soluzioni** aprire il menu di scelta rapida per il progetto, quindi scegliere **Proprietà**.  
  
2.  Scegliere la scheda **Applicazione**.  
  
3.  Nell'elenco **Tipo di output**, scegliere **File WinMD**.  
  
     L'opzione **File WinMD** è disponibile solo per i modelli di applicazione [!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)].  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## Esempio  
 Il seguente comando consente di compilare `filename.cs` in un file intermedio con estensione winmdobj.  
  
```  
csc /target:winmdobj filename.cs  
```  
  
## Vedere anche  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)