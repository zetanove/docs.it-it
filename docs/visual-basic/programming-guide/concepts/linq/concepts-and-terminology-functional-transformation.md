---
title: Concetti e terminologia (trasformazione funzionale) (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 24fd244d-ebae-4721-8858-89bb544aea0b
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9c4716765199798e50c4318b290f8a2d76ef5841
ms.lasthandoff: 03/13/2017


---
# <a name="concepts-and-terminology-functional-transformation-visual-basic"></a>Concetti e terminologia (trasformazione funzionale) (Visual Basic)
In questo argomento vengono presentati i concetti e i termini associati alle trasformazioni funzionali pure. La trasformazione funzionale dei dati consente di ottenere codice spesso più rapidamente programmabile, più espressivo e di cui è più facile eseguire il debug e la manutenzione rispetto alla più tradizionale programmazione imperativa.  
  
 Si noti che gli argomenti di questa sezione non offrono una spiegazione dettagliata sulla programmazione funzionale, ma indicano solo alcune delle funzionalità che semplificano la trasformazione del codice XML da una forma a un'altra.  
  
## <a name="what-is-pure-functional-transformation"></a>Informazioni sulla trasformazione funzionale pure  
 In *sulla trasformazione funzionale pure*, un set di funzioni, denominate *funzioni pure*, definire la modalità di trasformazione di un set di dati strutturati dal formato originale in un altro formato. Il termine "pure" indica che le funzioni sono *componibile*, che richiede che siano:  
  
-   *Indipendente*, in modo che possano essere liberamente ordinate e ridisposte senza ostacoli o interdipendenze con il resto del programma. Le trasformazioni pure non conoscono l'ambiente, né influiscono su di esso. Vale a dire le funzioni usate nella trasformazione non presentano *gli effetti collaterali*.  
  
-   *Senza stato*, in modo che eseguendo la stessa funzione o un set specifico di funzioni sullo stesso input si otterrà sempre lo stesso output. Le trasformazioni pure non mantengono in memoria informazioni sull'utilizzo precedente.  
  
> [!IMPORTANT]
>  Nelle restanti parti di questa esercitazione il termine "funzione pure" viene usato in senso generale per indicare un approccio di programmazione e non una funzionalità specifica del linguaggio.  
>   
>  Si noti che le funzioni pure devono essere implementate come funzioni in Visual Basic.  
>   
>  È inoltre opportuno non confondere le funzioni pure con i metodi virtuali pure di C++. Questi ultimi indicano che la classe contenitore è astratta e che non viene fornito alcun corpo del metodo.  
  
### <a name="functional-programming"></a>Programmazione funzionale  
 *Programmazione funzionale* è un approccio di programmazione che supporta direttamente la trasformazione funzionale pure.  
  
 In passato, generici linguaggi di programmazione funzionale, ad esempio ML, schema, Haskell e F #, sono stati principalmente di interesse della comunità accademica. Sebbene sia sempre stato possibile scrivere trasformazioni funzionali pure in Visual Basic, la difficoltà di procedere in modo non ha un'opzione interessante per la maggior parte dei programmatori. Nelle versioni successive di Visual Basic, tuttavia, nuovi costrutti di linguaggio, ad esempio espressioni lambda e inferenza del tipo rendere la programmazione funzionale più semplice ed efficiente.  
  
 Per ulteriori informazioni sulla programmazione funzionale, vedere [vs programmazione funzionale. Programmazione imperativa (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md).  
  
#### <a name="domain-specific-fp-languages"></a>Strumenti della programmazione funzionale specifici per il dominio  
 Sebbene i linguaggi di programmazione funzionale generici non sono stati adottati diffusamente, quelli specifici per il dominio hanno trovato miglior accoglienza. Ad esempio, i CSS (Cascading Style Sheets) vengono usati per determinare l'aspetto di molte pagine Web, mentre i fogli di stile XSLT (Extensible Stylesheet Language Transformations) vengono ampiamente usati per la modifica dei dati XML. Per ulteriori informazioni su XSLT, vedere [le trasformazioni XSLT](http://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03).  
  
## <a name="terminology"></a>Terminologia  
 Nella tabella seguente sono riportate le definizioni di alcuni termini correlati alle trasformazioni funzionali.  
  
 funzione di ordine superiore (prima classe)  
 Funzione che può essere considerata come oggetto a livello di codice. Ad esempio, una funzione di ordine superiore può essere passata ad altre funzioni o restituita da altre funzioni. In Visual Basic, delegati e le espressioni lambda sono funzionalità del linguaggio che supportano le funzioni di ordine superiore. Per scrivere una funzione di ordine superiore, è necessario dichiarare uno o più argomenti che accettano delegati e usare spesso espressioni lambda per la chiamata. Molti degli operatori di query standard sono funzioni di ordine superiore.  
  
 Per ulteriori informazioni, vedere [Panoramica di operatori Query Standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).  
  
 espressione lambda  
 Essenzialmente funzione anonima inline utilizzabile in tutti i casi in cui è previsto un tipo delegato. Questa è una definizione semplificata delle espressioni lambda, sebbene appropriata per gli scopi di questa esercitazione.  
  
 Per ulteriori informazioni, vedere [le espressioni Lambda](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 raccolta  
 Set strutturato di dati, in genere di tipo uniforme. Per essere compatibile con LINQ, è necessario implementare una raccolta di <xref:System.Collections.IEnumerable>interfaccia o <xref:System.Linq.IQueryable>interfaccia (o una delle controparti generiche <xref:System.Collections.Generic.IEnumerator%601>o <xref:System.Linq.IQueryable%601>).</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerator%601> </xref:System.Linq.IQueryable> </xref:System.Collections.IEnumerable>  
  
 tupla (tipi anonimi)  
 Concetto matematico. Corrisponde a una sequenza finita di oggetti, ognuno di un tipo specifico, Una tupla è anche nota come elenco ordinato. I tipi anonimi costituiscono un'implementazione del linguaggio di questo concetto e consentono di dichiarare un tipo di classe senza nome e contemporaneamente di creare un'istanza di un oggetto di tale tipo.  
  
 Per ulteriori informazioni, vedere [tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
 inferenza dei tipi (tipizzazione implicita)  
 Capacità di un compilatore di determinare il tipo di una variabile anche in mancanza di una dichiarazione di tipo esplicita.  
  
 Per ulteriori informazioni, vedere [l'inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
 esecuzione posticipata e valutazione lazy  
 Azione che consiste nel posticipare la valutazione di un'espressione finché il valore risolto non è effettivamente necessario. L'esecuzione posticipata è supportata nelle raccolte.  
  
 Per ulteriori informazioni, vedere [Basic Query Operations (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md) e [esecuzione posticipata e valutazione differita in LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).  
  
 Queste funzionalità del linguaggio saranno usate negli esempi di codice di tutta questa sezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alle trasformazioni funzionali Pure (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [Differenze tra programmazione funzionale e Programmazione imperativa (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)
