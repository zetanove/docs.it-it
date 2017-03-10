---
title: "Type &#39;&lt;typename&gt;&#39; is not defined | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30002"
  - "bc30002"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30002"
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Type &#39;&lt;typename&gt;&#39; is not defined
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'istruzione ha fatto riferimento a un tipo non definito.  È possibile definire un tipo in un'istruzione di dichiarazione quale ad esempio `Enum`, `Structure`, `Class` o `Interface`.  
  
 **ID errore:** BC30002  
  
### Per correggere l'errore  
  
-   Assicurarsi che la definizione del tipo e il relativo riferimento utilizzino entrambi la stessa ortografia.  
  
-   Assicurarsi che la definizione del tipo sia accessibile al riferimento.  Se il tipo è un altro modulo ed è stato dichiarato `Private`, ad esempio, spostare la definizione del tipo al modulo di riferimento oppure dichiararlo `Public`.  
  
-   Assicurarsi che lo spazio dei nomi del tipo non sia ridefinito all'interno del progetto.  Se è ridefinito, utilizzare la parola chiave `Global` per specificare il nome completo del tipo.  Ad esempio, se un progetto definisce lo spazio dei nomi `System`, è impossibile accedere al tipo <xref:System.Object?displayProperty=fullName> a meno che non venga specificato il nome completo con la parola chiave `Global`: `Global.System.Object`.  
  
-   Se il tipo è definito ma la libreria di oggetti o dei tipi in cui è definito non è registrata in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], scegliere **Aggiungi riferimento** dal menu **Progetto**, quindi selezionare la libreria di oggetti o dei tipi appropriata.  
  
-   Assicurarsi che il tipo sia contenuto in un assembly che fa parte del profilo di .NET Framework di destinazione.  Per ulteriori informazioni, vedere [Troubleshooting .NET Framework Targeting Errors](/visual-studio/msbuild/troubleshooting-dotnet-framework-targeting-errors).  
  
## Vedere anche  
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Enum Statement](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Gestione dei riferimenti in un progetto](/visual-studio/ide/managing-references-in-a-project)