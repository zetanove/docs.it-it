---
title: "&#39;&lt;membername&gt;&#39; cannot expose type &#39;&lt;typename&gt;&#39; outside the project through &lt;containertype&gt; &#39;&lt;containertypename&gt;&#39; | Microsoft Docs"
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
  - "bc30909"
  - "vbc30909"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30909"
ms.assetid: ffa7395d-e182-4087-8ce8-079810fdae54
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;&lt;membername&gt;&#39; cannot expose type &#39;&lt;typename&gt;&#39; outside the project through &lt;containertype&gt; &#39;&lt;containertypename&gt;&#39;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una variabile, un parametro di routine o un valore restituito da una funzione è esposto all'esterno di un contenitore ma è dichiarato come tipo da non esporre all'esterno di un contenitore.  
  
 Nello schema di codice seguente viene illustrata una situazione in cui viene generato questo errore.  
  
```  
Private Class privateClass  
End Class  
Public Class mainClass  
    Public exposedVar As New privateClass  
End Class  
```  
  
 Un tipo dichiarato `Protected`, `Friend`, `Protected Friend` o `Private` deve disporre di un accesso limitato all'esterno del relativo contesto di dichiarazione.  Se questo tipo venisse utilizzato come tipo di dati di una variabile che dispone di autorizzazioni di accesso meno limitate, non potrebbe essere eseguito come da dichiarazione.  Nello schema di codice precedente, `exposedVar` è `Public` ed espone `privateClass` nel codice che non può accedervi.  
  
 **ID errore:** BC30909  
  
### Per correggere l'errore  
  
-   Modificare il livello di accesso della variabile, del parametro di routine o del valore restituito dalla funzione in modo che presenti gli stessi limiti del livello di accesso del relativo tipo di dati.  
  
## Vedere anche  
 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)