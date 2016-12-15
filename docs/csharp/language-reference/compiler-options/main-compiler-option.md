---
title: "/main (C# Compiler Options) | Microsoft Docs"
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
  - "/main"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-main compiler option [C#]"
  - "main compiler option [C#]"
  - "/main compiler option [C#]"
ms.assetid: 975cf4d5-36ac-4530-826c-4aad0c7f2049
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /main (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Questa opzione consente di specificare la classe che contiene il punto di ingresso al programma, quando più classi contengono un metodo **Main**.  
  
## Sintassi  
  
```  
/main:class  
```  
  
## Argomenti  
 `class`  
 Rappresenta il tipo contenente il metodo **Main**.  
  
## Note  
 Se la compilazione include più tipi con un metodo [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md), sarà possibile specificare il tipo che contiene il metodo **Main** che si desidera utilizzare come punto di ingresso nel programma.  
  
 Utilizzare questa opzione solo durante la compilazione di un file EXE.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla pagina delle proprietà **Applicazione**.  
  
3.  Modificare la proprietà **Oggetto di avvio**.  
  
     Per impostare l'opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.ProjectProperties3.StartupObject%2A>.  
  
## Esempio  
 Compilare `t2.cs` e `t3.cs`, specificando che il metodo **Main** si trova in `Test2`:  
  
```  
csc t2.cs t3.cs /main:Test2  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)