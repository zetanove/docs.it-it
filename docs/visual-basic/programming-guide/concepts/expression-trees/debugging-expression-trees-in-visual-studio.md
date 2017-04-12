---
title: Debug di alberi delle espressioni in Visual Studio (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 492cc28f-b7a2-4c47-b582-b3c437b8a5d5
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: efbd8c19947c45b3ba15ce7b574000d56526ef45
ms.lasthandoff: 03/13/2017

---
# <a name="debugging-expression-trees-in-visual-studio-visual-basic"></a>Alberi delle espressioni di debug in Visual Studio (Visual Basic)
Quando si esegue il debug delle applicazioni, è possibile analizzare la struttura e il contenuto degli alberi delle espressioni. Per ottenere una rapida panoramica della struttura ad albero dell'espressione, è possibile utilizzare il `DebugView` proprietà, che è disponibile solo in modalità debug. Per ulteriori informazioni sul debug, vedere [debug in Visual Studio](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio).  
  
 Per rappresentare meglio il contenuto degli alberi delle espressioni, il `DebugView` proprietà utilizza i visualizzatori di Visual Studio. Per ulteriori informazioni, vedere [i visualizzatori personalizzati creare](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data).  
  
### <a name="to-open-a-visualizer-for-an-expression-tree"></a>Per aprire un visualizzatore per una struttura ad albero dell'espressione  
  
1.  Fare clic sull'icona di lente di ingrandimento visualizzata accanto al `DebugView` proprietà di un albero delle espressioni in **suggerimenti dati**, **espressioni di controllo** finestra, il **Auto** finestra o **variabili locali** finestra.  
  
     Verrà visualizzato un elenco di visualizzatori.  
  
2.  Fare clic sul visualizzatore da usare.  
  
 Ogni tipo di espressione viene visualizzato nel visualizzatore come descritto nelle sezioni seguenti.  
  
## <a name="parameterexpressions"></a>ParameterExpressions  
 <xref:System.Linq.Expressions.ParameterExpression>vengono visualizzati i nomi delle variabili con un simbolo "$" all'inizio.</xref:System.Linq.Expressions.ParameterExpression>  
  
 Se un parametro non ha un nome, viene assegnato un nome generato automaticamente, ad esempio `$var1` o `$var2`.  
  
### <a name="examples"></a>Esempi  
  
-   `Expression`  
  
    ```vb  
    Dim numParam As ParameterExpression =   
    Expression.Parameter(GetType(Integer), "num")  
    ```  
  
     Proprietà `DebugView`  
  
     `$num`  
  
-   `Expression`  
  
    ```vb  
    Dim numParam As ParameterExpression =   
    Expression.Parameter(GetType(Integer))  
    ```  
  
     Proprietà `DebugView`  
  
     `$var1`  
  
## <a name="constantexpressions"></a>ConstantExpressions  
 Per <xref:System.Linq.Expressions.ConstantExpression>gli oggetti che rappresentano valori integer, stringhe e `null`, viene visualizzato il valore della costante.</xref:System.Linq.Expressions.ConstantExpression>  
  
### <a name="examples"></a>Esempi  
  
-   `Expression`  
  
    ```vb  
    Dim num as Integer= 10  
    Dim expr As ConstantExpression = Expression.Constant(num)  
    ```  
  
     Proprietà `DebugView`  
  
     10  
  
-   `Expression`  
  
    ```vb  
    Dim num As Double = 10  
    Dim expr As ConstantExpression = Expression.Constant(num)  
    ```  
  
     Proprietà `DebugView`  
  
     10D  
  
## <a name="blockexpression"></a>BlockExpression  
 Se il tipo di un <xref:System.Linq.Expressions.BlockExpression>oggetto differisce dal tipo dell'ultima espressione nel blocco, il tipo viene visualizzato nel `DebugInfo` proprietà parentesi angolari (\< e >).</xref:System.Linq.Expressions.BlockExpression> In caso contrario, il tipo di <xref:System.Linq.Expressions.BlockExpression>oggetto non viene visualizzato.</xref:System.Linq.Expressions.BlockExpression>  
  
### <a name="examples"></a>Esempi  
  
-   `Expression`  
  
    ```vb  
    Dim block As BlockExpression = Expression.Block(Expression.Constant("test"))  
    ```  
  
     Proprietà `DebugView`  
  
     `.Block() {`  
  
     `"test"`  
  
     `}`  
  
-   `Expression`  
  
    ```vb  
    Dim block As BlockExpression =   
    Expression.Block(GetType(Object), Expression.Constant("test"))  
    ```  
  
     Proprietà `DebugView`  
  
     `.Block<System.Object>() {`  
  
     `"test"`  
  
     `}`  
  
## <a name="lambdaexpression"></a>Oggetto LambdaExpression  
 <xref:System.Linq.Expressions.LambdaExpression>gli oggetti vengono visualizzati insieme ai tipi delegati.</xref:System.Linq.Expressions.LambdaExpression>  
  
 Se un'espressione lambda non ha un nome, viene assegnato un nome generato automaticamente, ad esempio `#Lambda1` o `#Lambda2`.  
  
### <a name="examples"></a>Esempi  
  
-   `Expression`  
  
    ```vb  
    Dim lambda As LambdaExpression =   
    Expression.Lambda(Of Func(Of Integer))(Expression.Constant(1))  
    ```  
  
     Proprietà `DebugView`  
  
     `.Lambda #Lambda1<System.Func'1[System.Int32]>() {`  
  
     `1`  
  
     `}`  
  
-   `Expression`  
  
    ```vb  
    Dim lambda As LambdaExpression =   
    Expression.Lambda(Of Func(Of Integer))(Expression.Constant(1), "SampleLamda", Nothing)  
    ```  
  
     Proprietà `DebugView`  
  
     `.Lambda SampleLambda<System.Func'1[System.Int32]>() {`  
  
     `1`  
  
     `}`  
  
## <a name="labelexpression"></a>LabelExpression  
 Se si specifica un valore predefinito per il <xref:System.Linq.Expressions.LabelExpression>dell'oggetto, questo valore viene visualizzato prima di <xref:System.Linq.Expressions.LabelTarget>oggetto.</xref:System.Linq.Expressions.LabelTarget> </xref:System.Linq.Expressions.LabelExpression>  
  
 Il `.Label` token indica l'inizio dell'etichetta. Il `.LabelTarget` token indica la destinazione della destinazione a cui passare.  
  
 Se un'etichetta non ha un nome, viene assegnato un nome generato automaticamente, ad esempio `#Label1` o `#Label2`.  
  
### <a name="examples"></a>Esempi  
  
-   `Expression`  
  
    ```vb  
    Dim target As LabelTarget = Expression.Label(GetType(Integer), "SampleLabel")  
    Dim label1 As BlockExpression = Expression.Block(  
    Expression.Goto(target, Expression.Constant(0)),  
    Expression.Label(target, Expression.Constant(-1)))  
    ```  
  
     Proprietà `DebugView`  
  
     `.Block() {`  
  
     `.Goto SampleLabel { 0 };`  
  
     `.Label`  
  
     `-1`  
  
     `.LabelTarget SampleLabel:`  
  
     `}`  
  
-   `Expression`  
  
    ```vb  
    Dim target As LabelTarget = Expression.Label()  
    Dim block As BlockExpression = Expression.Block(  
    Expression.Goto(target), Expression.Label(target))  
    ```  
  
     Proprietà `DebugView`  
  
     `.Block() {`  
  
     `.Goto #Label1 { };`  
  
     `.Label`  
  
     `.LabelTarget #Label1:`  
  
     `}`  
  
## <a name="checked-operators"></a>Operatori checked  
 Gli operatori checked vengono visualizzati con il simbolo "#" davanti l'operatore. Ad esempio, l'operatore di addizione selezionato viene visualizzato come `#+`.  
  
### <a name="examples"></a>Esempi  
  
-   `Expression`  
  
    ```vb  
    Dim expr As Expression = Expression.AddChecked(  
    Expression.Constant(1), Expression.Constant(2))  
    ```  
  
     Proprietà `DebugView`  
  
     `1 #+ 2`  
  
-   `Expression`  
  
    ```vb  
    Dim expr As Expression = Expression.ConvertChecked(  
    Expression.Constant(10.0), GetType(Integer))  
    ```  
  
     Proprietà `DebugView`  
  
     `#(System.Int32)10D`  
  
## <a name="see-also"></a>Vedere anche  
 [Alberi delle espressioni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)   
 [Debugging in Visual Studio](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio)  (Debug in Visual Studio)  
 [Creazione di visualizzatori personalizzati](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data)
