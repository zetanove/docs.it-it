---
title: Metodi di estensione (Guida per programmatori C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- methods [C#], adding to existing types
- extension methods [C#]
- methods [C#], extension
ms.assetid: 175ce3ff-9bbf-4e64-8421-faeb81a0bb51
caps.latest.revision: 35
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
ms.translationtype: Human Translation
ms.sourcegitcommit: d65b4050287289df419685127cdbbb18f52ec719
ms.openlocfilehash: a214f129424fd458decf473ef94ec3c5ed6eed3c
ms.contentlocale: it-it
ms.lasthandoff: 05/16/2017

---
# <a name="extension-methods-c-programming-guide"></a>Metodi di estensione (Guida per programmatori C#)
I metodi di estensione consentono di "aggiungere" metodi ai tipi esistenti senza creare un nuovo tipo derivato, ricompilare o modificare in altro modo il tipo originale. I metodi di estensione sono uno speciale tipo di metodo statico, ma vengono chiamati come se fossero metodi di istanza sul tipo esteso. Per il codice client scritto in C# e Visual Basic non esistono differenze evidenti tra la chiamata a un metodo di estensione e ai metodi effettivamente definiti in un tipo.  
  
 I metodi di estensione più comuni sono gli operatori query standard [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] che aggiungono la funzionalità di query ai tipi <xref:System.Collections.IEnumerable?displayProperty=fullName> e <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> esistenti. Per utilizzare gli operatori query standard, inserirli innanzitutto nell'ambito con una direttiva `using System.Linq`. In questo modo qualsiasi tipo che implementa <xref:System.Collections.Generic.IEnumerable%601> avrà apparentemente metodi di istanza quali <xref:System.Linq.Enumerable.GroupBy%2A>, <xref:System.Linq.Enumerable.OrderBy%2A>, <xref:System.Linq.Enumerable.Average%2A>e così via. È possibile visualizzare questi metodi aggiuntivi con la funzionalità di completamento istruzioni di IntelliSense quando si digita "punto" dopo un'istanza di un tipo <xref:System.Collections.Generic.IEnumerable%601>, ad esempio <xref:System.Collections.Generic.List%601> o <xref:System.Array>.  
  
 Nell'esempio seguente viene illustrato come chiamare il metodo `OrderBy` dell'operatore query standard su una matrice di Integer. L'espressione tra parentesi è un'espressione lambda. Molti operatori query standard accettano espressioni lambda come parametri, sebbene non sia un requisito per i metodi di estensione. Per altre informazioni, vedere [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 [!code-cs[csProgGuideExtensionMethods#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/extension-methods_1.cs)]  
  
 I metodi di estensione sono definiti come metodi statici, ma vengono chiamati utilizzando la sintassi del metodo di istanza. Il primo parametro specifica su quale tipo opera il metodo ed è preceduto dal modificatore [this](../../../csharp/language-reference/keywords/this.md). I metodi di estensione si trovano nell'ambito solo quando si importa in modo esplicito lo spazio dei nomi nel codice sorgente con una direttiva `using`.  
  
 Nell'esempio riportato di seguito viene illustrato un metodo di estensione definito per la classe <xref:System.String?displayProperty=fullName>. Si noti che viene definito in una classe statica non annidata e non generica:  
  
 [!code-cs[csProgGuideExtensionMethods#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/extension-methods_2.cs)]  
  
 Il metodo di estensione `WordCount` può essere inserito nell'ambito con questa direttiva `using`:  
  
```  
using ExtensionMethods;  
```  
  
 Può inoltre essere chiamato da un'applicazione utilizzando questa sintassi:  
  
```  
string s = "Hello Extension Methods";  
int i = s.WordCount();  
```  
  
 Nel codice si richiama il metodo di estensione con la sintassi del metodo di istanza. Microsoft Intermediate Language (IL) generato dal compilatore converte tuttavia il codice in una chiamata sul metodo statico. Il principio di incapsulamento non viene pertanto realmente violato. Infatti, i metodi di estensione non possono accedere a variabili private nel tipo che stanno estendendo.  
  
 Per altre informazioni, vedere [Procedura: implementare e chiamare un metodo di estensione personalizzato](../../../csharp/programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method.md).  
  
 In generale, è molto più frequente chiamare i metodi di estensione che implementarne di personalizzati. Perché i metodi di estensione vengono chiamati utilizzando la sintassi del metodo di istanza, non è necessaria alcuna particolare conoscenza per utilizzarli dal codice client. Per abilitare i metodi di estensione per un particolare tipo, aggiungere una direttiva `using` per lo spazio dei nomi nel quale sono definiti i metodi. Per utilizzare ad esempio gli operatori query standard, aggiungere questa direttiva `using` al codice:  
  
```  
using System.Linq;  
```  
  
 Può inoltre essere necessario aggiungere un riferimento a System.Core.dll. Si noterà che gli operatori query standard vengono ora visualizzati in IntelliSense come metodi aggiuntivi disponibili per la maggior parte dei tipi <xref:System.Collections.Generic.IEnumerable%601>.  
  
> [!NOTE]
>  Anche se gli operatori query standard non sono visualizzati in IntelliSense per <xref:System.String>, sono tuttavia disponibili.  
  
## <a name="binding-extension-methods-at-compile-time"></a>Associazione di metodi di estensione in fase di compilazione  
 È possibile utilizzare metodi di estensione per estendere una classe o un'interfaccia, ma non per eseguirne l'override. Un metodo di estensione con lo stesso nome e la stessa firma di un metodo di interfaccia o di classe non verrà mai chiamato. In fase di compilazione, i metodi di estensione hanno sempre una priorità più bassa dei metodi di istanza definiti nel tipo stesso. In altre parole, se un tipo dispone di un metodo denominato `Process(int i)` e si dispone di un metodo di estensione con la stessa firma, il compilatore eseguirà sempre l'associazione al metodo di istanza. Quando il compilatore rileva una chiamata al metodo, cerca innanzitutto una corrispondenza nei metodi di istanza del tipo. Se non viene trovata alcuna corrispondenza, cercherà eventuali metodi di estensione definiti per il tipo ed eseguirà l'associazione al primo metodo di estensione trovato. Nell'esempio seguente viene dimostrato come il compilatore determina a quale metodo di estensione o metodo di istanza eseguire l'associazione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono illustrate le regole che il compilatore C# segue nel determinare se associare una chiamata al metodo a un metodo di istanza sul tipo o a un metodo di estensione. La classe `Extensions` statica contiene metodi di estensione definiti per qualsiasi tipo che implementa `IMyInterface`. Le classi `A`, `B` e `C` implementano tutte l'interfaccia.  
  
 Il metodo di estensione `MethodB` non viene mai chiamato perché il nome e la firma corrispondono esattamente a metodi già implementati dalle classi.  
  
 Quando il compilatore non è in grado di trovare un metodo di istanza con una firma corrispondente, eseguirà l'associazione a un metodo di estensione corrispondente se esistente.  
  
 [!code-cs[csProgGuideExtensionMethods#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/extension-methods_3.cs)]  
  
## <a name="general-guidelines"></a>Indicazioni generali  
 In generale, si consiglia di implementare i metodi di estensione sporadicamente e solo se necessario. Se possibile, è opportuno che il codice client che deve estendere un tipo esistente esegua questa operazione creando un nuovo tipo derivato dal tipo esistente. Per altre informazioni, vedere [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md).  
  
 Quando si utilizza un metodo di estensione per estendere un tipo di cui non è possibile modificare il codice sorgente, si corre il rischio che una modifica nell'implementazione del tipo provochi l'interruzione del metodo di estensione.  
  
 Se si implementano metodi di estensione per un determinato tipo, è importante tenere presente quanto segue:  
  
-   Un metodo di estensione non verrà mai chiamato se dispone della stessa firma di un metodo definito nel tipo.  
  
-   I metodi di estensione vengono inseriti nell'ambito al livello dello spazio dei nomi. Se, ad esempio, si dispone di più classi statiche contenenti metodi di estensione in un solo spazio dei nomi denominato `Extensions`, verranno tutti inseriti nell'ambito dalla direttiva `using Extensions;`.  
  
 Per una libreria di classi implementata, non è necessario utilizzare i metodi di estensione per evitare l'incremento del numero di versione di un assembly. Se si desidera aggiungere funzionalità significative a una libreria per il quale si è proprietari del codice sorgente, è necessario seguire le linee guida standard di .NET Framework per il controllo delle versioni degli assembly. Per altre informazioni, vedere [Controllo delle versioni degli assembly](https://msdn.microsoft.com/library/51ket42z).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Esempi di programmazione parallela (sono inclusi molti metodi di estensione di esempio)](http://code.msdn.microsoft.com/Samples-for-Parallel-b4b76364)   
 [Espressioni lambda](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Cenni preliminari sugli operatori di query standard](http://msdn.microsoft.com/library/24cda21e-8af8-4632-b519-c404a839b9b2)   
 [Regole di conversione per parametri Instance e relativo impatto](http://go.microsoft.com/fwlink/?LinkId=112385)   
 [Interoperabilità dei metodi di estensione tra linguaggi](http://go.microsoft.com/fwlink/?LinkId=112386)   
 [Metodi di estensione e delegati sottoposti a currying](http://go.microsoft.com/fwlink/?LinkId=112387)   
 [Associazione di metodi di estensione e segnalazione errori](http://go.microsoft.com/fwlink/?LinkId=112388)

