---
title: Raggruppare i risultati per chiavi contigue
description: Come raggruppare i risultati per chiavi contigue.
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: cbda9c08-151b-4c9e-82f7-c3d7f3dac66b
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f49b0e0dac7df20fc6e5015b9707208ee65a48d6
ms.lasthandoff: 03/13/2017

---
# <a name="group-results-by-contiguous-keys"></a>Raggruppare i risultati per chiavi contigue

Nell'esempio seguente viene illustrato come raggruppare elementi in blocchi che rappresentano sottosequenze di chiavi contigue. Si supponga di avere ad esempio la sequenza di coppie chiave-valore riportata di seguito:  
  
|Chiave|Valore|  
|---------|-----------|  
|A|Me|  
|A|think|  
|A|that|  
|B|Linq|  
|C|is|  
|A|really|  
|B|cool|  
|B|!|  
  
 Verranno creati i gruppi seguenti in questo ordine:  
  
1.  We, think, that  
  
2.  Linq  
  
3.  is  
  
4.  really  
  
5.  cool, !  
  
 La soluzione viene implementata come metodo di estensione thread-safe che restituisce i risultati in modalità di flusso. In altre parole, i gruppi vengono prodotti man mano che ci si sposta lungo la sequenza di origine. A differenza degli operatori `group` o `orderby`, questa soluzione può iniziare a restituire i gruppi al chiamante prima che sia stata letta tutta la sequenza.  
  
 La caratteristica thread-safe viene ottenuta effettuando una copia di ogni gruppo o blocco nel corso dell'iterazione della sequenza di origine, come spiegato nei commenti del codice sorgente. Se nella sequenza di origine è inclusa una serie numerosa di elementi contigui, Common Language Runtime potrebbe generare <xref:System.OutOfMemoryException>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato sia il metodo di estensione che il codice client usato.  
  
 [!code-cs[cscsrefContiguousGroups#1](../../../samples/snippets/csharp/concepts/linq/how-to-group-results-by-contiguous-keys_1.cs)]  
  
 Per usare il metodo di estensione nel progetto, copiare la classe statica `MyExtensions` in un file di codice sorgente nuovo o esistente e, se richiesto, aggiungere una direttiva `using` per lo spazio dei nomi in cui si trova.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni di query LINQ](index.md)   
 
