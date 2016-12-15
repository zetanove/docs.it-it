---
title: "Namespace or type specified in the Imports &#39;&lt;qualifiedelementname&gt;&#39; doesn&#39;t contain any public member or cannot be found | Microsoft Docs"
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
  - "bc40056"
  - "vbc40056"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40056"
ms.assetid: b59f5754-444f-4378-9272-9678b437e84a
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Namespace or type specified in the Imports &#39;&lt;qualifiedelementname&gt;&#39; doesn&#39;t contain any public member or cannot be found
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Lo spazio dei nomi o il tipo specificato nelle importazioni '\<nomeelementoqualificato\>' non contiene alcun membro pubblico o non è definito.Accertarsi che lo spazio dei nomi o il tipo sia definito e contenga almeno un membro pubblicoe che il nome dell'elemento importato non utilizzi alias.  
  
 Un'istruzione `Imports` specifica un elemento contenitore che non può essere trovato o che non definisce alcun membro `Public`.  
  
 Un *elemento contenitore* può essere uno spazio dei nomi, una classe, una struttura, un modulo, un'interfaccia o un'enumerazione  e contiene membri, ad esempio variabili, routine o altri elementi contenitore.  
  
 Lo scopo dell'importazione è consentire al codice di accedere allo spazio dei nomi o ai membri tipo senza doverne fornire il nome completo.  Il progetto potrebbe richiedere inoltre l'aggiunta di un riferimento allo spazio dei nomi o al tipo.  Per ulteriori informazioni, vedere "Containing Elements" in [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
 Se il compilatore non è in grado di trovare l'elemento contenitore specificato, non sarà possibile risolvere i riferimenti in cui viene utilizzato.  Se trova l'elemento ma questo non espone alcun membro `Public`, nessun riferimento avrà esito positivo.  In entrambi i casi è inutile importare l'elemento.  
  
 Tenere presente che se si importa un elemento contenitore e si assegna a questo un alias di importazione, tale alias non potrà essere utilizzato per importare l'altro elemento.  Il codice seguente genera un errore di compilazione.  
  
 `Imports`   `winfrm`   `= System.Windows.Forms`  
  
 `' The following statement is`   `INVALID`   `because it reuses an import alias.`  
  
 `Imports behav =`   `winfrm`  `.Design.Behavior`  
  
 **ID errore:** BC40056  
  
### Per correggere l'errore  
  
1.  Verificare che l'elemento contenitore sia accessibile dal progetto.  
  
2.  Verificare che la specifica dell'elemento contenitore non includa alias di importazione dall'altra importazione.  
  
3.  Verificare che l'elemento contenitore esponga almeno un membro `Public`.  
  
## Vedere anche  
 [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)