---
title: "/win32icon (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/win32icon"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "win32icon compiler option [C#]"
  - "/win32icon compiler option [C#]"
  - "-win32icon compiler option [C#]"
ms.assetid: 756d9b6d-ab07-41b7-ba58-5bd88f711138
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# /win32icon (C# Compiler Options)
L'opzione **\/win32icon** consente di inserire nel file di output un file .ico, che conferisce al file di output l'aspetto desiderato in Esplora file.  
  
## Sintassi  
  
```  
/win32icon:filename  
```  
  
## Argomenti  
 `filename`  
 Rappresenta il file ICO che si desidera aggiungere al file di output.  
  
## Note  
 Un file .ico può essere creato mediante il [Compilatore di risorse](http://go.microsoft.com/fwlink/?LinkId=148370).  Il compilatore di risorse viene richiamato quando si compila un programma Visual C\+\+ e il file ICO viene creato sulla base del file RC.  
  
 Per informazioni su come allegare o fare riferimento a un file di risorse .NET Framework, vedere rispettivamente [\/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md) o [\/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md).  Per informazioni sull'importazione di un file RES, vedere [\/win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire le pagine **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Applicazione**.  
  
3.  Modificare la proprietà **Icona applicazione**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.ApplicationIcon%2A>.  
  
## Esempio  
 Compilare `in.cs` e allegare il file ICO `rf.ico` per generare `in.exe`:  
  
```  
csc /win32icon:rf.ico in.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)