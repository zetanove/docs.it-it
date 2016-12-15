---
title: "/define (C# Compiler Options) | Microsoft Docs"
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
  - "/define"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-define compiler option [C#]"
  - "/define compiler option [C#]"
  - "-d compiler option [C#]"
  - "define compiler option [C#]"
  - "/d compiler option [C#]"
  - "d compiler option [C#]"
ms.assetid: f17d7b4d-82d0-4133-8563-68cced1cac6e
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /define (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/define** definisce `name` come simbolo in tutti i file di codice sorgente del programma.  
  
## Sintassi  
  
```  
/define:name[;name2]  
```  
  
## Argomenti  
 `name`, `name2`  
 Rappresentano i nomi di uno o più simboli che si desidera definire.  
  
## Note  
 L'opzione **\/define** ha lo stesso effetto dell'utilizzo di una direttiva del preprocessore [\#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) con la differenza che l'opzione del compilatore si applica a tutti i file nel progetto.  Un simbolo resta definito in un file d'origine fino a quando una direttiva [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md) nel file d'origine non rimuove la definizione.  Quando si utilizza l'opzione \/define, una direttiva `#undef`in un file non ha effetto sugli altri file di codice sorgente nel progetto.  
  
 È possibile utilizzare i simboli creati mediante questa opzione con [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md), [\#else](../../../csharp/language-reference/preprocessor-directives/preprocessor-else.md), [\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md) ed [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md) per effettuare la compilazione condizionale dei file di origine.  
  
 **\/d** rappresenta la versione abbreviata di **\/define**.  
  
 È possibile definire più simboli mediante **\/define** utilizzando un punto e virgola \(;\) o una virgola \(,\) come separatori dei nomi di simbolo.  Di seguito è riportato un esempio:  
  
```  
/define:DEBUG;TUESDAY  
```  
  
 Il compilatore C\# non definisce di per sé simboli o macro utilizzabili nel codice sorgente. Tutte le definizioni dei simboli devono essere definite dall'utente.  
  
> [!NOTE]
>  L'opzione C\# `#define` non consente di assegnare un valore a un simbolo, in modo analogo a quanto si verifica in altri linguaggi, quale C\+\+.  Non è ad esempio possibile utilizzare l'opzione `#define` per la creazione di una macro o la definizione di una costante.  Se è necessario definire una costante, utilizzare una variabile `enum`.  Per creare una macro di stile, è possibile avvalersi delle alternative disponibili, ad esempio i generics.  Poiché le macro sono notoriamente soggette a errori, C\# non ne consente l'uso ma fornisce alternative più sicure.  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Nella scheda **Compila** digitare il simbolo da definire nella casella **Simboli di compilazione condizionale**.  Ad esempio, se si utilizza l'esempio di codice che segue, digitare `xx` nella casella di testo.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DefineConstants%2A>.  
  
## Esempio  
  
```  
// preprocessor_define.cs  
// compile with: /define:xx  
// or uncomment the next line  
// #define xx  
using System;  
public class Test   
{  
    public static void Main()   
    {  
        #if (xx)   
            Console.WriteLine("xx defined");  
        #else  
            Console.WriteLine("xx not defined");  
        #endif  
    }  
}  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)