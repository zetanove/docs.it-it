---
title: "Differences Between Shadowing and Overriding (Visual Basic) | Microsoft Docs"
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
  - "shadowing, vs. overriding"
  - "overriding, vs. shadowing"
ms.assetid: 2d014a0b-7630-407d-8f4e-24bd87987923
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Differences Between Shadowing and Overriding (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando si definisce una classe che eredita da una classe base, talvolta è necessario ridefinire uno o più elementi della classe base nella classe derivata.  A questo scopo è possibile utilizzare sia lo shadowing che l'override.  
  
## Confronto  
 Sia lo shadowing che l'override vengono utilizzati quando una classe derivata eredita da una classe di base ed entrambi consentono di ridefinire un elemento dichiarato con un altro.  Esistono tuttavia differenze significative tra queste due tecniche.  
  
 Nella seguente tabella vengono illustrate le differenze tra lo shadowing e l'override.  
  
||||  
|-|-|-|  
|Elemento di confronto|Shadowing|Override|  
|Scopo|Impedisce le successive modifiche della classe base che introducono un membro già definito nella classe derivata|Applica il polimorfismo mediante la definizione di una diversa implementazione di una routine o di una proprietà con la stessa sequenza di chiamata<sup>1</sup>|  
|Elemento ridefinito|Qualsiasi tipo di elemento dichiarato|Solo una routine \(`Function`, `Sub` o `Operator`\) o una proprietà|  
|Elemento di ridefinizione|Qualsiasi tipo di elemento dichiarato|Solo una routine o una proprietà con identica sequenza di chiamata<sup>1</sup>|  
|Livello di accesso dell'elemento di ridefinizione|Qualsiasi livello di accesso|Non è possibile modificare il livello di accesso dell'elemento sottoposto a override|  
|Leggibilità dell'elemento di ridefinizione e possibilità di apportarvi modifiche|Qualsiasi combinazione|Impossibile modificare la leggibilità o la scrivibilità della proprietà sottoposta a override|  
|Controllo sulla ridefinizione|L'elemento della classe base non può applicare o impedire lo shadowing|L'elemento della classe base può specificare `MustOverride`, `NotOverridable` o `Overridable`|  
|Utilizzo di parole chiave|`Shadows` consigliata nella classe derivata; si presuppone `Shadows` se non vengono specificate né `Shadows` né `Overrides`<sup>2</sup>|`Overridable` o `MustOverride` obbligatoria nella classe base; `Overrides` obbligatoria nella classe derivata|  
|Eredità dell'elemento di ridefinizione da parte di classi che derivano dalla classe derivata|Elemento di shadowing ereditato da altre classi derivate; elemento su cui viene eseguito lo shadowing ancora nascosto<sup>3</sup>|Elemento di override ereditato da altre classi derivate; elemento su cui viene eseguito l'override ancora in override|  
  
 <sup>1</sup> La *sequenza di chiamata* è costituita da tipo di elemento \(`Function`, `Sub`, `Operator` o `Property`\), nome, elenco dei parametri e tipo restituito.  Non è possibile eseguire l'override di una routine con una proprietà o viceversa.  Non è possibile eseguire l'override di un tipo di routine \(`Function`, `Sub` o `Operator`\) con un altro tipo.  
  
 <sup>2</sup> Se non si specifica `Shadows` o `Overrides`, il compilatore restituisce un messaggio di avviso in cui viene chiesto di verificare il tipo di ridefinizione che si desidera utilizzare.  Se si ignora il messaggio di avviso, verrà utilizzato il meccanismo di shadowing.  
  
 <sup>3</sup> Se l'elemento di shadowing non risulta accessibile nelle altre classi derivate, lo shadowing non verrà ereditato.  Se ad esempio si dichiara l'elemento di shadowing come `Private`, una classe che deriva dalla classe derivata erediterà l'elemento originale anziché l'elemento di shadowing.  
  
## Indicazioni  
 L'override deve essere in genere utilizzato nei seguenti casi:  
  
-   Durante la definizione di classi derivate polimorfiche.  
  
-   Quando si desidera che il compilatore imponga la stessa sequenza di chiamata e lo stesso tipo di elemento.  
  
 Lo shadowing deve essere in genere utilizzato nei seguenti casi:  
  
-   Quando si prevede che la classe base possa essere modificata e si desidera definire un elemento utilizzando lo stesso nome.  
  
-   Quando si desidera avere la possibilità di modificare il tipo di elemento o la sequenza di chiamata.  
  
## Vedere anche  
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Shadowing in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [How to: Hide a Variable with the Same Name as Your Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)   
 [How to: Hide an Inherited Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)   
 [How to: Access a Variable Hidden by a Derived Class](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)