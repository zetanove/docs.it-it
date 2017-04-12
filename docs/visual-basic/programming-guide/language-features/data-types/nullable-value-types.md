---
title: Tipi di valore nullable (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Nullable
dev_langs:
- VB
helpviewer_keywords:
- nullable types [Visual Basic]
- '? [Visual Basic]'
- types [Visual Basic], nullable
- nullable types
- data types [Visual Basic], nullable
ms.assetid: 9ac3b602-6f96-4e6d-96f7-cd4e81c468a6
caps.latest.revision: 23
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9cdf1864fe955a082936596821ee84c831b86444
ms.lasthandoff: 03/13/2017

---
# <a name="nullable-value-types-visual-basic"></a>Tipi di valori nullable (Visual Basic)
A volte si lavora con un tipo di valore che non dispongono di un valore definito in determinate circostanze. Ad esempio, un campo in un database potrebbe essere necessario distinguere tra l'assegnazione di un valore significativo e non un valore assegnato. Tipi di valore possono essere esteso per i relativi valori normali o un valore null. Tale estensione viene chiamato un *tipo nullable*.  
  
 Ogni tipo nullable viene costruito dalla classe generica <xref:System.Nullable%601>struttura.</xref:System.Nullable%601> Si consideri un database che tiene traccia delle attività lavorative. Il seguente esempio crea un oggetto nullable `Boolean` digitare e dichiara una variabile di quel tipo. È possibile scrivere la dichiarazione in tre modi:  
  
 [!code-vb[VbVbalrNullableValue n.&1;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_1.vb)]  
  
 La variabile `ridesBusToWork` può contenere un valore di `True`, un valore di `False`, o nessun valore. Il valore iniziale non è alcun valore, che in questo caso potrebbe significare che le informazioni non ha ancora ottenute per questa persona. Al contrario, `False` potrebbe significare che ha ottenute le informazioni e la persona non sfruttare il bus di lavoro.  
  
 È possibile dichiarare variabili e proprietà con tipi nullable ed è possibile dichiarare una matrice con elementi di un tipo nullable. È possibile dichiarare procedure con tipi nullable come parametri, e si può restituire un tipo nullable da un `Function` procedura.  
  
 Non è possibile costruire un tipo nullable su un tipo di riferimento, ad esempio una matrice, un `String`, o una classe. Il tipo sottostante deve essere un tipo di valore. Per ulteriori informazioni, vedere [tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md).  
  
## <a name="using-a-nullable-type-variable"></a>Utilizzo di una variabile di tipo Nullable  
 I membri di un tipo nullable più importanti sono le <xref:System.Nullable%601.HasValue%2A>e <xref:System.Nullable%601.Value%2A>proprietà.</xref:System.Nullable%601.Value%2A> </xref:System.Nullable%601.HasValue%2A> Per una variabile di un tipo nullable, <xref:System.Nullable%601.HasValue%2A>indica se la variabile contiene un valore definito.</xref:System.Nullable%601.HasValue%2A> Se <xref:System.Nullable%601.HasValue%2A>è `True`, è possibile leggere il valore da <xref:System.Nullable%601.Value%2A>.</xref:System.Nullable%601.Value%2A> </xref:System.Nullable%601.HasValue%2A> Si noti che entrambi <xref:System.Nullable%601.HasValue%2A>e <xref:System.Nullable%601.Value%2A>sono `ReadOnly` proprietà.</xref:System.Nullable%601.Value%2A> </xref:System.Nullable%601.HasValue%2A>  
  
### <a name="default-values"></a>Valori predefiniti  
 Quando si dichiara una variabile con un tipo nullable, il relativo <xref:System.Nullable%601.HasValue%2A>proprietà ha un valore predefinito di `False`.</xref:System.Nullable%601.HasValue%2A> Ciò significa che per impostazione predefinita la variabile non ha valore definito, anziché il valore predefinito del relativo tipo di valore sottostante. Nell'esempio seguente, la variabile `numberOfChildren` inizialmente non ha valore definito, anche se il valore predefinito di `Integer` tipo è 0.  
  
 [!code-vb[VbVbalrNullableValue n.&2;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_2.vb)]  
  
 Un valore null è utile per indicare un valore non definito o sconosciuto. Se `numberOfChildren` fosse stato dichiarato come `Integer`, non vi sarà alcun valore in grado di indicare che le informazioni non sono attualmente disponibili.  
  
### <a name="storing-values"></a>La memorizzazione di valori  
 Archiviare un valore in una variabile o proprietà di un tipo nullable nel modo usuale. Nell'esempio seguente assegna un valore alla variabile `numberOfChildren` dichiarato nell'esempio precedente.  
  
 [!code-vb[VbVbalrNullableValue n.&3;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_3.vb)]  
  
 Se una variabile o proprietà di un tipo nullable contiene un valore definito, è possibile che venga ripristinato lo stato iniziale di non avere un valore assegnato. Questo caso, impostare la variabile o proprietà `Nothing`, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrNullableValue n.&4;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_4.vb)]  
  
> [!NOTE]
>  Sebbene sia possibile assegnare `Nothing` a una variabile di un tipo nullable, è possibile eseguirne il test per `Nothing` con il segno di uguale. Un confronto che utilizza il segno di uguale, `someVar = Nothing`, restituisce sempre `Nothing`. È possibile testare la variabile <xref:System.Nullable%601.HasValue%2A>proprietà `False`, o di test utilizzando il `Is` o `IsNot` operatore.</xref:System.Nullable%601.HasValue%2A>  
  
### <a name="retrieving-values"></a>Recupero di valori  
 Per recuperare il valore di una variabile di un tipo nullable, è necessario testare la <xref:System.Nullable%601.HasValue%2A>proprietà per assicurarsi che un valore.</xref:System.Nullable%601.HasValue%2A> Se si tenta di leggere il valore quando <xref:System.Nullable%601.HasValue%2A>è `False`, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] genera un <xref:System.InvalidOperationException>(eccezione).</xref:System.InvalidOperationException> </xref:System.Nullable%601.HasValue%2A> Nell'esempio seguente viene illustrato il modo consigliato per la lettura della variabile `numberOfChildren` degli esempi precedenti.  
  
 [!code-vb[VbVbalrNullableValue n.&5;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_5.vb)]  
  
## <a name="comparing-nullable-types"></a>Il confronto dei tipi Nullable  
 Quando nullable `Boolean` variabili vengono utilizzate nelle espressioni booleane, il risultato può essere `True`, `False`, o `Nothing`. Di seguito è la tabella della verità per `And` e `Or`. Poiché `b1` e `b2` disporrà di tre valori possibili sono presenti nove combinazioni da valutare.  
  
|B1|B2|B1 e b2|B1 o b2|  
|--------|--------|---------------|--------------|  
|`Nothing`|`Nothing`|`Nothing`|`Nothing`|  
|`Nothing`|`True`|`Nothing`|`True`|  
|`Nothing`|`False`|`False`|`Nothing`|  
|`True`|`Nothing`|`Nothing`|`True`|  
|`True`|`True`|`True`|`True`|  
|`True`|`False`|`False`|`True`|  
|`False`|`Nothing`|`False`|`Nothing`|  
|`False`|`True`|`False`|`True`|  
|`False`|`False`|`False`|`False`|  
  
 Quando il valore di una variabile o espressione booleana è `Nothing`, non è `true` né `false`. Si osservi l'esempio riportato di seguito.  
  
 [!code-vb[6 VbVbalrNullableValue](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_6.vb)]  
  
 In questo esempio, `b1 And b2` restituisce `Nothing`. Di conseguenza, il `Else` clausola viene eseguita in ogni `If` istruzione e l'output è indicato di seguito:  
  
 `Expression is not true`  
  
 `Expression is not false`  
  
> [!NOTE]
>  `AndAlso`e `OrElse`, che utilizzano la valutazione, short circuit devono valutare i secondi operandi quando restituisce il primo `Nothing`.  
  
## <a name="propagation"></a>Propagazione  
 Se uno o entrambi gli operandi di un aritmetica, di confronto, MAIUSC o operazione di tipo è nullable, il risultato dell'operazione è nullable. Se entrambi gli operandi hanno valori non `Nothing`, l'operazione viene eseguita sui valori sottostanti degli operandi, come se non fossero un tipo nullable. Nell'esempio seguente, le variabili `compare1` e `sum1` sono tipizzate in modo implicito. Se si posiziona il puntatore del mouse su di essi, si noterà che il compilatore deduce tipi nullable per entrambe.  
  
 [!code-vb[VbVbalrNullableValue&#7;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_7.vb)]  
  
 Se uno o entrambi gli operandi hanno un valore di `Nothing`, il risultato sarà `Nothing`.  
  
 [!code-vb[VbVbalrNullableValue n.&8;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_8.vb)]  
  
## <a name="using-nullable-types-with-data"></a>Utilizzo dei tipi Nullable con dati  
 Un database è uno dei posti più importanti per utilizzare i tipi nullable. Non tutti gli oggetti di database attualmente supportano i tipi nullable, mentre gli adattatori di tabella generati dalla finestra di progettazione. Vedere "Supporto dei TableAdapter per i tipi Nullable" in [TableAdapter Overview](https://docs.microsoft.com/visualstudio/data-tools/tableadapter-overview).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.InvalidOperationException></xref:System.InvalidOperationException>   
 <xref:System.Nullable%601.HasValue%2A></xref:System.Nullable%601.HasValue%2A>   
 [Uso dei tipi nullable](../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)   
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Panoramica di TableAdapter](https://docs.microsoft.com/visualstudio/data-tools/tableadapter-overview)   
 [Se (operatore)](../../../../visual-basic/language-reference/operators/if-operator.md)   
 [Inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Is (operatore)](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [Operatore IsNot](../../../../visual-basic/language-reference/operators/isnot-operator.md)
