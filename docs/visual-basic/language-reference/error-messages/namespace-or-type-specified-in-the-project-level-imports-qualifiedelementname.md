---
title: "Namespace or type specified in the project-level Imports &#39;&lt;qualifiedelementname&gt;&#39; doesn&#39;t contain any public member or cannot be found | Microsoft Docs"
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
  - "vbc40057"
  - "bc40057"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40057"
ms.assetid: 4ae3506e-2ebe-4ff3-995d-14ac60db5e9f
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Namespace or type specified in the project-level Imports &#39;&lt;qualifiedelementname&gt;&#39; doesn&#39;t contain any public member or cannot be found
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Lo spazio dei nomi o il tipo specificato nelle importazioni '\<nomeelementoqualificato\>' a livello di progetto non contiene alcun membro pubblico o non è definito.Accertarsi che lo spazio dei nomi o il tipo sia definito e contenga almeno un membro pubblicoe che il nome dell'elemento importato non utilizzi alias.  
  
 Una proprietà di importazione di un progetto specifica un elemento contenitore che non può essere trovato o che non definisce alcun membro `Public`.  
  
 Un *elemento contenitore* può essere uno spazio dei nomi, una classe, una struttura, un modulo, un'interfaccia o un'enumerazione  e contiene membri, ad esempio variabili, routine o altri elementi contenitore.  
  
 Lo scopo dell'importazione è consentire al codice di accedere allo spazio dei nomi o ai membri tipo senza doverne fornire il nome completo.  Il progetto potrebbe richiedere inoltre l'aggiunta di un riferimento allo spazio dei nomi o al tipo.  Per ulteriori informazioni, vedere "Containing Elements" in [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
 Se il compilatore non è in grado di trovare l'elemento contenitore specificato, non sarà possibile risolvere i riferimenti in cui viene utilizzato.  Se trova l'elemento ma questo non espone alcun membro `Public`, nessun riferimento avrà esito positivo.  In entrambi i casi è inutile importare l'elemento.  
  
 Utilizzare **Progettazione progetti** per specificare gli elementi da importare.  Utilizzare la sezione **Spazi dei nomi importati** della pagina **Riferimenti**.  È possibile accedere a **Progettazione progetti** facendo doppio clic sull'icona **Progetto** in **Esplora soluzioni**.  
  
 **ID errore:** BC40057  
  
### Per correggere l'errore  
  
1.  Aprire **Progettazione progetti** e passare alla pagina **Riferimento**.  
  
2.  Nella sezione **Spazi dei nomi importati**, verificare che l'elemento contenitore sia accessibile dal progetto.  
  
3.  Verificare che l'elemento contenitore esponga almeno un membro `Public`.  
  
## Vedere anche  
 [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)   
 [Procedura: modificare le proprietà e le impostazioni di configurazione dei progetti](http://msdn.microsoft.com/it-it/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)