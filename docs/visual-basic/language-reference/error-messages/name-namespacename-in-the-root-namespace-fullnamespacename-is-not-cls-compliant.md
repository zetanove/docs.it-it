---
title: "Name &lt;namespacename&gt; in the root namespace &lt;fullnamespacename&gt; is not CLS-compliant | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc40039"
  - "bc40039"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40039"
ms.assetid: c5bd5914-ae71-416a-8bed-f76f644f78be
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Name &lt;namespacename&gt; in the root namespace &lt;fullnamespacename&gt; is not CLS-compliant
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un assembly viene contrassegnato come `<CLSCompliant(True)>`, ma un elemento del nome dello spazio dei nomi principale inizia con un carattere di sottolineatura \(`_`\).  
  
 In un elemento di programmazione possono essere presenti uno o più caratteri di sottolineatura, ma per la compatibilità con [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), non può iniziare con un segno di sottolineatura.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
 Quando si applica l'<xref:System.CLSCompliantAttribute> a un elemento di programmazione, il parametro `isCompliant` dell'attributo viene impostato su `True` o `False` per indicare la compatibilità o la non compatibilità.  L'impostazione predefinita per questo parametro non è disponibile, è necessario quindi specificare un valore.  
  
 Se <xref:System.CLSCompliantAttribute> non viene applicato a un elemento, l'elemento non sarà considerato conforme.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso.  Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40039  
  
### Per correggere l'errore  
  
-   Se è richiesta la compatibilità con CLS, modificare il nome dello spazio dei nomi principale in modo che nessuno dei suoi elementi inizi con un segno di sottolineatura.  
  
-   Se il nome dello spazio dei nomi deve rimanere invariato, rimuovere l'<xref:System.CLSCompliantAttribute> dall'assembly o contrassegnarlo come `<CLSCompliant(False)>`.  
  
## Vedere anche  
 [Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [\/rootnamespace](../../../visual-basic/reference/command-line-compiler/rootnamespace.md)   
 [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)   
 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Visual Basic Naming Conventions](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/it-it/4c705105-69a2-4e5e-b24e-0633bc32c7f3)