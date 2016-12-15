---
title: "/platform (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/13/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/platform"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "platform compiler option [C#]"
  - "-platform compiler option [C#]"
  - "/platform compiler option [C#]"
ms.assetid: c290ff5e-47f4-4a85-9bb3-9c2525b0be04
caps.latest.revision: 46
caps.handback.revision: 46
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /platform (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica la versione di Common Language Runtime \(CLR\) in grado di eseguire l'assembly.  
  
## Sintassi  
  
```  
/platform:string  
```  
  
#### Parametri  
 `string`  
 anycpu \(impostazione predefinita\), anycpu32bitpreferred, ARM, x64, x86, o Itanium.  
  
## Note  
  
-   **anycpu** \(valore predefinito\) consente di compilare l'assembly in modo da essere eseguito su qualsiasi piattaforma.  L'applicazione viene eseguita come processo a 64 bit quando possibile e esegue il fallback a 32 bit quando solo questa modalità è disponibile.  
  
-   **anycpu32bitpreferred**: consente di compilare l'assembly in modo che sia possibile eseguirlo su qualsiasi piattaforma.  L'applicazione viene eseguita in modalità a 32 bit sui sistemi che supportano sia le applicazioni a 64 bit che quelle a 32 bit.  È possibile specificare questa opzione solo per i progetti destinati a .NET Framework 4.5.  
  
-   **ARM** compila l'assembly in modo da essere eseguito su un computer dotato di un processore Advanced RISC Machine \(ARM\).  
  
-   **x64**: consente di compilare l'assembly in modo che sia possibile eseguirlo con Common Language Runtime a 64 bit su un computer che supporta il set di istruzioni AMD64 o EM64T  
  
-   **x86** compila l'assembly in modo da essere eseguito dalla versione di Common Language Runtime compatibile con x86 a 32 bit.  
  
-   **Itanium** compila l'assembly in modo da essere eseguito dalla versione di Common Language Runtime a 64 bit in un computer con processore Itanium.  
  
 In un sistema operativo Windows a 64 bit:  
  
-   Gli assembly compilati con **\/platform:x86** verranno eseguiti dalla versione di Common Language Runtime a 32 bit in WOW64.  
  
-   Una DLL compilata con l'opzione **\/platform:anycpu** viene eseguita dallo stesso Common Language Runtime del processo in cui viene caricata.  
  
-   Gli eseguibili compilati con **\/platform:anycpu** sono eseguiti dalla versione di Common Language Runtime a 64 bit.  
  
-   Gli eseguibili compilati con l'opzione **\/platform:anycpu32bitpreferred** sono eseguiti da Common Language Runtime a 32 bit.  
  
 L'impostazione **anycpu32bitpreferred** è valida solo per file eseguibili \(.EXE\) e richiede .NET Framework 4.5.  
  
 Per ulteriori informazioni sullo sviluppo di un'applicazione da eseguire in un sistema operativo Windows a 64 bit, vedere [Applicazioni a 64 bit](../Topic/64-bit%20Applications.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Modificare la proprietà **Piattaforma di destinazione** e, per i progetti destinati a .NET Framework 4.5, selezionare o deselezionare la casella di controllo **Preferisci 32 bit**.  
  
 **Nota**  
 **\/platform** non è disponibile nell'ambiente di sviluppo di Visual C\# Express.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.PlatformTarget%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'opzione **\/platform** per specificare che l'applicazione deve essere eseguita dalla versione di Common Language Runtime a 64 bit in un sistema operativo Windows a 64 bit.  
  
```  
csc /platform:anycpu filename.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)