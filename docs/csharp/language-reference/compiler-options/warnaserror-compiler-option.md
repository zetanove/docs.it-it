---
title: "/warnaserror (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/warnaserror"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/warnaserror compiler option [C#]"
  - "-warnaserror compiler option [C#]"
  - "warnaserror compiler option [C#]"
ms.assetid: 04680ec3-08d6-4e2e-a274-38310e10e33c
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /warnaserror (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specificando l'opzione **\/warnaserror\+**, tutti gli avvisi vengono gestiti come errori.  
  
## Sintassi  
  
```  
/warnaserror[<U>+</U> | -][:warning-list]  
```  
  
## Note  
 Tutti i messaggi che, in condizioni normali, verrebbero presentati come avvisi vengono invece segnalati come errori, con l'interruzione del processo di compilazione e, di conseguenza, senza la creazione di file di output.  
  
 Per impostazione predefinita, è attiva l'opzione **\/warnaserror\-** e gli avvisi non impediscono quindi la generazione di un file di output.  Con l'opzione **\/warnaserror**, che equivale a **\/warnaserror\+**, gli avvisi vengono gestiti come errori.  
  
 Se eventualmente si desidera che solo determinati avvisi vengano gestiti come errori, è possibile specificare un elenco delimitato da virgole contenente i numeri di avviso da considerare come tali.  
  
 Per specificare il livello di avvisi che il compilatore deve visualizzare, utilizzare [\/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md).  Utilizzare [\/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) per disabilitare determinati avvisi.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Modificare la proprietà **Considera gli avvisi come errori**.  
  
     Per impostare l'opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.TreatWarningsAsErrors%2A>.  
  
## Esempio  
 Compilare `in.cs` e fare in modo che il compilatore non visualizzi alcun avviso:  
  
```  
csc /warnaserror in.cs  
csc /warnaserror:642,649,652 in.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)