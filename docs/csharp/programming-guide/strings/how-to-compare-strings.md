---
title: 'Procedura: Confrontare stringhe (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], comparison
- comparing strings [C#]
ms.assetid: e1268e28-ee98-4695-98e9-92280f1c33c0
caps.latest.revision: 23
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 164d84a1e241572a1545c6fc2d3d1e9f0821cfcb
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-compare-strings-c-programming-guide"></a>Procedura: confrontare stringhe (Guida per programmatori C#)
Quando si confrontano stringhe, viene prodotto un risultato che indica che una delle stringhe è più grande dell'altra o che le due stringhe sono uguali. Le regole che determinano il risultato sono diverse a seconda che si esegua un *confronto ordinale* o un *confronto con distinzione delle impostazioni cultura*. È importante usare il tipo di confronto corretto per l'attività specifica.  
  
 Usare i confronti ordinali di base quando è necessario confrontare o ordinare i valori di due stringhe indipendentemente dalle convenzioni linguistiche. Un confronto ordinale di base (`System.StringComparison.Ordinal`) distingue tra maiuscole e minuscole, il che significa che le due stringhe devono corrispondere esattamente carattere per carattere: "e" non è uguale a "E". Una variante usata di frequente è `System.StringComparison.OrdinalIgnoreCase`, che include la corrispondenza a "e" ed "E". `StringComparison.OrdinalIgnoreCase` viene spesso usato per confrontare i nomi di file, i nomi di percorso, i percorsi di rete e qualsiasi altra stringa il cui valore non cambia in base alle impostazioni locali del computer dell'utente. Per altre informazioni, vedere <xref:System.StringComparison?displayProperty=fullName>.  
  
 I confronti con distinzione delle impostazioni cultura vengono in genere usati per confrontare e ordinare stringhe immesse dagli utenti finali, in quanto i caratteri e le convenzioni di ordinamento di tali stringhe possono variare a seconda delle impostazioni locali del computer dell'utente. Anche stringhe che contengono caratteri identici potrebbero essere ordinate in modo diverso a seconda delle impostazioni cultura del thread corrente.  
  
> [!NOTE]
>  Quando si confrontano stringhe, è opportuno usare i metodi che consentono di specificare in modo esplicito il tipo di confronto che si intende eseguire. In questo modo il codice risulta molto più gestibile e leggibile. Se possibile, usare gli overload dei metodi delle classi <xref:System.String?displayProperty=fullName> e <xref:System.Array?displayProperty=fullName> che accettano un parametro di enumerazione <xref:System.StringComparison>, in modo da poter specificare il tipo di confronto da eseguire. È consigliabile evitare di usare gli operatori `==` e `!=` quando si confrontano stringhe. Evitare anche di usare i metodi di istanza <xref:System.String.CompareTo%2A?displayProperty=fullName> perché nessuno degli overload accetta <xref:System.StringComparison>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come confrontare correttamente stringhe i cui valori non cambiano in base alle impostazioni locali del computer dell'utente. Viene anche illustrata la funzionalità di *centralizzazione delle stringhe* di C#. Quando un programma dichiara due o più variabili di stringa identiche, il compilatore le archivia tutte nello stesso percorso. Chiamando il metodo <xref:System.Object.ReferenceEquals%2A>, è possibile vedere che le due stringhe si riferiscono effettivamente allo stesso oggetto in memoria. Per evitare la centralizzazione, usare il metodo <xref:System.String.Copy%2A?displayProperty=fullName> , come illustrato nell'esempio.  
  
 [!code-cs[csProgGuideStrings#11](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_1.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come confrontare le stringhe con la modalità preferita tramite i metodi <xref:System.String?displayProperty=fullName>i che accettano un'enumerazione <xref:System.StringComparison>. Si noti che i metodi di istanza <xref:System.String.CompareTo%2A?displayProperty=fullName> non vengono usati in questo caso, poiché nessuno degli overload accetta <xref:System.StringComparison>.  
  
 [!code-cs[csProgGuideStrings#31](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_2.cs)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come ordinare e cercare le stringhe in una matrice con distinzione delle impostazioni cultura usando i metodi statici <xref:System.Array> che accettano un parametro <xref:System.StringComparer?displayProperty=fullName>.  
  
 [!code-cs[csProgGuideStrings#32](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-compare-strings_3.cs)]  
  
 Le classi di raccolta, come ad esempio <xref:System.Collections.Hashtable?displayProperty=fullName>, <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> e <xref:System.Collections.Generic.List%601?displayProperty=fullName> hanno dei costruttori che accettano un parametro <xref:System.StringComparer?displayProperty=fullName> quando il tipo degli elementi o delle chiavi è `string`. In generale è necessario usare sempre questi costruttori, quando possibile, e specificare il parametro `Ordinal` o `OrdinalIgnoreCase`.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>   
 <xref:System.StringComparer?displayProperty=fullName>   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)   
 [Confronto di stringhe](http://msdn.microsoft.com/library/977dc094-fe19-4955-98ec-d2294d04a4ba)   
 [Globalizzazione e localizzazione di applicazioni](https://docs.microsoft.com/visualstudio/ide/globalizing-and-localizing-applications)
