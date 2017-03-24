---
title: Cenni preliminari sugli operatori di Query standard (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 302bd39e-2ec1-495b-94bf-37d370d6f05f
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: eb28988ef49e0583fb7e9197c4e13c84665074ac
ms.lasthandoff: 03/13/2017

---
# <a name="standard-query-operators-overview-visual-basic"></a>Cenni preliminari sugli operatori di Query standard (Visual Basic)
Il *operatori di query standard* i metodi che costituiscono il modello LINQ. La maggior parte di questi metodi agisce sulle sequenze, dove una sequenza è un oggetto il cui tipo implementa il <xref:System.Collections.Generic.IEnumerable%601>interfaccia o <xref:System.Linq.IQueryable%601>interfaccia.</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601> Gli operatori di query standard forniscono funzionalità di query, incluso il filtro, proiezione, aggregazione, ordinamento e altro ancora.  
  
 Esistono due set di operatori di query standard LINQ, uno che agisce sugli oggetti di tipo <xref:System.Collections.Generic.IEnumerable%601>e l'altro che agisce sugli oggetti di tipo <xref:System.Linq.IQueryable%601>.</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601> I metodi che costituiscono ogni insieme sono membri statici della <xref:System.Linq.Enumerable>e <xref:System.Linq.Queryable>classi, rispettivamente.</xref:System.Linq.Queryable> </xref:System.Linq.Enumerable> Vengono definiti come *metodi di estensione* del tipo cui operare. Ciò significa che possono essere chiamati utilizzando la sintassi del metodo statico o la sintassi del metodo di istanza.  
  
 Inoltre, molti metodi degli operatori di query standard agiscono su tipi diversi da quelli basati su <xref:System.Collections.Generic.IEnumerable%601>o <xref:System.Linq.IQueryable%601>.</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601> Il <xref:System.Linq.Enumerable>tipo definisce due diversi metodi che agiscono entrambi su oggetti di tipo <xref:System.Collections.IEnumerable>.</xref:System.Collections.IEnumerable> </xref:System.Linq.Enumerable> Questi metodi, <xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29>e <xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29>, consentono abilitare una raccolta senza parametri o non generica, eseguire una query nel modello LINQ.</xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29> </xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> Ciò avviene mediante la creazione di una raccolta di oggetti fortemente tipizzati. La <xref:System.Linq.Queryable>classe definisce due metodi simili <xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29>e <xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>, che operano su oggetti di tipo <xref:System.Linq.Queryable>.</xref:System.Linq.Queryable> </xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29> </xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29> </xref:System.Linq.Queryable>  
  
 Gli operatori di query standard sono diversi nei tempi di esecuzione, a seconda che restituiscono un valore singleton o una sequenza di valori. I metodi che restituiscono un valore singleton (ad esempio, <xref:System.Linq.Enumerable.Average%2A>e <xref:System.Linq.Enumerable.Sum%2A>) vengono eseguite immediatamente.</xref:System.Linq.Enumerable.Sum%2A> </xref:System.Linq.Enumerable.Average%2A> I metodi che restituiscono una sequenza di rinviare l'esecuzione della query e restituiscono un oggetto enumerabile.  
  
 Nel caso i metodi che agiscono sulle raccolte in memoria, ovvero i metodi che estendono <xref:System.Collections.Generic.IEnumerable%601>, l'oggetto enumerabile restituito acquisisce gli argomenti passati al metodo.</xref:System.Collections.Generic.IEnumerable%601> Quando l'oggetto viene enumerata, viene impiegata la logica dell'operatore di query e vengono restituiti i risultati della query.  
  
 Al contrario, i metodi che estendono <xref:System.Linq.IQueryable%601>non implementano il comportamento delle query, ma creare una struttura ad albero dell'espressione che rappresenta la query da eseguire.</xref:System.Linq.IQueryable%601> Elaborazione della query viene gestita dall'origine <xref:System.Linq.IQueryable%601>oggetto.</xref:System.Linq.IQueryable%601>  
  
 Chiamate ai metodi di query possono essere concatenate in una query, che consente di eseguire query di diventare arbitrariamente complesse.  
  
 Esempio di codice seguente viene illustrato come utilizzare gli operatori di query standard per ottenere informazioni su una sequenza.  
  
```vb  
Dim sentence = "the quick brown fox jumps over the lazy dog"  
' Split the string into individual words to create a collection.  
Dim words = sentence.Split(" "c)  
  
Dim query = From word In words   
            Group word.ToUpper() By word.Length Into gr = Group   
            Order By Length _  
            Select Length, GroupedWords = gr  
  
Dim output As New System.Text.StringBuilder  
For Each obj In query  
    output.AppendLine(String.Format("Words of length {0}:", obj.Length))  
    For Each word As String In obj.GroupedWords  
        output.AppendLine(word)  
    Next  
Next  
  
'Display the output  
MsgBox(output.ToString())  
  
' This code example produces the following output:  
'  
' Words of length 3:  
' THE  
' FOX  
' THE  
' DOG  
' Words of length 4:  
' OVER  
' LAZY  
' Words of length 5:  
' QUICK  
' BROWN  
' JUMPS   
```  
  
## <a name="query-expression-syntax"></a>Sintassi delle espressioni di query  
 Alcuni degli operatori di query standard utilizzate più di frequente dispongono dedicata c# e Visual Basic sintassi della parola chiave del linguaggio che consente loro di essere chiamato come parte di un *query* *espressione*. Per ulteriori informazioni sugli operatori di query standard che sono parole chiave dedicate e le relative sintassi, vedere [sintassi delle espressioni di Query per operatori di Query Standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md).  
  
## <a name="extending-the-standard-query-operators"></a>Estensione degli operatori di Query Standard  
 È possibile integrare il set di operatori di query standard da Creazione metodi specifici del dominio appropriate per il dominio di destinazione o la tecnologia. È inoltre possibile sostituire gli operatori di query standard con implementazioni personalizzate che forniscono servizi aggiuntivi, ad esempio la valutazione remota, la conversione di query e ottimizzazione. Vedere <xref:System.Linq.Enumerable.AsEnumerable%2A>per un esempio.</xref:System.Linq.Enumerable.AsEnumerable%2A>  
  
## <a name="related-sections"></a>Sezioni correlate  
 I collegamenti seguenti consentono di accedere ad argomenti che forniscono ulteriori informazioni sugli operatori di query standard diversi in base alle funzionalità.  
  
 [Ordinamento dei dati](../../../../visual-basic/programming-guide/concepts/linq/sorting-data.md)  
  
 [Operazioni sui set (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/set-operations.md)  
  
 [Il filtraggio dei dati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/filtering-data.md)  
  
 [Operazioni quantificatore (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md)  
  
 [Operazioni di proiezione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projection-operations.md)  
  
 [Partizionamento dei dati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/partitioning-data.md)  
  
 [Creare un join Operations (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/join-operations.md)  
  
 [Raggruppamento di dati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/grouping-data.md)  
  
 [Operazioni di generazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/generation-operations.md)  
  
 [Operazioni di uguaglianza (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/equality-operations.md)  
  
 [Operazioni sugli elementi (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/element-operations.md)  
  
 [La conversione dei tipi di dati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md)  
  
 [Operazioni di concatenazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/concatenation-operations.md)  
  
 [Operazioni di aggregazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md)  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable></xref:System.Linq.Enumerable>   
 <xref:System.Linq.Queryable></xref:System.Linq.Queryable>   
 [Introduzione a LINQ (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-linq.md)   
 [Sintassi delle espressioni di query per gli operatori Query Standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/query-expression-syntax-for-standard-query-operators.md)   
 [Classificazione degli operatori di Query Standard in base alla modalità di esecuzione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)   
 [Metodi di estensione](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)
