---
title: "/doc | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "doc compiler option [Visual Basic]"
  - "-doc compiler option [Visual Basic]"
  - "/doc compiler option [Visual Basic]"
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /doc
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Elabora i commenti della documentazione in un file XML.  
  
## Sintassi  
  
```  
/doc[+ | -]  
' -or-  
/doc:file  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`+`  &#124; `-`|Parametro facoltativo.  Se si specifica \+ o semplicemente `/doc`, verranno generate informazioni sulla documentazione che saranno inserite in un file XML.  Specificando `-` si ottiene lo stesso effetto che si ottiene non specificando `/doc`, ovvero non verranno create informazioni sulla documentazione.|  
|`file`|Obbligatorio se viene utilizzato `/doc:`.  Specifica il file XML di output in cui vengono inseriti i commenti presenti nei file di codice sorgente della compilazione.  Se il nome file contiene uno spazio, racchiudere il nome tra virgolette \(" "\).|  
  
## Note  
 L'opzione `/doc` controlla se il compilatore genera un file XML contenente i commenti sulla documentazione.  Se si utilizza la sintassi `/doc:``file`, il parametro `file` specifica il nome del file XML.  Se si utilizza `/doc` o `/doc+`, il nome del file XML corrisponderà a quello del file eseguibile o della libreria creata dal compilatore.  Se si utilizza `/doc-` o non si specifica l'opzione `/doc`, il compilatore non creerà alcun file XML.  
  
 All'interno dei file di codice sorgente i commenti sulla documentazione possono precedere le seguenti definizioni:  
  
-   Tipi definiti dall'utente, ad esempio una [classe](../../../visual-basic/language-reference/statements/class-statement.md) o un'[interfaccia](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
-   Membri quali un campo, un [evento](../../../visual-basic/language-reference/statements/event-statement.md), una [proprietà](../../../visual-basic/language-reference/statements/property-statement.md), una [funzione](../../../visual-basic/language-reference/statements/function-statement.md) o una [subroutine](../../../visual-basic/language-reference/statements/sub-statement.md).  
  
 Per utilizzare il file XML generato con la funzione [IntelliSense](/visual-studio/ide/using-intellisense) di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], fare in modo che il nome del file XML corrisponda all'assembly che si intende supportare.  Assicurarsi che il file XML si trovi nella stessa directory dell'assembly in modo che sia possibile individuarlo quando viene fatto riferimento all'assembly nel progetto di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)].  I file della documentazione XML non sono necessari per l'utilizzo di IntelliSense con il codice all'interno di un progetto o di progetti a cui fa riferimento un progetto.  
  
 A meno che non si esegua la compilazione con `/target:module`, il file XML contiene i tag `<assembly></assembly>`.  Tali tag specificano il nome del file contenente il manifesto assembly per il file di output della compilazione.  
  
 Per informazioni sulla generazione di documentazione da commenti presenti nel codice, vedere [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md).  
  
||  
|-|  
|Per impostare l'opzione \/doc nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Impostare il valore nella casella **Genera il file di documentazione XML**.|  
  
## Esempio  
 Per un esempio, vedere [Documenting Your Code with XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md).  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Documenting Your Code with XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)