---
title: Concetti e terminologia (trasformazione funzionale) (C#) | Documentazione Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 03defb3a-7e17-4ab1-8efa-4dd66621e860
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3e4ff1807605164afc95eaebf37a131d9dddb79c
ms.lasthandoff: 03/13/2017


---
# <a name="concepts-and-terminology-functional-transformation-c"></a>Concetti e terminologia (trasformazione funzionale) (C#)
In questo argomento vengono presentati i concetti e i termini associati alle trasformazioni funzionali pure. La trasformazione funzionale dei dati consente di ottenere codice spesso più rapidamente programmabile, più espressivo e di cui è più facile eseguire il debug e la manutenzione rispetto alla più tradizionale programmazione imperativa.  
  
 Si noti che gli argomenti di questa sezione non offrono una spiegazione dettagliata sulla programmazione funzionale, ma indicano solo alcune delle funzionalità che semplificano la trasformazione del codice XML da una forma a un'altra.  
  
## <a name="what-is-pure-functional-transformation"></a>Informazioni sulla trasformazione funzionale pure  
 Nella *trasformazione funzionale pura* un set di funzioni, denominate *funzioni pure*, definisce la modalità di trasformazione di un set di dati strutturati dal formato originale in un altro formato. Il termine "pure" indica che tali funzioni sono *componibili*, ovvero sono:  
  
-   *Autosufficienti*, pertanto possono essere ordinate e ridisposte liberamente senza ostacoli o interdipendenze con il resto del programma. Le trasformazioni pure non conoscono l'ambiente, né influiscono su di esso. Le funzioni usate nella trasformazione non presentano quindi *effetti collaterali*.  
  
-   *Indipendenti dallo stato*, pertanto eseguendo la stessa funzione o un set specifico di funzioni sullo stesso input si otterrà sempre lo stesso output. Le trasformazioni pure non mantengono in memoria informazioni sull'utilizzo precedente.  
  
> [!IMPORTANT]
>  Nelle restanti parti di questa esercitazione il termine "funzione pure" viene usato in senso generale per indicare un approccio di programmazione e non una funzionalità specifica del linguaggio.  
>   
>  Notare che le funzioni pure devono essere implementate come metodi in C#.  
>   
>  È inoltre opportuno non confondere le funzioni pure con i metodi virtuali pure di C++. Questi ultimi indicano che la classe contenitore è astratta e che non viene fornito alcun corpo del metodo.  
  
### <a name="functional-programming"></a>Programmazione funzionale  
 La *programmazione funzionale* è un approccio di programmazione che supporta direttamente la trasformazione funzionale pure.  
  
 Dal punto di vista storico, i linguaggi di programmazione funzionale generici, tra cui ML, Scheme, Haskell e F# sono stati oggetto di interesse principalmente della comunità accademica. Sebbene sia sempre stato possibile scrivere trasformazioni funzionali pure in C#, le difficoltà associate a tale operazione ne hanno scoraggiato l'uso. Nelle recenti versioni di C#, tuttavia, nuovi costrutti di linguaggio, quali le espressioni lambda e l'inferenza dei tipi contribuiscono a rendere la programmazione funzionale più semplice e produttiva.  
  
 Per altre informazioni sulla programmazione funzionale, vedere [Differenze tra programmazione funzionale e programmazione imperativa (C#)](../../../../csharp/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md).  
  
#### <a name="domain-specific-fp-languages"></a>Strumenti della programmazione funzionale specifici per il dominio  
 Sebbene i linguaggi di programmazione funzionale generici non sono stati adottati diffusamente, quelli specifici per il dominio hanno trovato miglior accoglienza. Ad esempio, i CSS (Cascading Style Sheets) vengono usati per determinare l'aspetto di molte pagine Web, mentre i fogli di stile XSLT (Extensible Stylesheet Language Transformations) vengono ampiamente usati per la modifica dei dati XML. Per altre informazioni su XSLT, vedere [Trasformazioni XSLT](http://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03).  
  
## <a name="terminology"></a>Terminologia  
 Nella tabella seguente sono riportate le definizioni di alcuni termini correlati alle trasformazioni funzionali.  
  
 funzione di ordine superiore (prima classe)  
 Funzione che può essere considerata come oggetto a livello di codice. Ad esempio, una funzione di ordine superiore può essere passata ad altre funzioni o restituita da altre funzioni. In C# i delegati e le espressioni lambda sono funzionalità del linguaggio che supportano le funzioni di ordine superiore. Per scrivere una funzione di ordine superiore, è necessario dichiarare uno o più argomenti che accettano delegati e usare spesso espressioni lambda per la chiamata. Molti degli operatori di query standard sono funzioni di ordine superiore.  
  
 Per altre informazioni, vedere [Cenni preliminari sugli operatori di query standard (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md).  
  
 espressione lambda  
 Essenzialmente funzione anonima inline utilizzabile in tutti i casi in cui è previsto un tipo delegato. Questa è una definizione semplificata delle espressioni lambda, sebbene appropriata per gli scopi di questa esercitazione.  
  
 Per altre informazioni, vedere [Espressioni lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 raccolta  
 Set strutturato di dati, in genere di tipo uniforme. Per essere compatibile con LINQ, è necessario implementare l'interfaccia <xref:System.Collections.IEnumerable> o l'interfaccia <xref:System.Linq.IQueryable> o una delle controparti generiche quali <xref:System.Collections.Generic.IEnumerator%601> o <xref:System.Linq.IQueryable%601>.  
  
 tupla (tipi anonimi)  
 Concetto matematico. Corrisponde a una sequenza finita di oggetti, ognuno di un tipo specifico, Una tupla è anche nota come elenco ordinato. I tipi anonimi costituiscono un'implementazione del linguaggio di questo concetto e consentono di dichiarare un tipo di classe senza nome e contemporaneamente di creare un'istanza di un oggetto di tale tipo.  
  
 Per altre informazioni, vedere [Tipi anonimi](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md).  
  
 inferenza dei tipi (tipizzazione implicita)  
 Capacità di un compilatore di determinare il tipo di una variabile anche in mancanza di una dichiarazione di tipo esplicita.  
  
 Per altre informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
 esecuzione posticipata e valutazione lazy  
 Azione che consiste nel posticipare la valutazione di un'espressione finché il valore risolto non è effettivamente necessario. L'esecuzione posticipata è supportata nelle raccolte.  
  
 Per altre informazioni, vedere [Introduzione alle query LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md) e [Esecuzione posticipata e valutazione lazy in LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).  
  
 Queste funzionalità del linguaggio saranno usate negli esempi di codice di tutta questa sezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alle trasformazioni funzionali pure (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [Differenze tra programmazione funzionale e programmazione imperativa (C#)](../../../../csharp/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md).
