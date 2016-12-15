---
title: "Cannot refer to &#39;&lt;name&gt;&#39; because it is a member of the value-typed field &#39;&lt;name&gt;&#39; of class &#39;&lt;classname&gt;&#39; which has &#39;System.MarshalByRefObject&#39; as a base class | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc30310"
  - "bc30310"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30310"
ms.assetid: 2aeb8872-7c87-4f01-98ef-9714ba3eebbe
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Cannot refer to &#39;&lt;name&gt;&#39; because it is a member of the value-typed field &#39;&lt;name&gt;&#39; of class &#39;&lt;classname&gt;&#39; which has &#39;System.MarshalByRefObject&#39; as a base class
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La classe `System.MarshalByRefObject` consente alle applicazioni che supportano l'accesso remoto di accedere a oggetti che si trovano oltre i limiti del dominio applicazione.  I tipi devono ereditare dalla classe `MarshalByRejectObject` quando il tipo viene utilizzato oltre i limiti del dominio applicazione.  Lo stato dell'oggetto non deve essere copiato in quanto i membri dell'oggetto non possono essere utilizzati al di fuori del dominio applicazione in cui sono stati creati.  
  
 **ID errore:** BC30310  
  
### Per correggere l'errore  
  
1.  Controllare il riferimento per assicurarsi che il membro a cui si fa riferimento sia valido.  
  
2.  Qualificare esplicitamente il membro con la parola chiave `Me`.  
  
## Vedere anche  
 <xref:System.MarshalByRefObject>   
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)