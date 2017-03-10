---
title: "/warn (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/warn"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "warning level [C#]"
  - "/w compiler option [C#]"
  - "-w compiler option [C#]"
  - "-warn compiler option [C#]"
  - "/warn compiler option [C#]"
  - "w compiler option [C#]"
  - "warn compiler option [C#]"
ms.assetid: 5f80ff59-4991-4382-9f9a-77da18446e71
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# /warn (C# Compiler Options)
L'opzione **\/warn** specifica il livello di avviso da visualizzare.  
  
## Sintassi  
  
```  
/warn:option  
```  
  
## Argomenti  
 `option`  
 Il livello degli avvisi da visualizzare per la compilazione. I numeri inferiori indicano solo gli avvisi di maggiore gravità, mentre i numeri superiori descrivono più avvisi.  I valori validi sono compresi tra 0 e 4.  
  
|Livello avvisi|Significato|  
|--------------------|-----------------|  
|0|Disattiva l'emissione di qualsiasi messaggio di avviso.|  
|1|Vengono visualizzati gli avvisi di maggiore gravità.|  
|2|Visualizza gli avvisi di livello 1 e alcuni avvisi di minore gravità, quali gli avvisi relativi ai membri nascosti delle classi.|  
|3|Visualizza gli avvisi di livello 2 e alcuni avvisi di minore gravità, ad esempio quelli relativi alle espressioni che restituiscono sempre `true` o `false`.|  
|4 \(valore predefinito\)|Visualizza tutti gli avvisi di livello 3 e gli avvisi informativi.|  
  
## Note  
 Per informazioni su un errore o un avviso, è possibile cercare il codice corrispondente nell'indice della Guida.  Per altri modi di ottenere informazioni su un errore o un avviso, vedere [C\# Compiler Errors](../../../csharp/language-reference/compiler-messages/index.md).  
  
 Utilizzare [\/warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md) per far sì che tutti gli avvisi vengano considerati come errori.  Utilizzare [\/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) per disabilitare determinati avvisi.  
  
 **\/w** rappresenta la versione abbreviata di **\/warn**.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Modificare la proprietà **Livello avvisi**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.WarningLevel%2A>.  
  
## Esempio  
 Compilare `in.cs` e fare in modo che il compilatore visualizzi solo gli avvisi di livello 1:  
  
```  
csc /warn:1 in.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)