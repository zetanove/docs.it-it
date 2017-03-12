---
title: "How to: Create XML Documentation in Visual Basic | Microsoft Docs"
ms.custom: ""
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
  - "XML comments"
  - "XML documentation, creating"
ms.assetid: 27b5b06c-09b9-496a-8245-f9542d846230
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# How to: Create XML Documentation in Visual Basic
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questo esempio viene illustrato come aggiungere al codice commenti relativi alla documentazione XLM.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per creare la documentazione XML per un tipo o un membro  
  
1.  Nell'**editor di codice** posizionare il cursore sulla riga al di sopra del tipo o del membro per cui si desidera creare la documentazione.  
  
2.  Digitare `'''` \(tre virgolette singole\).  
  
     Uno scheletro XML per il tipo o il membro viene aggiunto all'**editor di codice**.  
  
3.  Aggiungere le informazioni descrittive tra i tag appropriati.  
  
    > [!NOTE]
    >  Se si aggiungono altre righe all'interno del blocco di documentazione XML, ogni riga deve iniziare con `'''`.  
  
4.  Aggiungere ulteriore codice che utilizza il tipo o il membro con i nuovi commenti relativi alla documentazione XML.  
  
     IntelliSense visualizza il testo dal tag \<summary\> relativo al tipo o al membro.  
  
5.  Compilare il codice per generare un file XML contenente i commenti relativi alla documentazione.  Per ulteriori informazioni, vedere [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md).  
  
## Vedere anche  
 [Documenting Your Code with XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)   
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)   
 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md)