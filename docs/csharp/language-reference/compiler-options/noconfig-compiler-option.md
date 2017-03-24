---
title: "/noconfig (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/noconfig"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/noconfig compiler option [C#]"
  - "csc.rsp"
  - "-noconfig compiler option [C#]"
  - "noconfig compiler option [C#]"
ms.assetid: cd26967e-e494-4c8c-b5c9-af13b2f78b2e
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# /noconfig (C# Compiler Options)
L'opzione **\/noconfig** indica al compilatore di non eseguire la compilazione utilizzando il file csc.rsp, memorizzato e caricato dalla stessa directory in cui si trova il file csc.exe.  
  
## Sintassi  
  
```  
/noconfig  
```  
  
## Note  
 Il file csc.rsp fa riferimento a tutti gli assembly forniti con .NET Framework.  I riferimenti effettivi inclusi nell'ambiente di sviluppo di Visual Studio .NET dipendono dal tipo di progetto.  
  
 È possibile modificare il file csc.rsp e specificare altre opzioni del compilatore da includere in ogni compilazione eseguita dalla riga di comando utilizzando il file csc.exe, ad eccezione dell'opzione **\/noconfig**.  
  
 Le opzioni passate al comando **csc** verranno elaborate nel compilatore per ultime.  Le opzioni della riga di comando eseguiranno pertanto l'override delle impostazioni relative alle stesse opzioni nel file csc.rsp.  
  
 Se non si desidera che il compilatore cerchi e utilizzi le impostazioni del file csc.rsp, specificare **\/noconfig**.  
  
 Questa opzione del compilatore non è disponibile in Visual Studio e non può essere modificata a livello di codice.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)