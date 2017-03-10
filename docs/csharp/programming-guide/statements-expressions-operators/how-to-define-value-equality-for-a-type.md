---
title: "Procedura: definire l&#39;uguaglianza di valori per un tipo (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Equals (metodo) [C#], override"
  - "equivalenza [C#]"
  - "equivalenza tra oggetti [C#]"
  - "override del metodo Equals [C#]"
  - "uguaglianza di valori [C#]"
ms.assetid: 4084581e-b931-498b-9534-cf7ef5b68690
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Procedura: definire l&#39;uguaglianza di valori per un tipo (Guida per programmatori C#)
Quando si definisce una classe o uno struct, si stabilisce se abbia senso creare una definizione personalizzata di uguaglianza \(o equivalenza\) di valori per il tipo.  L'uguaglianza di valori viene normalmente implementata quando si prevede che gli oggetti del tipo vengano aggiunti a una raccolta di qualche genere o quando lo scopo principale è quello di archiviare un set di campi o di proprietà.  È possibile basare la definizione di uguaglianza di valori su un confronto di tutti i campi e tutte le proprietà nel tipo oppure su un sottoinsieme.  Ma in entrambi i casi, e sia nelle classi che negli struct, l'implementazione deve seguire le cinque garanzie di equivalenza:  
  
1.  x.`Equals`\(x\) restituisce `true.` Si tratta della proprietà riflessiva.  
  
2.  x.`Equals`\(y\) restituisce lo stesso valore di y.`Equals`\(x\).  Si tratta della proprietà simmetrica.  
  
3.  Se \(x.`Equals`\(y\) && y.`Equals`\(z\)\) restituisce `true`, anche x.`Equals`\(z\) restituisce `true`.  Si tratta della proprietà transitiva.  
  
4.  Le successive chiamate di x.`Equals`\(y\) restituiscono lo stesso valore purché gli oggetti a cui x e y fanno riferimento non vengano modificati.  
  
5.  x.`Equals`\(null\) restituisce `false`.  Tuttavia, null.Equals\(null\) genera un'eccezione. Non rispetta la precedente regola numero 2.  
  
 Gli struct definiti dispongono già di un'implementazione predefinita di uguaglianza di valori che ereditano dall'override <xref:System.ValueType?displayProperty=fullName> del metodo <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName>.  Questa implementazione utilizza la reflection per esaminare tutte le proprietà e i campi pubblici e non pubblici nel tipo.  Anche se questa implementazione produce risultati corretti, è relativamente lenta rispetto a un'implementazione personalizzata scritta specificamente per il tipo.  
  
 I dettagli di implementazione relativi all'uguaglianza di valori sono diversi per le classi e gli struct.  Tuttavia, sia le classi che gli struct richiedono gli stessi passaggi di base per l'implementazione dell'uguaglianza:  
  
1.  Eseguire l'override del metodo <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> [virtuale](../../../csharp/language-reference/keywords/virtual.md).  Nella maggior parte dei casi, l'implementazione di `bool Equals( object obj )` deve solo eseguire la chiamata nel metodo `Equals` specifico del tipo che corrisponde all'implementazione dell'interfaccia <xref:System.IEquatable%601?displayProperty=fullName>.  Vedere il passaggio 2.  
  
2.  Implementare l'interfaccia <xref:System.IEquatable%601?displayProperty=fullName> fornendo un metodo `Equals` specifico del tipo.  Questo è il punto in cui viene eseguito il confronto di equivalenze effettivo.  È possibile, ad esempio, decidere di definire l'uguaglianza confrontando solo uno o due campi nel tipo.  Non generare eccezioni da `Equals`.  Solo per le classi: questo metodo deve esaminare solo i campi dichiarati nella classe.  Deve chiamare `base.Equals` per esaminare i campi presenti nella classe di base.  Non eseguire questa operazione se il tipo eredita direttamente da <xref:System.Object>, perché l'implementazione <xref:System.Object> di <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> esegue un controllo dell'uguaglianza dei riferimenti.  
  
3.  Facoltativo, ma consigliato: eseguire l'overload degli operatori [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md) e [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md).  
  
4.  Eseguire l'override di <xref:System.Object.GetHashCode%2A?displayProperty=fullName> in modo che due oggetti che presentano un'uguaglianza di valori producano lo stesso codice hash.  
  
5.  Facoltativo: per supportare le definizioni relative a "maggiore di" o "minore di", implementare l'interfaccia <xref:System.IComparable%601> per il tipo ed eseguire inoltre l'overload degli operatori [\<\=](../../../csharp/language-reference/operators/less-than-equal-operator.md) e [\>\=](../../../csharp/language-reference/operators/greater-than-equal-operator.md).  
  
 Nel primo degli esempi seguenti viene illustrata l'implementazione di una classe.  Nel secondo esempio viene illustrata l'implementazione di uno struct.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come implementare l'uguaglianza di valori in una classe \(tipo di riferimento\).  
  
 [!code-cs[csProgGuideStatements#19](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-define-value-equa_1.cs)]  
  
 Nelle classi \(tipi di riferimento\), l'implementazione predefinita di entrambi i metodi <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> esegue un confronto di uguaglianza dei riferimenti, non un controllo dell'uguaglianza dei valori.  Un responsabile dell'implementazione esegue l'override del metodo virtuale allo scopo di assegnargli la semantica di uguaglianza dei valori.  
  
 Gli operatori `==` e `!=` possono essere utilizzati con le classi anche se la classe non ne esegue l'overload.  Il comportamento predefinito, tuttavia, prevede l'esecuzione di un controllo dell'uguaglianza dei riferimenti.  In una classe, se si esegue l'overload del metodo `Equals`, è possibile eseguire l'overload degli operatori `==` e `!=`, sebbene tale operazione non sia necessaria.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come implementare l'uguaglianza di valori in uno struct \(tipo di valore\).  
  
 [!code-cs[csProgGuideStatements#20](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/how-to-define-value-equa_2.cs)]  
  
 Per gli struct, l'implementazione predefinita di <xref:System.Object.Equals%28System.Object%29?displayProperty=fullName> \(la versione sottoposta a override in <xref:System.ValueType?displayProperty=fullName>\) esegue un controllo dell'uguaglianza dei valori utilizzando la reflection per confrontare i valori di ogni campo nel tipo.  Un responsabile dell'implementazione esegue l'override del metodo `Equals` virtuale in uno struct allo scopo di fornire un mezzo più efficiente per eseguire il controllo dell'uguaglianza dei valori e facoltativamente basare il confronto su alcuni sottoinsiemi del campo o delle proprietà dello struct.  
  
 Gli operatori [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md) e [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md) non possono operare in uno struct a meno che lo struct non ne esegua l'overload esplicito.  
  
## Vedere anche  
 [Confronti di uguaglianza](../../../csharp/programming-guide/statements-expressions-operators/equality-comparisons.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)