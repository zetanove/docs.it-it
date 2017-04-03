---
title: Debug degli alberi delle espressioni in Visual Studio (C#) | Documentazione Microsoft
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
ms.assetid: 1369fa25-0fbd-4b92-98d0-8df79c49c27a
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 14ab67e78a3b4c4819ddca36a406526e78f5485e
ms.lasthandoff: 03/13/2017

---
# <a name="debugging-expression-trees-in-visual-studio-c"></a>Debug degli alberi delle espressioni in Visual Studio (C#)
È possibile analizzare la struttura e il contenuto degli alberi delle espressioni durante il debug delle applicazioni. Per una breve panoramica della struttura ad albero dell'espressione, è possibile usare la proprietà `DebugView`, disponibile solo nella modalità di debug. Per altre informazioni sul debug, vedere [Debug in Visual Studio](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio).  
  
 Per rappresentare meglio il contenuto degli alberi delle espressioni, la proprietà `DebugView` usa i visualizzatori di Visual Studio. Per altre informazioni, vedere [Creare visualizzatori personalizzati](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data).  
  
### <a name="to-open-a-visualizer-for-an-expression-tree"></a>Per aprire un visualizzatore per un albero delle espressioni  
  
1.  Fare clic sull'icona a forma di lente di ingrandimento visualizzata accanto alla proprietà `DebugView` di una struttura ad albero dell'espressione in **Suggerimenti dati**, in una finestra **Espressioni di controllo**, nella finestra **Auto** o nella finestra **Variabili locali**.  
  
     Verrà visualizzato un elenco di visualizzatori.  
  
2.  Fare clic sul visualizzatore da usare.  
  
 Ogni tipo di espressione viene visualizzato nel visualizzatore come descritto nelle sezioni seguenti.  
  
## <a name="parameterexpressions"></a>ParameterExpressions  
 I nomi di variabili <xref:System.Linq.Expressions.ParameterExpression> vengono visualizzati con un simbolo "$" all'inizio.  
  
 Se un parametro non ha un nome, viene assegnato un nome generato automaticamente, ad esempio `$var1` o `$var2`.  
  
### <a name="examples"></a>Esempi  
  
|Espressione|Proprietà `DebugView`|  
|----------------|--------------------------|  
|`ParameterExpression numParam =  Expression.Parameter(typeof(int), "num");`|`$num`|  
|`ParameterExpression numParam =  Expression.Parameter(typeof(int));`|`$var1`|  
  
## <a name="constantexpressions"></a>ConstantExpressions  
 Per gli oggetti <xref:System.Linq.Expressions.ConstantExpression> che rappresentano valori intero, stringhe e `null`, viene visualizzato il valore della costante.  
  
 Per i tipi numerici che usano suffissi standard come valori letterali in C#, il suffisso viene aggiunto al valore. La tabella seguente mostra i suffissi associati ai vari tipi numerici.  
  
|Tipo|Suffisso|  
|----------|------------|  
|<xref:System.UInt32>|G|  
|<xref:System.Int64>|L|  
|<xref:System.UInt64>|UL|  
|<xref:System.Double>|D|  
|<xref:System.Single>|F|  
|<xref:System.Decimal>|M|  
  
### <a name="examples"></a>Esempi  
  
|Espressione|Proprietà `DebugView`|  
|----------------|--------------------------|  
|`int num = 10; ConstantExpression expr = Expression.Constant(num);`|10|  
|`double num = 10; ConstantExpression expr = Expression.Constant(num);`|10D|  
  
## <a name="blockexpression"></a>BlockExpression  
 Se il tipo di un oggetto <xref:System.Linq.Expressions.BlockExpression> differisce dal tipo dell'ultima espressione nel block, il tipo viene visualizzato nella proprietà `DebugInfo` tra bracket angolari (\< e >). In caso contrario, il tipo dell'oggetto <xref:System.Linq.Expressions.BlockExpression> non viene visualizzato.  
  
### <a name="examples"></a>Esempi  
  
|Espressione|Proprietà `DebugView`|  
|----------------|--------------------------|  
|`BlockExpression block = Expression.Block(Expression.Constant("test"));`|`.Block() {`<br /><br /> `"test"`<br /><br /> `}`|  
|`BlockExpression block =  Expression.Block(typeof(Object), Expression.Constant("test"));`|`.Block<System.Object>() {`<br /><br /> `"test"`<br /><br /> `}`|  
  
## <a name="lambdaexpression"></a>LambdaExpression  
 Gli oggetti <xref:System.Linq.Expressions.LambdaExpression> vengono visualizzati insieme ai relativi tipi di delegati.  
  
 Se un'espressione lamda non ha un nome, viene assegnato un nome generato automaticamente, ad esempio `#Lambda1` o `#Lambda2`.  
  
### <a name="examples"></a>Esempi  
  
|Espressione|Proprietà `DebugView`|  
|----------------|--------------------------|  
|`LambdaExpression lambda =  Expression.Lambda<Func<int>>(Expression.Constant(1));`|`.Lambda #Lambda1<System.Func'1[System.Int32]>() {`<br /><br /> `1`<br /><br /> `}`|  
|`LambdaExpression lambda =  Expression.Lambda<Func<int>>(Expression.Constant(1), "SampleLambda", null);`|`.Lambda SampleLambda<System.Func'1[System.Int32]>() {`<br /><br /> `1`<br /><br /> `}`|  
  
## <a name="labelexpression"></a>LabelExpression  
 Se si specifica un valore predefinito per l'oggetto <xref:System.Linq.Expressions.LabelExpression>, questo valore viene visualizzato prima dell'oggetto <xref:System.Linq.Expressions.LabelTarget>.  
  
 Il token `.Label` indica l'inizio dell'etichetta. Il token `.LabelTarget` indica la destinazione alla quale passare.  
  
 Se un'etichetta non presenta un nome, ne viene assegnato uno generato automaticamente, ad esempio `#Label1` o `#Label2`.  
  
### <a name="examples"></a>Esempi  
  
|Espressione|Proprietà `DebugView`|  
|----------------|--------------------------|  
|`LabelTarget target = Expression.Label(typeof(int), "SampleLabel"); BlockExpression block = Expression.Block( Expression.Goto(target, Expression.Constant(0)), Expression.Label(target, Expression.Constant(-1)));`|`.Block() {`<br /><br /> `.Goto SampleLabel { 0 };`<br /><br /> `.Label`<br /><br /> `-1`<br /><br /> `.LabelTarget SampleLabel:`<br /><br /> `}`|  
|`LabelTarget target = Expression.Label(); BlockExpression block = Expression.Block( Expression.Goto(target5), Expression.Label(target5));`|`.Block() {`<br /><br /> `.Goto #Label1 { };`<br /><br /> `.Label`<br /><br /> `.LabelTarget #Label1:`<br /><br /> `}`|  
  
## <a name="checked-operators"></a>Operatori checked  
 Gli operatori di questo tipo vengono visualizzati con il simbolo "#" davanti l'operatore. Ad esempio, l'operatore di addizione checked viene visualizzato come `#+`.  
  
### <a name="examples"></a>Esempi  
  
|Espressione|Proprietà `DebugView`|  
|----------------|--------------------------|  
|`Expression expr = Expression.AddChecked( Expression.Constant(1), Expression.Constant(2));`|`1 #+ 2`|  
|`Expression expr = Expression.ConvertChecked( Expression.Constant(10.0), typeof(int));`|`#(System.Int32)10D`|  
  
## <a name="see-also"></a>Vedere anche  
 [Alberi delle espressioni (C#)](../../../../csharp/programming-guide/concepts/expression-trees/index.md)   
 [Debugging in Visual Studio](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio)  (Debug in Visual Studio)  
 [Creazione di visualizzatori personalizzati](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data)
