---
title: "/target:winexe (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/target:winexe"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/target compiler options [C#], /target:winexe"
  - "-target compiler options [C#], /target:winexe"
  - "target compiler options [C#], /target:winexe"
ms.assetid: b5a0619c-8caa-46a5-a743-1cf68408ad7a
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# /target:winexe (C# Compiler Options)
Specificando l'opzione **\/target:winexe**, il compilatore crea un programma eseguibile \(EXE\) per Windows.  
  
## Sintassi  
  
```  
/target:winexe  
```  
  
## Note  
 Il file eseguibile creato avrà estensione EXE.  Per programma per Windows si intende un programma che fornisce un'interfaccia utente dalla libreria di .NET Framework o con le API Win32.  
  
 Per creare un'applicazione console, utilizzare [\/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md).  
  
 Se non diversamente specificato mediante l'opzione [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), il nome del file di output corrisponderà al nome del file di input che contiene il metodo [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md).  
  
 Quando specificato alla riga di comando, tutti i file fino alla successiva opzione **\/out** o [\/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) verranno utilizzati per creare il programma per Windows.  
  
 È necessario un unico metodo **Main** nei file di codice sorgente che vengono compilati in un file EXE.  L'opzione [\/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) consente di specificare la classe contenente il metodo **Main**, nei casi in cui il codice presenti più classi con un metodo **Main**.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Applicazione**.  
  
3.  Modificare la proprietà **Tipo di output**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## Esempio  
 Compilare `in.cs` in un programma per Windows:  
  
```  
csc /target:winexe in.cs  
```  
  
## Vedere anche  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)