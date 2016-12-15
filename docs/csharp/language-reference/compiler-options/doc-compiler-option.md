---
title: "/doc (C# Compiler Options) | Microsoft Docs"
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
  - "FileProperties.BuildAction"
  - "/doc"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "comments, C# code"
  - "XML documentation [C#], comments in source files"
  - "doc compiler option [C#]"
  - "Visual C#, XML documentation for"
  - "-doc compiler option [C#]"
  - "/doc compiler option [C#]"
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /doc (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'opzione **\/doc** consente di inserire commenti per la documentazione in un file XML.  
  
## Sintassi  
  
```  
/doc:file  
```  
  
## Argomenti  
 `file`  
 Rappresenta il file di output per XML, compilato con i commenti presenti nei file di codice sorgente della compilazione.  
  
## Note  
 Nei file di codice sorgente è possibile elaborare e aggiungere al file XML i commenti relativi alla documentazione che precedono quanto segue:  
  
-   Tipi definiti dall'utente quali una [classe](../../../csharp/language-reference/keywords/class.md), un [delegato](../../../csharp/language-reference/keywords/delegate.md) o un'[interfaccia](../../../csharp/language-reference/keywords/interface.md)  
  
-   Membri quali un campo, un [evento](../../../csharp/language-reference/keywords/event.md), una [proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md) o un metodo  
  
 Il primo output inserito nel file XML è quello del file di codice sorgente che contiene Main.  
  
 Per utilizzare il file XML generato con la funzionalità [IntelliSense](/visual-studio/ide/using-intellisense), assegnare al file XML lo stesso nome dell'assembly che si desidera supportare, quindi accertarsi che il file XML si trovi nella stessa directory dell'assembly.  In questo modo quando si farà riferimento all'assembly nel progetto Visual Studio, verrà trovato anche il file XML.  Per ulteriori informazioni, vedere [Commenti al codice](/visual-studio/ide/supplying-xml-code-comments).  
  
 Se non si esegue la compilazione con [\/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), `file` conterrà tag \<assembly\>\<\/assembly\> che specificano il nome del file contenente il manifesto assembly per il file di output della compilazione.  
  
> [!NOTE]
>  L'opzione \/doc può essere utilizzata per tutti i file di input o, se definita in Impostazioni progetto, per tutti i file di un progetto.  Per disabilitare la visualizzazione degli avvisi relativi ai commenti di documentazione per una sezione di codice o un file specifico, utilizzare [\#pragma warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md).  
  
 Per informazioni sulla generazione di documentazione da commenti presenti nel codice, vedere [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md).  
  
### Per impostare l'opzione del compilatore nell'ambiente di sviluppo di Visual Studio  
  
1.  Aprire la pagina **Proprietà** del progetto.  
  
2.  Fare clic sulla scheda **Compila**.  
  
3.  Modificare la proprietà **File di documentazione XML**.  
  
 Per informazioni su come impostare questa opzione del compilatore a livello di codice, vedere <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>.  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)