---
title: "Nullable Value Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Nullable"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "nullable types [Visual Basic]"
  - "? [Visual Basic]"
  - "types [Visual Basic], nullable"
  - "nullable types"
  - "data types [Visual Basic], nullable"
ms.assetid: 9ac3b602-6f96-4e6d-96f7-cd4e81c468a6
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# Nullable Value Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Talvolta si utilizzano tipi valore che in alcune circostanze sono privi di un valore definito.  Ad esempio, in un campo di un database potrebbe essere necessario distinguere tra l'assegnazione di un valore significativo e la non assegnazione di un valore.  È possibile estendere i tipi di valore per far sì che venga loro assegnato il valore normale o un valore null.  Tale estensione viene denominata *tipo nullable*.  
  
 Ogni tipo nullable viene costruito a partire dalla struttura <xref:System.Nullable%601> generica.  Prendere in considerazione un database che tiene traccia delle attività relative al lavoro.  Nell'esempio seguente viene creato un tipo `Boolean` nullable e viene dichiarata una variabile di quel tipo.  È possibile scrivere la dichiarazione in tre modi:  
  
 [!code-vb[VbVbalrNullableValue#1](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_1.vb)]  
  
 La variabile `ridesBusToWork` è in grado di contenere un valore di `True`, un valore di `False` o nessun valore.  Il valore iniziale non è un valore, che in questo caso potrebbe significare che le informazioni non sono ancora state ottenute per questa persona.  Il valore `False`, al contrario, potrebbe significare che si sono ottenute le informazioni e che la persona non prende l'autobus per andare a lavorare.  
  
 È possibile dichiarare variabili e proprietà con tipi nullable e dichiarare una matrice con elementi di tipo nullable.  È possibile dichiarare procedure con tipi nullable come parametri e restituire un tipo nullable da una procedura `Function`.  
  
 Non è possibile creare un tipo nullable su un tipo di riferimento quale una matrice, una `String` o una classe.  Il tipo sottostante deve essere un tipo di valore.  Per ulteriori informazioni, vedere [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md).  
  
## Utilizzo di una variabile di tipo nullable  
 I membri più importanti di un tipo nullable sono le sue proprietà <xref:System.Nullable%601.HasValue%2A> e <xref:System.Nullable%601.Value%2A>.  Per una variabile di tipo nullable, <xref:System.Nullable%601.HasValue%2A> indica se la variabile contiene un valore definito.  Se <xref:System.Nullable%601.HasValue%2A> è `True`, è possibile leggere il valore da <xref:System.Nullable%601.Value%2A>.  Si noti che <xref:System.Nullable%601.HasValue%2A> e <xref:System.Nullable%601.Value%2A> sono entrambe proprietà `ReadOnly`.  
  
### Valori predefiniti  
 Quando si dichiara una variabile con un tipo nullable, la sua proprietà <xref:System.Nullable%601.HasValue%2A> dispone di un valore predefinito di `False`.  Ciò significa che per impostazione predefinita la variabile non ha valore definito, anziché il valore predefinito del suo tipo di valore sottostante.  Nell'esempio che segue, inizialmente la variabile `numberOfChildren` non ha valore definito, anche se il valore predefinito del tipo `Integer` corrisponde a 0.  
  
 [!code-vb[VbVbalrNullableValue#2](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_2.vb)]  
  
 Un valore null è utile per indicare un valore non definito o sconosciuto.  Se `numberOfChildren` è stato dichiarato come `Integer`, non sarà presente alcun valore in grado di indicare che le informazioni non sono attualmente disponibili.  
  
### Memorizzazione di valori  
 La memorizzazione di un valore in una variabile o proprietà di un tipo nullable viene effettuata nel modo normale.  Nell'esempio che segue viene illustrato come assegnare un valore alla variabile `numberOfChildren` dichiarata nell'esempio precedente.  
  
 [!code-vb[VbVbalrNullableValue#3](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_3.vb)]  
  
 Se una variabile o proprietà di un tipo nullable contiene un valore definito, è possibile provocare il ripristino del suo stato iniziale \(non assegnazione di un valore\).  Per far questo è necessario impostare la variabile o proprietà su `Nothing`, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrNullableValue#4](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_4.vb)]  
  
> [!NOTE]
>  Sebbene sia possibile assegnare `Nothing` a una variabile del tipo nullable, non è possibile eseguirne la verifica per `Nothing` utilizzando il segno di uguale.  Un confronto che utilizza il segno di uguale, `someVar = Nothing`, restituisce sempre `Nothing`.  È possibile testare la proprietà <xref:System.Nullable%601.HasValue%2A> della variabile per `False` o testarla utilizzando l'operatore `Is` o `IsNot`.  
  
### Recupero di valori  
 Per recuperare il valore di una variabile di tipo nullable, è consigliabile verificarne prima la proprietà <xref:System.Nullable%601.HasValue%2A> per confermare che sia dotata di un valore.  Se si tenta di leggere il valore quando <xref:System.Nullable%601.HasValue%2A> è `False`, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] viene generata un'eccezione <xref:System.InvalidOperationException>.  Nell'esempio riportato di seguito viene illustrato il metodo consigliato per la lettura della variabile `numberOfChildren` degli esempi precedenti.  
  
 [!code-vb[VbVbalrNullableValue#5](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_5.vb)]  
  
## Confronto di tipi nullable  
 Quando vengono utilizzate variabili `Boolean` nullable nelle espressioni booleane, il risultato può essere `True`, `False` o `Nothing`.  Di seguito è riportata la tabella della verità per `And` e `Or`.  Poiché `b1` e `b2` hanno ora tre possibili valori, è necessario valutare nove combinazioni.  
  
|b1|b2|b1 And b2|b1 Or b2|  
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
  
 Quando il valore di una variabile o espressione booleana è `Nothing`, non è `true`  né `false`.  Prendere in considerazione l'esempio riportato di seguito.  
  
 [!code-vb[VbVbalrNullableValue#6](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_6.vb)]  
  
 In questo esempio `b1 And b2` restituisce `Nothing`.  Di conseguenza, la clausola `Else` viene eseguita in ogni istruzione `If` e l'output è il seguente:  
  
 `Expression is not true`  
  
 `Expression is not false`  
  
> [!NOTE]
>  `AndAlso` e `OrElse`, che utilizzano la valutazione short circuit devono valutare i secondi operandi quando i primi restituiscono `Nothing`.  
  
## Propagazione  
 Se uno o entrambi gli operandi di un'operazione aritmetica, di confronto, di spostamento o sui tipi sono nullable, anche il risultato dell'operazione è nullable.  Se entrambi gli operandi hanno valori che non sono `Nothing`, l'operazione viene eseguita sui valori sottostanti degli operandi, come se non fossero di tipo nullable.  Nell'esempio riportato di seguito le variabili `compare1` e `sum1` sono tipizzate in modo implicito.  Se si posiziona il puntatore del mouse su di esse, si vedrà che il compilatore deduce tipi nullable per entrambe.  
  
 [!code-vb[VbVbalrNullableValue#7](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_7.vb)]  
  
 Se uno o entrambi gli operandi hanno un valore `Nothing`, il risultato sarà `Nothing`.  
  
 [!code-vb[VbVbalrNullableValue#8](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_8.vb)]  
  
## Utilizzo di tipi nullable con i dati  
 Uno dei posti più importanti in cui utilizzare i tipi nullable è un database.  I tipi nullable non sono attualmente supportati da tutti gli oggetti di database, mentre lo sono dagli adattatori di tabella generati dalla finestra di progettazione.  Vedere "Supporto dei TableAdapter per i tipi nullable" in [Cenni preliminari sugli oggetti TableAdapter](/visual-studio/data-tools/tableadapter-overview).  
  
## Vedere anche  
 <xref:System.InvalidOperationException>   
 <xref:System.Nullable%601.HasValue%2A>   
 [Utilizzo dei tipi nullable](../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)   
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Cenni preliminari sugli oggetti TableAdapter](/visual-studio/data-tools/tableadapter-overview)   
 [If Operator](../../../../visual-basic/language-reference/operators/if-operator.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Is Operator](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot Operator](../../../../visual-basic/language-reference/operators/isnot-operator.md)