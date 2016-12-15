---
title: "/target:appcontainerexe (opzioni del compilatore C#) | Microsoft Docs"
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
ms.assetid: e7e62229-23ea-4e53-bef5-380d951bf95f
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /target:appcontainerexe (opzioni del compilatore C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Se si utilizza l'opzione del compilatore **\/target:appcontainerexe**, il compilatore crea un file eseguibile di Windows \(exe\) che deve essere eseguito in un contenitore di app.  Questa opzione equivale a [\/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md), ma è progettata per le applicazioni [!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)].  
  
## Sintassi  
  
```  
/target:appcontainerexe  
```  
  
## Note  
 Per richiedere che l'applicazione venga eseguita in un contenitore di app, questa opzione imposta un bit nel file [eseguibile di tipo PE](http://go.microsoft.com/fwlink/p/?LinkId=236960).  Quando questo bit è impostato, viene generato un errore se il metodo CreateProcess tenta di avviare il file eseguibile all'esterno di un contenitore di app.  
  
 A meno che non si utilizzi l'opzione [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), il nome del file di output corrisponderà al nome del file di input contenente il metodo [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md).  
  
 Quando si specifica questa opzione da un prompt dei comandi, tutti i file fino alla successiva opzione **\/out** o **\/target** vengono utilizzati per creare il file eseguibile.  
  
### Per impostare l'opzione del compilatore nell'IDE  
  
1.  In **Esplora soluzioni** aprire il menu di scelta rapida per il progetto, quindi scegliere **Proprietà**.  
  
2.  Nell'elenco **Tipo di output** della scheda **Applicazione**, scegliere **Applicazione Windows Store**.  
  
     Questa opzione è disponibile solo per i modelli di app [!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)].  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## Esempio  
 Il seguente comando consente di compilare `filename.cs` in un file eseguibile di Windows che può essere eseguito solo in un contenitore di app.  
  
```  
csc /target:appcontainerexe filename.cs  
```  
  
## Vedere anche  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [\/target:winexe \(Create a Windows Program\)](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)