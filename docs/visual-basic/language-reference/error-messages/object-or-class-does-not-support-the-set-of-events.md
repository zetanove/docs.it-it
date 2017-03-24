---
title: "Object or class does not support the set of events | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID459"
dev_langs: 
  - "VB"
ms.assetid: 785df3f3-2aae-4a25-af36-1f9879d4e5fd
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Object or class does not support the set of events
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Si è tentato di utilizzare una variabile `WithEvents` con un componente che non può fungere da origine per l'insieme di eventi specificato.  Scopo dell'operazione era effettuare il sink degli eventi di un oggetto e quindi creare un altro oggetto che eseguisse `Implements` sul primo.  È opportuno tenere presente che non è sempre possibile effettuare il sink degli eventi dall'oggetto implementato.  `Implements` implementa solo un'interfaccia per metodi e proprietà.  `WithEvents` non è supportato per l'oggetto `UserControls` privato, perché le informazioni sui tipi necessarie per generare l'oggetto `ObjectEvent` non sono disponibili in fase di esecuzione.  
  
### Per correggere l'errore  
  
1.  Non è possibile effettuare il sink di eventi per un componente che non sia l'origine degli eventi.  
  
## Vedere anche  
 [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)   
 [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md)