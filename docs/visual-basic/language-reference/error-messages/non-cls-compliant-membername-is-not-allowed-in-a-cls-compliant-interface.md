---
title: "Non-CLS-compliant &lt;membername&gt; is not allowed in a CLS-compliant interface | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc40033"
  - "vbc40033"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40033"
ms.assetid: 060c4b08-798e-40f1-94cf-c05c524f1b8a
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Non-CLS-compliant &lt;membername&gt; is not allowed in a CLS-compliant interface
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una proprietà, una routine o un evento in un'interfaccia viene contrassegnato come `<CLSCompliant(True)>` quando l'interfaccia stessa è contrassegnata come `<CLSCompliant(False)>` o non è contrassegnata.  
  
 Perché l'interfaccia sia conforme con [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), è necessario che siano conformi tutti i suoi membri.  
  
 Quando si applica l'<xref:System.CLSCompliantAttribute> a un elemento di programmazione, il parametro `isCompliant` dell'attributo viene impostato su `True` o `False` per indicare la compatibilità o la non compatibilità.  L'impostazione predefinita per questo parametro non è disponibile, è necessario quindi specificare un valore.  
  
 Se <xref:System.CLSCompliantAttribute> non viene applicato a un elemento, l'elemento non sarà considerato conforme.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40033  
  
### Per correggere l'errore  
  
-   Se è richiesta la conformità con CLS ed è possibile accedere al codice sorgente dell'interfaccia, contrassegnare l'interfaccia come `<CLSCompliant(True)>` se tutti i membri sono conformi.  
  
-   Se è richiesta la conformità con CLS e non è possibile accedere al codice sorgente dell'interfaccia, o se esso non può essere conforme, definire il membro all'interno di un'interfaccia differente.  
  
-   Se è necessario mantenere il membro nell'interfaccia corrente, rimuovere <xref:System.CLSCompliantAttribute> dalla relativa definizione o contrassegnarlo come `<CLSCompliant(False)>`.  
  
## Vedere anche  
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)