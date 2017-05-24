---
title: Esecuzione di alberi delle espressioni
description: Esecuzione di alberi delle espressioni
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 109e0ac5-2a9c-48b4-ac68-9b6219cdbccf
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 8423e19047d3c967a69566ebd863f677d11a0898
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---

# <a name="executing-expression-trees"></a>Esecuzione di alberi delle espressioni

[Precedente -- Tipi di framework che supportano alberi delle espressioni](expression-classes.md)

Un *albero delle espressioni* è una struttura dei dati che rappresenta il codice.
Non è codice compilato ed eseguibile. Se si vuole eseguire il codice .NET che è rappresentato da un albero delle espressioni, è necessario convertirlo in istruzioni IL eseguibili. 
## <a name="lambda-expressions-to-functions"></a>Espressioni lambda per funzioni
È possibile convertire qualsiasi LambdaExpression o qualsiasi tipo derivato da LambdaExpression in IL eseguibile. Altri tipi di espressioni non possono essere convertiti direttamente in codice. Questa restrizione ha un effetto limitato nella pratica. Le espressioni lambda sono gli unici tipi di espressioni che potrebbero essere eseguite convertendole in linguaggio intermedio eseguibile (IL). (Riflettere su cosa significherebbe eseguire direttamente una `ConstantExpression`. Sarebbe utile?) Un albero delle espressioni che è una `LamdbaExpression` o un tipo derivato da `LambdaExpression` può essere convertito in IL.
Il tipo di espressione `Expression<TDelegate>` è l'unico esempio concreto nelle librerie di .NET Core. Viene usato per rappresentare un'espressione che esegue il mapping a qualsiasi tipo delegato. Poiché questo tipo è mappato a un tipo delegato, .NET può esaminare l'espressione e generare IL per un delegato appropriato che corrisponda alla firma dell'espressione lambda. 

Nella maggior parte dei casi, verrà creato un mapping semplice tra un'espressione e il delegato corrispondente. Ad esempio, un albero delle espressioni che è rappresentato da `Expression<Func<int>>` viene convertito in un delegato del tipo `Func<int>`. Per un'espressione lambda con qualsiasi tipo restituito e un elenco di argomenti, esiste un tipo delegato che rappresenta il tipo di destinazione per il codice eseguibile rappresentato dall'espressione lambda.

Il tipo `LamdbaExpression` contiene i membri `Compile` e `CompileToMethod` usati per convertire un albero delle espressioni in codice eseguibile. Il metodo `Compile` crea un delegato. Il metodo `ConmpileToMethod` aggiorna un oggetto `MethodBuilder` con il linguaggio intermedio che rappresenta l'output compilato dell'albero delle espressioni. Si noti che `CompileToMethod` è disponibile solo nella versione desktop completa di Framework, non su .NET Core Framework.

Facoltativamente, è anche possibile specificare un `DebugInfoGenerator` che riceverà le informazioni di debug del simbolo per l'oggetto delegato generato. Ciò consente di convertire l'albero delle espressioni in un oggetto delegato e di avere informazioni di debug complete sul delegato generato.

È necessario convertire un'espressione in un delegato tramite il codice seguente:

```csharp
Expression<Func<int>> add = () => 1 + 2;
var func = add.Compile(); // Create Delegate
var answer = func(); // Invoke Delegate
Console.WriteLine(answer);
```

Si noti che il tipo delegato è basato sul tipo di espressione. Se si vuole usare l'oggetto delegato in modo fortemente tipizzato, è necessario conoscere il tipo restituito e l'elenco di argomenti. Il metodo `LambdaExpression.Compile()` restituisce il tipo `Delegate`. È necessario eseguirne il cast al tipo di delegato corretto affinché gli strumenti in fase di compilazione controllino l'elenco di argomenti del tipo restituito.

## <a name="execution-and-lifetimes"></a>Esecuzione e durate

Si esegue il codice richiamando il delegato creato durante la chiamata a `LamdbaExpression.Compile()`. È possibile vederlo qui sopra dove `add.Compile()` restituisce un delegato. Richiamando il delegato, la chiamata a `func()` esegue il codice.

Il delegato rappresenta il codice nell'albero delle espressioni. È possibile mantenere il punto di controllo al delegato e richiamarlo in un secondo momento. Non è necessario compilare l'albero delle espressioni ogni volta che si vuole eseguire il codice che rappresenta. Tenere presente che gli alberi delle espressioni non sono modificabili e la compilazione dello stesso albero delle espressioni in un secondo momento creerà un delegato che esegue lo stesso codice.

È consigliabile prestare la massima attenzione quando si tenta di creare un meccanismo di memorizzazione nella cache più sofisticato per migliorare le prestazioni evitando chiamate di compilazione non necessarie. Il confronto tra due alberi delle espressioni arbitrari per determinare se rappresentino lo stesso algoritmo richiederà anche molto tempo. Probabilmente si scoprirà che il tempo di calcolo risparmiato evitando le chiamate aggiuntive a `LambdaExpression.Compile()` verrà abbondantemente consumato dal tempo per l'esecuzione del codice che determina due risultati diversi degli alberi delle espressioni nello stesso codice eseguibile.

## <a name="caveats"></a>Avvertenze

La compilazione di un'espressione lambda a un delegato e la chiamata al delegato è una delle operazioni più semplici che si possono eseguire con un albero delle espressioni. Anche con questa semplice operazione vi sono tuttavia alcune avvertenze da tenere in considerazione. 

Le espressioni lambda creano chiusure su tutte le variabili locali a cui si fa riferimento nell'espressione. È necessario garantire che tutte le variabili che fanno parte del delegato siano utilizzabili in corrispondenza della posizione in cui viene chiamato `Compile` e quando si esegue il delegato risultante.

In generale, il compilatore garantirà che questa condizione sia vera. Se tuttavia l'espressione accede a una variabile che implementa `IDisposable`, è possibile che il codice elimini l'oggetto mentre è ancora mantenuto attivo dall'albero delle espressioni.

Ad esempio, questo codice funziona correttamente poiché `int` non implementa `IDisposable`:

```csharp
private static Func<int, int> CreateBoundFunc()
{
    var constant = 5; // constant is captured by the expression tree
    Expression<Func<int, int>> expression = (b) => constant + b;
    var rVal = expression.Compile();
    return rVal;
}
```

Il delegato ha acquisito un riferimento alla variabile locale `constant`.
Tale variabile è accessibile in qualsiasi momento successivo, quando viene eseguita la funzione restituita da `CreateBoundFunc`.

Tenere presente tuttavia questa classe (piuttosto improbabile) che implementa `IDisposable`:

```csharp
public class Resource : IDisposable
{
    private bool isDisposed = false;
    public int Argument
    {
        get
        {
            if (!isDisposed)
                return 5;
            else throw new ObjectDisposedException("Resource");
        }
    }

    public void Dispose()
    {
        isDisposed = true;
    }
}
```

Se usata in un'espressione come illustrato di seguito, si otterrà un `ObjectDisposedException` quando si esegue il codice a cui fa riferimento la proprietà `Resource.Argument`:

```csharp
private static Func<int, int> CreateBoundResource()
{
    using (var constant = new Resource()) // constant is captured by the expression tree
    {
        Expression<Func<int, int>> expression = (b) => constant.Argument + b;
        var rVal = expression.Compile();
        return rVal;
    }
}
```

Il delegato restituito da questo metodo è stato chiuso sull'oggetto `constant`, che è stato eliminato. (È stato eliminato, perché è stato dichiarato in un'istruzione `using`.) 

A questo punto, quando si esegue il delegato restituito da questo metodo, si avrà una `ObjecctDisposedException` generata al momento dell'esecuzione.

Può sembrare strano ricevere un errore di runtime che rappresenta un costrutto in fase di compilazione, ma questo è ciò che avviene negli alberi delle espressioni.

Esistono molte variazioni di questo problema, pertanto è difficile offrire indicazioni generali per evitarlo. Prestare attenzione all'accesso alle variabili locali quando si definiscono le espressioni e prestare attenzione all'accesso allo stato nell'oggetto corrente (rappresentato da `this`) quando viene creato un albero delle espressioni che può essere restituito da un'API pubblica.

Il codice nell'espressione può fare riferimento a metodi o proprietà in altri assembly. Tale assembly deve essere accessibile quando viene definita l'espressione, quando viene compilata e quando viene richiamato il delegato risultante. Quando non è presente, si incontrerà una `ReferencedAssemblyNotFoundException`.

## <a name="summary"></a>Riepilogo

Gli alberi delle espressioni che rappresentano le espressioni lambda possono essere compilati per creare un delegato che è possibile eseguire. Questo offre un meccanismo per eseguire il codice rappresentato da un albero delle espressioni.

L'albero delle espressioni non rappresenta il codice da eseguire per qualsiasi costrutto specifico creato. Finché l'ambiente in cui viene compilato ed eseguito il codice corrisponderà all'ambiente in cui si crea l'espressione, tutto funzionerà come previsto. In caso contrario, gli errori sono molto prevedibili e verranno intercettati nei primi test di qualsiasi codice basato sugli alberi delle espressioni.

[Successivo --Interpretazione di espressioni](expression-trees-interpreting.md)

