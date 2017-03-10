---
title: "/pdb (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/pdb"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-pdb compiler option [C#]"
  - "pdb compiler option [C#]"
  - "/pdb compiler option [C#]"
ms.assetid: e9d0f96a-5b75-45d6-9765-92538dd5f823
caps.latest.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 8
---
# /pdb (C# Compiler Options)
L'opzione del compilatore **\/pdb** consente di specificare il nome e il percorso del file di simboli di debug.  
  
## Sintassi  
  
```  
/pdb:filename  
```  
  
## Argomenti  
 `filename`  
 Nome e percorso del file di simboli di debug.  
  
## Note  
 Quando si specifica [\/debug \(Emit Debugging Information\)](../../../csharp/language-reference/compiler-options/debug-compiler-option.md), il compilatore crea nella stessa directory in cui verrà creato il file di output \(con estensione exe o dll\) un file con estensione pdb il cui nome è identico a quello del file di output.  
  
 **\/pdb** consente di specificare un nome e un percorso non predefiniti per il file con estensione pdb.  
  
 Questa opzione del compilatore non può essere impostata nell'ambiente di sviluppo di Visual Studio, né modificata a livello di codice.  
  
## Esempio  
 Compilare `t.cs` e creare un file con estensione pdb denominato tt.pdb:  
  
```  
csc /debug /pdb:tt t.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)