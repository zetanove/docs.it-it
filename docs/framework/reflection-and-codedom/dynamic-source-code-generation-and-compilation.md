---
title: "Dynamic Source Code Generation and Compilation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Code Document Object Model"
  - "System.CodeDom namespace"
  - "language-independent source code modeling"
  - "CodeDOM"
  - "multiple languages supported by CodeDOM"
  - "source code in multiple languages"
  - "languages, multiple language support by CodeDOM"
ms.assetid: d077a3e8-bd81-4bdf-b6a3-323857ea30fb
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Dynamic Source Code Generation and Compilation
In .NET Framework è incluso un meccanismo denominato Code Document Object Model \(CodeDOM\) che consente agli sviluppatori di programmi che creano codice sorgente di generare codice sorgente in più linguaggi di programmazione in fase di esecuzione, in base a un unico modello che rappresenta il codice da generare.  
  
 Per rappresentare il codice sorgente, gli elementi CodeDOM vengono collegati l'un l'altro a formare una struttura di dati nota come grafico CodeDOM, che rappresenta la struttura del codice sorgente.  
  
 Nello spazio dei nomi `System.CodeDom` vengono definiti tipi che possono rappresentare la struttura logica del codice sorgente, indipendentemente da uno specifico linguaggio di programmazione.  Nello spazio dei nomi `System.CodeDom.Compiler` sono definiti i tipi per la generazione di codice sorgente da grafici CodeDOM e per la gestione della compilazione del codice sorgente nei linguaggi supportati.  I produttori di compilatori e gli sviluppatori possono ampliare l'insieme dei linguaggi supportati.  
  
 La modellazione di codice sorgente svincolata da uno specifico linguaggio si rivela particolarmente utile quando occorre che un programma generi codice sorgente per un modello di programma in più linguaggi o in un linguaggio di destinazione non ancora definito.  Alcuni progettisti utilizzano ad esempio CodeDOM come interfaccia indipendente dal linguaggio per produrre codice sorgente nel linguaggio di programmazione desiderato, ove sia disponibile il supporto CodeDOM per tale linguaggio.  
  
 Con .NET Framework vengono forniti compilatori di codice e generatori di codice per i seguenti linguaggi: [C\#](frlrfMicrosoftCSharpCSharpCodeProviderClassTopic), [JScript](frlrfMicrosoftJScriptJScriptCodeProviderClassTopic) e [Visual Basic](frlrfMicrosoftVisualBasicVBCodeProviderClassTopic).  
  
## In questa sezione  
 [Utilizzo di CodeDOM](../../../docs/framework/reflection-and-codedom/using-the-codedom.md)  
 Vengono descritti gli utilizzi comuni e viene illustrata la compilazione di un semplice grafico di oggetti con CodeDOM.  
  
 [Generazione di codice sorgente e compilazione di un programma a partire da un grafico CodeDOM](../../../docs/framework/reflection-and-codedom/generating-and-compiling-source-code-from-a-codedom-graph.md)  
 Viene illustrato come generare codice sorgente e compilare il codice generato con un compilatore esterno utilizzando le classi definite nello spazio dei nomi `System.CodeDom.Compiler`.  
  
 [How to: Create an XML Documentation File Using CodeDOM](../../../docs/framework/reflection-and-codedom/how-to-create-an-xml-documentation-file-using-codedom.md)  
 Viene illustrato come utilizzare CodeDOM per generare codice con commenti di documentazione XML e compilare il codice generato in modo che venga creato l'output di tale documentazione.  
  
 [How to: Create a Class Using CodeDOM](../../../docs/framework/reflection-and-codedom/how-to-create-a-class-using-codedom.md)  
 Viene illustrato come utilizzare CodeDOM per generare una classe contenente campi, proprietà, un metodo, un costruttore e un punto di ingresso.  
  
## Riferimenti  
 <xref:System.CodeDom>  
 Definisce elementi che rappresentano elementi di codice in linguaggi di programmazione che si avvalgono del Common Language Runtime.  
  
 <xref:System.CodeDom.Compiler>  
 Vengono descritte le interfacce per la generazione e la compilazione di codice in fase di esecuzione.  
  
## Sezioni correlate  
 [CodeDOM Quick Reference](http://msdn.microsoft.com/it-it/c77b8bfd-0a32-4e36-b59a-4f687f32c524)  
 Viene fornito agli sviluppatori un modo rapido per cercare elementi CodeDOM che rappresentano elementi del codice sorgente.