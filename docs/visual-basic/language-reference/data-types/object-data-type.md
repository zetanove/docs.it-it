---
title: "Object Data Type | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Object"
  - "vb.Variant"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "object variables, Object type"
  - "data types [Visual Basic], assigning"
  - "Object data type"
  - "Object data type, reference"
ms.assetid: 61ea4a7c-3b3d-48d4-adc4-eacfa91779b2
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Object Data Type
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Contiene indirizzi riferiti a oggetti.  A una variabile `Object` è possibile assegnare qualsiasi tipo di riferimento \(stringa, matrice, classe o interfaccia\).  Una variabile `Object` può inoltre fare riferimento a qualsiasi tipo di valore \(numerico, `Boolean`, `Char`, `Date`, struttura o enumerazione\).  
  
## Note  
 Il tipo di dati `Object` può fare riferimento a dati di qualsiasi tipo, comprese le istanze di oggetto riconosciute dall'applicazione.  Utilizzare il tipo di dati `Object` quando in fase di compilazione non si conosce il tipo di dati a cui potrebbe fare riferimento la variabile.  
  
 Il valore predefinito di `Object` è `Nothing`, un riferimento null.  
  
## Tipi di dati  
 A una variabile `Object` è possibile assegnare una variabile, una costante o un'espressione di qualsiasi tipo di dati.  Per stabilire il tipo di dati a cui fa attualmente riferimento una variabile `Object`, è possibile utilizzare il metodo <xref:System.Type.GetTypeCode%2A> della classe <xref:System.Type?displayProperty=fullName>.  Questa condizione è illustrata nell'esempio che segue.  
  
```  
Dim myObject As Object  
' Suppose myObject has now had something assigned to it.  
Dim datTyp As Integer  
datTyp = Type.GetTypeCode(myObject.GetType())  
```  
  
 Il tipo di dati `Object` è un tipo di riferimento.  Quando fa riferimento a dati di un tipo di valore, tuttavia, una variabile `Object` viene considerata un tipo di valore.  
  
## Memoria  
 Indipendentemente dal tipo di dati a cui fa riferimento, una variabile `Object` non contiene il valore dei dati stesso bensì un puntatore al valore.  Utilizza sempre quattro byte della memoria del computer, ma questo non comprende lo spazio di archiviazione necessario per i dati che rappresentano il valore della variabile.  A causa del codice che utilizza il puntatore per individuare i dati, l'accesso alle variabili `Object` che contengono tipi valore risulta leggermente più lento rispetto alle variabili di tipo esplicito.  
  
## Suggerimenti per la programmazione  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che i tipi di puntatore in altri ambienti non sono compatibili con il tipo `Object` Visual Basic.  
  
-   **Prestazioni.** Una variabile dichiarata con il tipo `Object` è abbastanza flessibile da contenere un riferimento a qualsiasi oggetto.  Quando, tuttavia, su una variabile di questo tipo si richiama un metodo o una proprietà, si verifica sempre l'*associazione tardiva* \(in fase di esecuzione\).  Per imporre l'*associazione anticipata* \(in fase di compilazione\) e ottenere prestazioni migliori, dichiarare la variabile con un nome classe specifico oppure eseguirne il cast al tipo di dati specifico.  
  
     Quando si dichiara una variabile oggetto, provare a utilizzare un tipo di classe specifico, ad esempio <xref:System.OperatingSystem>, invece del tipo `Object` generalizzato.  È inoltre consigliabile utilizzare la classe più specifica disponibile, ad esempio <xref:System.Windows.Forms.TextBox> invece di <xref:System.Windows.Forms.Control>, in modo da poter accedere alle proprietà e ai metodi rispettivi.  È in genere possibile utilizzare la casella di riepilogo **Classi** del **Visualizzatore oggetti** per cercare i nomi delle classi disponibili.  
  
-   **Conversione verso un tipo di dati più grande.** Tutti i tipi di dati e tutti i tipi di riferimento vengono convertiti nel tipo di dati `Object` più grande.  In altre parole, è possibile convertire in `Object` qualsiasi tipo senza che si verifichi un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
     Se, tuttavia, si esegue la conversione tra tipi di valori e `Object`, vengono eseguite le operazioni di *boxing* e *unboxing* che determinano un rallentamento dell'esecuzione.  
  
-   **Caratteri tipo.** `Object` non ha alcun carattere di tipo letterale o carattere identificatore di tipo.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la classe <xref:System.Object?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata una variabile `Object` che fa riferimento a un'istanza di oggetto.  
  
```  
Dim objDb As Object  
Dim myCollection As New Collection()  
' Suppose myCollection has now been populated.  
objDb = myCollection.Item(1)  
```  
  
## Vedere anche  
 <xref:System.Object>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [How to: Determine Whether Two Objects Are Related](../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [How to: Determine Whether Two Objects Are Identical](../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)