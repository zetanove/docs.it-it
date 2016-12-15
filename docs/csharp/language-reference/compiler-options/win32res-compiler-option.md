---
title: "/win32res (C# Compiler Options) | Microsoft Docs"
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
  - "/win32res"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "win32res compiler option"
  - "/win32res compiler option [C#]"
  - "-win32res compiler option [C#]"
  - "win32res compiler option [C#]"
ms.assetid: 3c33f750-6948-4c7e-a27e-bef98f77255b
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /win32res (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/win32res** consente di inserire una risorsa Win32 nel file di output.  
  
## Sintassi  
  
```  
/win32res:filename  
```  
  
## Argomenti  
 `filename`  
 Rappresenta il file di risorse che si desidera aggiungere al file di output.  
  
## Note  
 Un file di risorse Win32 può essere creato con il [Compilatore di risorse](http://go.microsoft.com/fwlink/?LinkId=148370).  Il Compilatore di risorse viene richiamato quando si compila un programma Visual C\+\+. Il file con estensione res viene creato dal file con estensione rc.  
  
 Una risorsa Win32 può contenere informazioni sulla versione o su un'immagine bitmap \(icona\) che consentono di identificare l'applicazione in Esplora file.  Se l'opzione **\/win32res** non viene specificata, durante le compilazione verranno generate informazioni di versione basate sulla versione dell'assembly.  
  
 Per informazioni su come allegare o fare riferimento a un file di risorse .NET Framework, vedere rispettivamente [\/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md) o [\/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Applicazione**.  
  
3.  Fare clic sul pulsante **File di risorse** e scegliere un file tramite la casella combinata.  
  
## Esempio  
 Compilare `in.cs` e allegare il file di risorse Win32 `rf.res` per generare `in.exe`:  
  
```  
csc /win32res:rf.res in.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)