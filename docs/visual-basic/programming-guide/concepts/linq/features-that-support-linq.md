---
title: "Funzionalità di Visual Basic che supportano LINQ | Documenti di Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic, LINQ features
- LINQ [Visual Basic], features supporting LINQ
ms.assetid: c821bb50-b6f6-4cf9-8aba-2717e465bd3a
caps.latest.revision: 51
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3bca15a07a88195589b9c9de5f9842eea42912f1
ms.lasthandoff: 03/13/2017

---
# <a name="visual-basic-features-that-support-linq"></a>Funzionalità di Visual Basic che supportano LINQ
Il nome [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] si riferisce alla tecnologia in Visual Basic che supporta la sintassi della query e altri linguaggio costruisce direttamente nel linguaggio. Con [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], non è necessario imparare un nuovo linguaggio di query su un'origine dati esterna. È possibile eseguire query sui dati in database relazionali, archivi XML o oggetti utilizzando Visual Basic. Questa integrazione delle funzionalità di query nel linguaggio consente il controllo in fase di compilazione per gli errori di sintassi e indipendenza dai tipi. Questa integrazione garantisce inoltre che si conosce già la maggior parte delle informazioni necessarie per poter scrivere query complesse in Visual Basic.  
  
 Nelle sezioni seguenti vengono descritti i costrutti di linguaggio che supportano LINQ informazioni sufficienti per consentire di iniziare a leggere la documentazione introduttiva, esempi di codice e applicazioni di esempio. È inoltre possibile fare clic sui collegamenti per trovare spiegazioni più dettagliate su come le funzionalità del linguaggio si riuniscono per abilitare language integrated query. È un buon punto di partenza [procedura dettagliata: scrittura di query in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md).  
  
## <a name="query-expressions"></a>Espressioni di query  
 Espressioni di query in Visual Basic possono essere espresse in una sintassi dichiarativa simile a quella di SQL o XQuery. In fase di compilazione, la sintassi di query viene convertita in chiamate al metodo di implementazione di un provider LINQ dei metodi di estensione operatore query standard. Le applicazioni controllano gli operatori di query standard sono nell'ambito specificando lo spazio dei nomi appropriato con un `Imports` istruzione. Sintassi per un'espressione di query di Visual Basic è simile al seguente:  
  
 [!code-vb[VbLINQVbFeatures n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_1.vb)]  
  
 Per ulteriori informazioni, vedere [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md).  
  
## <a name="implicitly-typed-variables"></a>Variabili tipizzate implicitamente  
 Anziché specificare in modo esplicito un tipo quando è necessario dichiarare e inizializzare una variabile, è possibile abilitare il compilatore di dedurre e assegnare il tipo. Ciò è detto *inferenza del tipo locale*.  
  
 Le variabili i cui tipi inferiti sono fortemente tipizzate, proprio come le variabili il cui tipo è specificare in modo esplicito. Inferenza del tipo locale funziona solo quando si definisce una variabile locale all'interno di un corpo del metodo. Per ulteriori informazioni, vedere [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md) e [l'inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
 Nell'esempio seguente viene illustrata l'inferenza del tipo locale. Per utilizzare questo esempio, è necessario impostare `Option Infer` a `On`.  
  
 [!code-vb[VbLINQVbFeatures n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_2.vb)]  
  
 Inferenza del tipo locale rende inoltre possibile creare tipi anonimi, che sono descritte più avanti in questa sezione e sono necessari per le query LINQ.  
  
 Nell'esempio seguente di LINQ, l'inferenza del tipo si verifica se `Option Infer` è `On` o `Off`. Si verifica un errore in fase di compilazione se `Option Infer` è `Off` e `Option Strict` è `On`.  
  
 [!code-vb[VbLINQVbFeatures n.&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_3.vb)]  
  
## <a name="object-initializers"></a>Inizializzatori di oggetti  
 Gli inizializzatori di oggetto utilizzati nelle espressioni di query quando è necessario creare un tipo anonimo per contenere i risultati di una query. Inoltre possono essere utilizzati per inizializzare gli oggetti di tipi denominati di fuori di query. Utilizzando un inizializzatore di oggetto, è possibile inizializzare un oggetto in una sola riga senza chiamare in modo esplicito un costruttore. Supponendo che sia presente una classe denominata `Customer` con pubblica `Name` e `Phone` proprietà, insieme ad altre proprietà, un inizializzatore di oggetto può essere utilizzato in questo modo:  
  
 [!code-vb[VbLINQVbFeatures n.&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_4.vb)]  
  
 Per ulteriori informazioni, vedere [gli inizializzatori di oggetto: tipi denominati e anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md).  
  
## <a name="anonymous-types"></a>Tipi anonimi  
 Tipi anonimi offrono un modo pratico per raggruppare temporaneamente un set di proprietà in un elemento che si desidera includere nel risultato di una query. In questo modo è possibile scegliere qualsiasi combinazione di campi disponibili nella query, in qualsiasi ordine, senza definire un tipo di dati denominato per l'elemento.  
  
 Un *tipo anonimo* viene costruito dinamicamente dal compilatore. Il nome del tipo è assegnato dal compilatore e può cambiare a ogni nuova compilazione. Pertanto, il nome non può essere utilizzato direttamente. Tipi anonimi vengono inizializzati nel modo seguente:  
  
 [!code-vb[VbLINQVbFeatures n.&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_5.vb)]  
  
 Per ulteriori informazioni, vedere [tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
## <a name="extension-methods"></a>Metodi di estensione  
 Metodi di estensione consentono di aggiungere metodi a un tipo di dati o un'interfaccia all'esterno la definizione. Questa funzionalità consente di fatto, aggiungere nuovi metodi a un tipo esistente senza modificare il tipo. Gli operatori di query standard sono un set di metodi di estensione che forniscono [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] funzionalità di query per qualsiasi tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>.</xref:System.Collections.Generic.IEnumerable%601> Altre estensioni <xref:System.Collections.Generic.IEnumerable%601>includono <xref:System.Linq.Enumerable.Count%2A>, <xref:System.Linq.Enumerable.Union%2A>e <xref:System.Linq.Enumerable.Intersect%2A>.</xref:System.Linq.Enumerable.Intersect%2A> </xref:System.Linq.Enumerable.Union%2A> </xref:System.Linq.Enumerable.Count%2A> </xref:System.Collections.Generic.IEnumerable%601>  
  
 Il metodo di estensione seguente aggiunge un metodo di stampa per la <xref:System.String>classe.</xref:System.String>  
  
 [!code-vb[6 VbLINQVbFeatures](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_6.vb)]  
  
 Viene chiamato il metodo come metodo di istanza comune di <xref:System.String>:</xref:System.String>  
  
 [!code-vb[VbLINQVbFeatures&#7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_7.vb)]  
  
 Per ulteriori informazioni, vedere [metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md).  
  
## <a name="lambda-expressions"></a>Espressioni lambda  
 Un'espressione lambda è una funzione senza nome, che calcola e restituisce un singolo valore. A differenza delle funzioni denominate, un'espressione lambda può essere definita ed eseguita nello stesso momento. Nell'esempio seguente viene visualizzato 4.  
  
 [!code-vb[VbLINQVbFeatures n.&8;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_8.vb)]  
  
 È possibile assegnare la definizione dell'espressione lambda a un nome di variabile e quindi utilizzare il nome per chiamare la funzione. Nell'esempio seguente viene visualizzato anche 4.  
  
 [!code-vb[VbLINQVbFeatures&#12;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_9.vb)]  
  
 In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], molti degli operatori di query standard hanno espressioni lambda sottostanti. Il compilatore crea le espressioni lambda per acquisire i calcoli definiti nei metodi di query fondamentali, ad esempio `Where`, `Select`, `Order By`, `Take While`e altri.  
  
 Ad esempio, il codice seguente definisce una query che restituisce tutti gli studenti senior da un elenco di studenti.  
  
 [!code-vb[9 VbLINQVbFeatures](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_10.vb)]  
  
 La definizione della query viene compilata nel codice che è simile all'esempio seguente, che utilizza due espressioni lambda per specificare gli argomenti per `Where` e `Select`.  
  
 [!code-vb[VbLINQVbFeatures&#10;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_11.vb)]  
  
 Entrambe le versioni possono essere eseguita tramite un `For Each` ciclo:  
  
 [!code-vb[VbLINQVbFeatures&#11;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_12.vb)]  
  
 Per ulteriori informazioni, vedere [le espressioni Lambda](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Language-Integrated Query (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [LINQ e stringhe (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [Istruzione Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
