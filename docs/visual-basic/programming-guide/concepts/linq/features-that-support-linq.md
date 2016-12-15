---
title: "Visual Basic Features That Support LINQ | Microsoft Docs"
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
  - "Visual Basic, LINQ features"
  - "LINQ [Visual Basic], features supporting LINQ"
ms.assetid: c821bb50-b6f6-4cf9-8aba-2717e465bd3a
caps.latest.revision: 51
caps.handback.revision: 49
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Visual Basic Features That Support LINQ
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Il nome [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] si riferisce alla tecnologia in Visual Basic che supporta la sintassi della query e gli altri costrutti di linguaggio direttamente nel linguaggio.  Con [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] non è necessario imparare un nuovo linguaggio per eseguire una query su un'origine dati esterna.  È possibile eseguire una query sui dati presenti in database relazionali, archivi XML o oggetti utilizzando Visual Basic.  Questa integrazione delle funzionalità di query nel linguaggio consente il controllo degli errori di sintassi e dell'indipendenza dai tipi in fase di compilazione.  Questa integrazione fornisce inoltre tutte le informazioni necessarie per poter scrivere query complesse in Visual Basic.  
  
 Nelle sezioni seguenti vengono illustrati dettagliatamente i costrutti di linguaggio che supportano LINQ per poter iniziare a leggere la documentazione introduttiva, gli esempi di codice e le applicazioni di esempio.  È inoltre possibile fare clic sui collegamenti per spiegazioni più dettagliate sulle funzionalità del linguaggio per consentire l'utilizzo di Language Integrated Query.  Si consiglia di iniziare da [Procedura dettagliata: Scrittura delle query in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md).  
  
## Espressioni di query  
 Le espressioni di query in Visual Basic possono essere definite in una sintassi dichiarativa simile a quella di SQL o XQuery.  In fase di compilazione la sintassi della query viene convertita nelle chiamate al metodo per l'implementazione di un provider LINQ dei metodi di estensione degli operatori di query standard.  Le applicazioni controllano gli operatori di query standard inclusi nell'ambito specificando lo spazio dei nomi adatto con un'istruzione `Imports`.  Di seguito è riportato un esempio della sintassi per un'espressione di query Visual Basic:  
  
 [!code-vb[VbLINQVbFeatures#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_1.vb)]  
  
 Per ulteriori informazioni, vedere [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md).  
  
## Variabili tipizzate in modo implicito  
 Anziché specificare in modo esplicito un tipo quando si dichiara e inizializza una variabile, è possibile consentire al compilatore di dedurre e assegnare il tipo.  Questo processo viene definito *inferenza del tipo di variabile locale*.  
  
 Le variabili il cui tipo viene dedotto sono fortemente tipizzate, esattamente come le variabili in cui il tipo viene specificato in modo esplicito.  L'inferenza del tipo di variabile locale funziona solo quando si definisce una variabile locale all'interno del corpo di un metodo.  Per ulteriori informazioni, vedere [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md) e [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
 Nell'esempio seguente viene illustrata l'inferenza del tipo di variabile locale.  Per utilizzare questo esempio, è necessario impostare `Option Infer` su `On`.  
  
 [!code-vb[VbLINQVbFeatures#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_2.vb)]  
  
 L'inferenza del tipo di variabile locale consente inoltre di creare tipi anonimi, descritte più avanti in questa sezione e sono necessari per le query LINQ.  
  
 Nell'esempio di LINQ seguente l'inferenza del tipo si verifica se `Option Infer` è `On` o `Off`.  Se `Option Infer` è `Off` e `Option Strict` è `On` si verifica un errore in fase di compilazione.  
  
 [!code-vb[VbLINQVbFeatures#3](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_3.vb)]  
  
## Inizializzatori di oggetti  
 Gli inizializzatori di oggetto vengono utilizzati nelle espressioni di query quando è necessario creare un tipo anonimo per contenere i risultati di una query.  Possono inoltre essere utilizzati per inizializzare oggetti di tipi denominati all'esterno delle query.  Utilizzando un inizializzatore di oggetto, è possibile inizializzare un oggetto in una sola riga senza una chiamata esplicita a un costruttore.  Se si dispone di una classe denominata `Customer` con le proprietà pubbliche `Name` e `Phone`, insieme alle altre proprietà, l'inizializzatore di oggetto può essere utilizzato in questo modo:  
  
 [!code-vb[VbLINQVbFeatures#4](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_4.vb)]  
  
 Per ulteriori informazioni, vedere [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md).  
  
## Tipi anonimi  
 I tipi anonimi costituiscono una valida soluzione per raggruppare temporaneamente un insieme di proprietà in un elemento che si desidera includere nel risultato di una query.  In questo modo è possibile scegliere qualsiasi combinazione di campi disponibili nella query, in qualsiasi ordine, senza definire un tipo di dati denominato per l'elemento.  
  
 Un *tipo anonimo* viene costruito dinamicamente dal compilatore.  Il nome del tipo viene assegnato dal compilatore e può cambiare a ogni nuova compilazione.  Pertanto, il nome non può essere utilizzato direttamente.  I tipi anonimi vengono inizializzati nel modo seguente:  
  
 [!code-vb[VbLINQVbFeatures#5](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_5.vb)]  
  
 Per ulteriori informazioni, vedere [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
## Metodi di estensione  
 I metodi di estensione consentono di aggiungere metodi a un tipo di dati o a un'interfaccia all'esterno della definizione.  Questa funzionalità consente in pratica di aggiungere nuovi metodi a un tipo esistente senza dovere effettivamente modificare il tipo.  Gli operatori query standard costituiscono un insieme di metodi di estensione che forniscono le funzionalità delle query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] per qualsiasi tipo che implementi <xref:System.Collections.Generic.IEnumerable%601>. Altre estensioni a <xref:System.Collections.Generic.IEnumerable%601> includono <xref:System.Linq.Enumerable.Count%2A>, <xref:System.Linq.Enumerable.Union%2A> e <xref:System.Linq.Enumerable.Intersect%2A>.  
  
 Il metodo di estensione seguente aggiunge un metodo di stampa alla classe <xref:System.String>.  
  
 [!code-vb[VbLINQVbFeatures#6](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_6.vb)]  
  
 Il metodo viene chiamato come metodo di istanza comune di <xref:System.String>:  
  
 [!code-vb[VbLINQVbFeatures#7](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_7.vb)]  
  
 Per ulteriori informazioni, vedere [Metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md).  
  
## Espressioni lambda  
 Una espressione lambda è una funzione senza nome, che calcola e restituisce un singolo valore.  A differenza delle funzioni denominate, un'espressione lambda può essere definita ed eseguita contemporaneamente.  Nell'esempio seguente viene visualizzato 4.  
  
 [!code-vb[VbLINQVbFeatures#8](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_8.vb)]  
  
 È possibile assegnare la definizione dell'espressione lambda a un nome di variabile e utilizzare quindi il nome per chiamare la funzione.  Anche nell'esempio seguente viene visualizzato 4.  
  
 [!code-vb[VbLINQVbFeatures#12](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_9.vb)]  
  
 In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] molti degli operatori di query standard hanno espressioni lambda sottostanti.  Il compilatore crea le espressioni lambda per acquisire i calcoli definiti nei metodi di query fondamentali, ad esempio `Where`, `Select`,`Order By`, `Take While` e altri.  
  
 Ad esempio, nel codice seguente viene definita una query che restituisce tutti gli studenti senior da un elenco di studenti.  
  
 [!code-vb[VbLINQVbFeatures#9](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_10.vb)]  
  
 La definizione della query viene compilata nel codice simile all'esempio seguente che utilizza due espressioni lambda per specificare gli argomenti per `Where` e `Select`.  
  
 [!code-vb[VbLINQVbFeatures#10](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_11.vb)]  
  
 Entrambe le versioni possono essere eseguite utilizzando un ciclo `For Each`:  
  
 [!code-vb[VbLINQVbFeatures#11](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_12.vb)]  
  
 Per ulteriori informazioni, vedere [Lambda Expressions](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
## Vedere anche  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Getting Started with LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [LINQ e stringhe](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [C\# Features That Support LINQ](../../../../csharp/programming-guide/concepts/linq/features-that-support-linq.md)   
 [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)