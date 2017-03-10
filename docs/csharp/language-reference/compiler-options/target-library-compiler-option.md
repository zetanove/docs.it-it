---
title: "/target:library (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/dll"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-target compiler options [C#], /target:library"
  - "target compiler options [C#], /target:library"
  - "/target compiler options [C#], /target:library"
ms.assetid: c5670e88-2126-47c1-8d1c-217923837d17
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# /target:library (C# Compiler Options)
L'opzione **\/target:library** consente la creazione di una libreria DLL anziché di un file eseguibile EXE.  
  
## Sintassi  
  
```  
/target:library  
```  
  
## Note  
 La libreria creata avrà estensione DLL.  
  
 Se non diversamente specificato mediante l'opzione [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), il nome del file di output corrisponderà al nome del primo file di input.  
  
 Quando specificato alla riga di comando, tutti i file fino alla successiva opzione **\/out** o **\/target:module** verranno utilizzati per creare il file DLL.  
  
 Quando si compila un file DLL non è richiesto alcun metodo [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Applicazione**.  
  
3.  Modificare la proprietà **Tipo di output**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## Esempio  
 Compilare `in.cs`, creando `in.dll`.  
  
```  
csc /target:library in.cs  
```  
  
## Vedere anche  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)