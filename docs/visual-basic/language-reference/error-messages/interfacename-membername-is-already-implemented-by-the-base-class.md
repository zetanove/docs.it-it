---
title: "&#39;&lt;interfacename&gt;.&lt;membername&gt;&#39; is already implemented by the base class &#39;&lt;baseclassname&gt;&#39;. Re-implementation of &lt;type&gt; assumed | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc42015"
  - "bc42015"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42015"
ms.assetid: 658c070a-113e-4bd8-b294-12c243191160
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# &#39;&lt;interfacename&gt;.&lt;membername&gt;&#39; is already implemented by the base class &#39;&lt;baseclassname&gt;&#39;. Re-implementation of &lt;type&gt; assumed
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una proprietà, una routine o un evento in una classe derivata utilizza una clausola `Implements` che specifica un membro di interfaccia già implementato nella classe base.  
  
 Una classe derivata può reimplementare un membro di interfaccia implementato dalla sua classe base.  Si noti che ciò non ha la stessa funzione dell'esecuzione dell'override dell'implementazione della classe base.  Per ulteriori informazioni, vedere [Implements](../../../visual-basic/language-reference/statements/implements-clause.md).  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42015  
  
### Per correggere l'errore  
  
-   Se si intende reimplementare il membro di interfaccia, non occorre fare nulla.  Grazie al codice presente nella classe derivata è possibile accedere al membro reimplementato se non si utilizza la parola chiave `MyBase` per accedere all'implementazione della classe base.  
  
-   Se non si intende reimplementare il membro di interfaccia, rimuovere la clausola `Implements` dalla proprietà, procedura o dichiarazione di evento.  
  
## Vedere anche  
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)