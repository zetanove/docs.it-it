---
title: "/langversion (C# Compiler Options) | Microsoft Docs"
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
  - "/langversion"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/langversion compiler option [C#]"
  - "-langversion compiler option [C#]"
  - "langversion compiler option [C#]"
ms.assetid: 3fb00b05-a0ff-4782-b313-13a4c0f62d94
caps.latest.revision: 33
caps.handback.revision: 33
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /langversion (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Imposta il compilatore in modo da accettare solo sintassi inclusa nella specifica di linguaggio C\# selezionata.  
  
## Sintassi  
  
```  
/langversion:option  
```  
  
## Argomenti  
 `option`  
 Di seguito vengono illustrati i valori validi.  
  
|Opzione|Significato|  
|-------------|-----------------|  
|default|Il compilatore accetta tutte le sintassi di linguaggio valide.|  
|ISO\-1|Il compilatore accetta solo la sintassi inclusa nella specifica di linguaggio C\# ISO\/IEC 23270:2003.|  
|ISO\-2|Il compilatore accetta solo la sintassi inclusa nella specifica di linguaggio C\# ISO\/IEC 23270:2006.  Questa specifica è disponibile nel sito Web [ISO](http://go.microsoft.com/fwlink/?LinkId=144406).|  
|3|Il compilatore accetta solo la sintassi inclusa nella versione 3.0 di [Specifiche del linguaggio C\#](../../../csharp/language-reference/language-specification.md).|  
  
## Note  
 I metadati cui viene fatto riferimento nell'applicazione C\# non sono soggetti all'opzione **\/langversion** del compilatore.  
  
 Poiché ogni versione del compilatore C\# contiene estensioni della specifica del linguaggio, **\/langversion** non fornisce la funzionalità equivalente di una versione precedente del compilatore.  
  
 Indipendentemente dall'impostazione di **\/langversion** specificata, per creare il file con estensione exe o dll verrà utilizzata la versione corrente di Common Language Runtime.  Un'eccezione è costituita dagli assembly Friend e da [\/moduleassemblyname \(Specify Friend Assembly for Module\)](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md), eseguibili in **\/langversion:ISO\-1**.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Fare clic sul pulsante **Avanzate**.  
  
4.  Modificare la proprietà **Versione linguaggio**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.LanguageVersion%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Specifiche del linguaggio C\#](../../../csharp/language-reference/language-specification.md)