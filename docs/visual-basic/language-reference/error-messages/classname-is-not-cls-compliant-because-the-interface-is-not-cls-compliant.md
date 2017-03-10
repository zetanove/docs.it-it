---
title: "&#39;&lt;classname&gt;&#39; is not CLS-compliant because the interface &#39;&lt;interfacename&gt;&#39; it implements is not CLS-compliant | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc40029"
  - "vbc40029"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40029"
ms.assetid: 178452f3-5575-4da0-9d6c-53bcddb6a338
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# &#39;&lt;classname&gt;&#39; is not CLS-compliant because the interface &#39;&lt;interfacename&gt;&#39; it implements is not CLS-compliant
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una classe o un'interfaccia viene contrassegnata come `<CLSCompliant(True)>` quando deriva o implementa un tipo contrassegnato come `<CLSCompliant(False)>` o non contrassegnato.  
  
 Una classe o un'interfaccia è conforme con [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\) se lo è anche la relativa gerarchia di ereditarietà.  Di conseguenza, anche ogni tipo da cui la classe o l'interfaccia eredita, direttamente o indirettamente, deve essere conforme.  In modo simile, se una classe implementa una o più interfacce, tutte le relative gerarchie di ereditarietà devono essere conformi.  
  
 Quando si applica l'<xref:System.CLSCompliantAttribute> a un elemento di programmazione, il parametro `isCompliant` dell'attributo viene impostato su `True` o `False` per indicare la compatibilità o la non compatibilità.  L'impostazione predefinita per questo parametro non è disponibile, è necessario quindi specificare un valore.  
  
 Se <xref:System.CLSCompliantAttribute> non viene applicato a un elemento, l'elemento non sarà considerato conforme.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40029  
  
### Per correggere l'errore  
  
-   Se è necessaria la conformità con CLS, definire il tipo in una diversa gerarchia di ereditarietà o in un diverso schema di implementazione.  
  
-   Se questo tipo deve rimanere nella gerarchia di ereditarietà o nello schema di implementazione corrente, rimuovere l'attributo <xref:System.CLSCompliantAttribute> dalla definizione o contrassegnarlo come `<CLSCompliant(False)>`.  
  
## Vedere anche  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)