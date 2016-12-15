---
title: "/filealign (C# Compiler Options) | Microsoft Docs"
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
  - "/filealign"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/alignment compiler option [C#]"
  - "filealign compiler option [C#]"
  - "-filealign compiler option [C#]"
  - "/sections compiler option [C#]"
  - "alignment compiler option [C#]"
  - "sections compiler option [C#]"
  - "-sections compiler option [C#]"
  - "/filealign compiler option [C#]"
  - "file sharing [C#]"
  - "-alignment compiler option [C#]"
  - "section alignment [C#]"
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /filealign (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/filealign** consente di specificare le dimensioni delle sezioni del file di output.  
  
## Sintassi  
  
```  
/filealign:number  
```  
  
## Argomenti  
 `number`  
 Rappresenta un valore che specifica le dimensioni delle sezioni del file di output.  I valori validi sono 512, 1024, 2048, 4096 e 8192.  I valori sono in byte.  
  
## Note  
 Ogni sezione viene allineata a una posizione iniziale multipla del valore di **\/filealign**.  Non esiste un'impostazione predefinita fissa.  Se **\/filealign** non è specificato, in Common Language Runtime verrà scelto un valore predefinito in fase di compilazione.  
  
 La specifica delle dimensioni delle sezioni ha effetto sulle dimensioni del file di output.  La modifica delle dimensioni delle sezioni può quindi rivelarsi utile per i programmi eseguiti su periferiche con capacità ridotta.  
  
 Utilizzare [DUMPBIN](/visual-cpp/build/reference/dumpbin-options) per visualizzare informazioni sulle sezioni del file di output.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Fare clic sul pulsante **Avanzate**.  
  
4.  Modificare la proprietà **Allineamento file**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)