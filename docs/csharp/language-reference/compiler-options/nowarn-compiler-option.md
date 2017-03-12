---
title: "/nowarn (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/nowarn"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nowarn compiler option [C#]"
  - "/nowarn compiler option [C#]"
  - "-nowarn compiler option [C#]"
ms.assetid: 6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# /nowarn (C# Compiler Options)
L'opzione **\/nowarn** impedisce al compilatore di visualizzare uno o più avvisi.  Separare più numeri di avvisi mediante virgole.  
  
## Sintassi  
  
```  
/nowarn:number1[,number2,...]  
```  
  
## Argomenti  
 `number1`, `number2`  
 Il numero o i numeri degli avvisi che il compilatore non deve visualizzare.  
  
## Note  
 È sufficiente specificare la parte numerica dell'identificatore dell'avviso.  Se si desidera, ad esempio, disattivare la visualizzazione dell'avviso CS0028, sarà possibile specificare `/nowarn:28`.  
  
 I numeri di avviso passati a `/nowarn` che erano validi nei rilasci precedenti, ma che sono stati rimossi dal compilatore, verranno ignorati in modo invisibile all'utente.  L'avviso numero CS0679 era, ad esempio, valido nel compilatore di Visual Studio .NET 2002 ma è stato successivamente rimosso.  
  
 Non è possibile evitare la visualizzazione degli avvisi seguenti utilizzando l'opzione `/nowarn`:  
  
-   Compilatore avviso \(livello 1\) CS2002  
  
-   Compilatore avviso \(livello 1\) CS2023  
  
-   Compilatore avviso \(livello 1\) CS2029  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  Per informazioni dettagliate, vedere [Pagina Compilazione, Progettazione progetti \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp).  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Modificare la proprietà **Non visualizzare avvisi**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [C\# Compiler Errors](../../../csharp/language-reference/compiler-messages/index.md)