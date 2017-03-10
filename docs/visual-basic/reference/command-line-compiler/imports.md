---
title: "/imports (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/imports compiler option [Visual Basic]"
  - "imports compiler option [Visual Basic]"
  - "-imports compiler option [Visual Basic]"
ms.assetid: 9a93fb53-c080-497b-bf9b-441022dbbc39
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# /imports (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Importa gli spazi dei nomi da un assembly specificato.  
  
## Sintassi  
  
```  
/imports:namespaceList  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`namespaceList`|Obbligatorio.  Elenco delimitato da virgole di spazi dei nomi da importare.|  
  
## Note  
 L'opzione `/imports` consente di importare qualsiasi spazio dei nomi definito all'interno del gruppo di file di origine correnti o da qualsiasi assembly cui viene fatto riferimento.  
  
 I membri di uno spazio dei nomi specificato con l'opzione `/imports` sono disponibili per tutti i file di codice sorgente presenti nella compilazione.  L'[Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) consente di utilizzare uno spazio dei nomi in singoli file del codice sorgente.  
  
||  
|-|  
|Per impostare \/imports nell'ambiente di sviluppo integrato di Visual Studio|  
|1.  Selezionare un progetto in **Esplora soluzioni**.  Scegliere **Proprietà** dal menu **Progetto**.  Per ulteriori informazioni, vedere [Introduction to the Project Designer](http://msdn.microsoft.com/it-it/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Riferimenti**.<br />3.  Immettere il nome dello spazio dei nomi nella casella accanto al pulsante **Aggiungi importazione utente**.<br />4.  Fare clic sul pulsante **Aggiungi importazione utente**.|  
  
## Esempio  
 Il codice che segue viene compilato quando si specifica `/imports:system`.  
  
 [!code-vb[VbVbalrCompiler#21](../../../visual-basic/reference/command-line-compiler/codesnippet/visualbasic/imports_1.vb)]  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [References and the Imports Statement](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)