---
title: "/keycontainer (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/keycontainer"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/keycontainer compiler option [C#]"
  - "keycontainer compiler option [C#]"
  - "-keycontainer compiler option [C#]"
ms.assetid: b3982b6d-2382-4f7e-bebd-ce98eaa30763
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /keycontainer (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica il nome del contenitore di chiavi di crittografia.  
  
## Sintassi  
  
```  
/keycontainer:string  
```  
  
## Argomenti  
 `string`  
 Nome del contenitore di chiavi con nome sicuro.  
  
## Note  
 Quando viene utilizzata l'opzione **\/keycontainer**, il compilatore crea un componente condivisibile inserendo una chiave pubblica dal contenitore specificato nel manifesto dell'assembly e firmando l'assembly finale con la chiave privata.  Per generare un file di chiave, digitare sn \-k `file` nella riga di comando. sn \-i installa la coppia di chiavi in un contenitore.  
  
 Se si esegue la compilazione con [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), il nome del file di chiave verrà conservato nel modulo e incorporato nell'assembly, quando il modulo verrà compilato in un assembly con [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md).  
  
 Questa opzione può essere specificata anche come attributo personalizzato \(<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>\) nel codice sorgente di qualsiasi modulo MSIL \(Microsoft Intermediate Language\).  
  
 È possibile passare al compilatore le informazioni di crittografia anche mediante [\/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md).  Utilizzare [\/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md) se si desidera aggiungere la chiave pubblica al manifesto dell'assembly, ma si preferisce ritardare la firma dell'assembly finché non ne viene eseguito il test.  
  
 Per ulteriori informazioni, vedere [Creazione e utilizzo degli assembly con nome sicuro](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md) e [Ritardo della firma di un assembly](../Topic/Delay%20Signing%20an%20Assembly.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Questa opzione del compilatore non è disponibile nell'ambiente di sviluppo di Visual Studio.  
  
 È possibile accedere a questa opzione del compilatore a livello di codice con <xref:VSLangProj.ProjectProperties.AssemblyKeyContainerName%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)