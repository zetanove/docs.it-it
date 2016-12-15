---
title: "/target:exe (C# Compiler Options) | Microsoft Docs"
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
  - "/exe"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "target compiler options [C#], /target:exe"
  - "/target compiler options [C#], /target:exe"
  - "-target compiler options [C#], /target:exe"
ms.assetid: bda5717d-1b91-4848-956b-fcf85c30e432
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /target:exe (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specificando l'opzione **\/target:exe** il compilatore crea un'applicazione console eseguibile \(EXE\).  
  
## Sintassi  
  
```  
/target:exe  
```  
  
## Note  
 L'opzione **\/target:exe** è attiva per impostazione predefinita.  Il file eseguibile creato avrà estensione EXE.  
  
 Per creare un programma eseguibile per Windows, utilizzare [\/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md).  
  
 Se non diversamente specificato mediante l'opzione [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), il nome del file di output corrisponderà al nome del file di input che contiene il metodo [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md).  
  
 Quando specificato alla riga di comando, tutti i file fino alla successiva opzione **\/out** o **\/target:module** verranno utilizzati per creare il file EXE.  
  
 È necessario un unico metodo **Main** nei file di codice sorgente che vengono compilati in un file EXE.  L'opzione del compilatore [\/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) consente di specificare la classe contenente il metodo **Main**, nei casi in cui il codice presenti più classi con un metodo **Main**.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Applicazione**.  
  
3.  Modificare la proprietà **Tipo di output**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## Esempio  
 Ciascuna delle seguenti righe di comando compilerà `in.cs`, creando `in.exe`:  
  
```  
csc /target:exe in.cs  
csc in.cs  
```  
  
## Vedere anche  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)