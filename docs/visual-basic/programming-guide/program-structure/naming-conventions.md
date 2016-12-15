---
title: "Visual Basic Naming Conventions | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "names, Visual Basic rules"
  - "naming conventions"
  - "naming conventions, Visual Basic"
  - "Visual Basic code, naming conventions"
  - "conventions, Visual Basic coding"
  - "names, naming conventions"
  - "naming conventions, classes"
ms.assetid: 164949a4-2a7c-4736-9d82-9c3078e2e56c
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic Naming Conventions
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

I nomi assegnati agli elementi nell'applicazione Visual Basic devono iniziare con un carattere alfabetico o un carattere di sottolineatura.  Tenere conto che i nomi che iniziano con un carattere di sottolineatura non sono conformi con [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\).  
  
 Per le operazioni di denominazione, tenere presenti i seguenti suggerimenti.  
  
-   L'iniziale di ciascuna parola che compone il nome deve essere scritta in maiuscolo, ad esempio `FindLastRecord` e `RedrawMyForm`.  
  
-   I nomi di funzioni e metodi devono iniziare con un verbo, ad esempio `InitNameArray` o `CloseDialog`.  
  
-   I nomi di classi, strutture, moduli e proprietà devono iniziare con un sostantivo, ad esempio `EmployeeName` o `CarAccessory`.  
  
-   I nomi di interfacce devono iniziare con il prefisso "I" seguito da un nome o da una locuzione nominale, come `IComponent`, oppure con un aggettivo che descrive il comportamento dell'interfaccia, ad esempio `IPersistable`.  Non utilizzare il carattere di sottolineatura ed evitare il più possibile le abbreviazioni, in quanto possono essere fonte di confusione e malintesi.  
  
-   I nomi dei gestori di eventi devono iniziare con un nome che descrive il tipo di evento, seguito dal suffisso "`EventHandler`", ad esempio "`MouseEventHandler`".  
  
-   Il nome delle classi di argomenti di eventi deve includere il suffisso "`EventArgs`".  
  
-   Se un evento ha insito un concetto di "prima" o "dopo", utilizzare un suffisso al presente o al passato, come in "`ControlAdd`" o "`ControlAdded`".  
  
-   Per i termini lunghi o di uso frequente, ricorrere alle abbreviazioni per contenere la lunghezza del nome, ad esempio "HTML" anziché "Hyper\-Text Markup Language".  In generale, i nomi di variabili che contengono più di 32 caratteri sono difficili da leggere su un monitor a bassa risoluzione.  Assicurarsi inoltre che le abbreviazioni siano utilizzate in modo uniforme in tutta l'applicazione.  L'utilizzo alternato delle diciture "HTML" e "Hyper\-Text Markup Language" all'interno di un progetto può creare ambiguità.  
  
-   Evitare di utilizzare in un ambito interno nomi uguali a quelli utilizzati in un ambito esterno.  In caso di accesso alla variabile sbagliata, possono essere generati degli errori.  Se si verifica un conflitto tra una variabile e la parola chiave con lo stesso nome, è necessario identificare la parola chiave anteponendovi la libreria di tipi appropriata.  Per una variabile denominata `Date`, è possibile utilizzare la funzione intrinseca `Date` solo chiamando <xref:System.DateTime.Date%2A?displayProperty=fullName>.  
  
## Vedere anche  
 [Keywords as Element Names in Code](../../../visual-basic/programming-guide/program-structure/keywords-as-element-names-in-code.md)   
 [Me, My, MyBase, and MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Visual Basic Language Reference](../../../visual-basic/language-reference/index.md)