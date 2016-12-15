---
title: "/checked (C# Compiler Options) | Microsoft Docs"
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
  - "/checked"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "checked compiler option [C#]"
  - "-checked compiler option [C#]"
  - "/checked compiler option [C#]"
ms.assetid: fb7475d3-e6a6-4e6d-b86c-69e7a74c854b
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /checked (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/checked** consente di specificare se un'istruzione di calcolo su interi che genera un valore non compreso nell'intervallo del tipo di dati e che non è inclusa nell'ambito di una parola chiave [checked](../../../csharp/language-reference/keywords/checked.md) o [unchecked](../../../csharp/language-reference/keywords/unchecked.md), causerà un'eccezione in fase di esecuzione.  
  
## Sintassi  
  
```  
/checked[+ | -]  
```  
  
## Note  
 L'opzione **\/checked** non influisce su un'istruzione di calcolo su interi inclusa nell'ambito di una parola chiave `checked` o `unchecked`.  
  
 Se un'istruzione di calcolo su interi non inclusa nell'ambito di una parola chiave `checked` o `unchecked` genera un valore non compreso nell'intervallo del tipo di dati e nella compilazione viene utilizzata l'opzione **\/checked\+** \(**\/checked**\), verrà generata un'eccezione in fase di esecuzione.  Se nella compilazione viene utilizzata l'opzione **\/checked\-**, l'istruzione non genererà eccezioni in fase di esecuzione.  
  
 Il valore predefinito dell'opzione è **\/checked\-**.  Uno scenario per l'utilizzo di **\/checked\-** è la compilazione di applicazioni di grandi dimensioni.  Gli strumenti automatizzati vengono talvolta utilizzati per compilare tali applicazioni e tale strumento potrebbe automaticamente impostare **\/checked** su \+.  È possibile eseguire l'override del valore predefinito globale dello strumento specificando **\/checked\-**.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  Per ulteriori informazioni, vedere [Pagina Compilazione, Progettazione progetti \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp).  
  
2.  Fare clic sulla pagina delle proprietà **Compila**.  
  
3.  Fare clic sul pulsante **Avanzate**.  
  
4.  Modificare la proprietà **Controlla overflow\/underflow aritmetico**.  
  
 Per accedere all'opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.CheckForOverflowUnderflow%2A>.  
  
## Esempio  
 Il seguente comando viene utilizzato per compilare `t2.cs`.  L'utilizzo di `/checked` nel comando specifica che un'istruzione di calcolo su numeri interi nel file non inclusa nell'ambito di una parola chiave `checked` o `unchecked` e che genera un valore non compreso nell'intervallo del tipo di dati causa un'eccezione in fase di esecuzione.  
  
```  
csc t2.cs /checked  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7)