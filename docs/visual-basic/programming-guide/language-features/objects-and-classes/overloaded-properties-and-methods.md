---
title: "Overloaded Properties and Methods (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "properties [Visual Basic], overloading"
  - "methods [Visual Basic], overloading"
  - "shadowing"
  - "names, multiple procedures with same"
  - "procedures, mulltiples with same name"
  - "classes [Visual Basic], properties"
  - "classes [Visual Basic], methods"
  - "method overloading"
  - "Overloads keyword, overloaded members"
ms.assetid: b686fb97-e7d7-4001-afaa-6650cba08f0d
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Overloaded Properties and Methods (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per overload si intende la creazione di più routine, costruttori di istanza o proprietà con lo stesso nome all'interno di una classe ma con diversi tipi di argomento.  
  
## Utilizzo dell'overload  
 L'overload è particolarmente utile quando il modello a oggetti impone l'utilizzo di nomi identici per routine che utilizzano tipi di dati diversi.  Una classe che consente la visualizzazione di diversi tipi di dati ad esempio può presentare routine `Display` simili alle seguenti:  
  
 [!code-vb[VbVbalrOOP#64](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_1.vb)]  
  
 Senza l'overload, sarebbe necessario creare nomi distinti per ciascuna routine, anche se tutte svolgono un'azione dello stesso tipo, come indicato di seguito:  
  
 [!code-vb[VbVbalrOOP#65](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_2.vb)]  
  
 L'overload semplifica l'utilizzo di proprietà e metodi in quanto consente di utilizzare diversi tipi di dati.  Il metodo `Display` di overload esaminato in precedenza ad esempio può essere chiamato da una qualsiasi delle seguenti righe di codice:  
  
 [!code-vb[VbVbalrOOP#66](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_3.vb)]  
  
 In fase di esecuzione, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] verrà chiamata la routine corretta in base ai tipi di dati dei parametri specificati.  
  
## Regole per l'overload  
 Per creare un membro in overload per una classe, aggiungere due o più proprietà o metodi con lo stesso nome.  Ad eccezione dei membri derivati in overload, è necessario che a ogni membro in overload siano associati diversi elenchi di parametri e non è possibile utilizzare i seguenti elementi come caratteristica di differenziazione quando si esegue l'overload di una proprietà o una routine:  
  
-   Modificatori, quali `ByVal` o `ByRef`, applicabili a un membro o ai parametri del membro.  
  
-   Nomi di parametri  
  
-   Tipi di valori restituiti delle routine  
  
 La parola chiave `Overloads` è facoltativa quando si esegue l'overload, ma se tale parola chiave viene utilizzata da un membro in overload, è necessario che sia specificata anche da tutti gli altri membri in overload con lo stesso nome.  
  
 Le classi derivate sono in grado di eseguire l'overload di membri ereditati con membri a cui sono associati identici parametri e tipi di parametri. Questo processo è noto come *shadowing in base al nome e alla firma*.  Se la parola chiave `Overloads` viene utilizzata quando si esegue lo shadowing in base al nome e alla firma, l'implementazione del membro presente nella classe derivata verrà utilizzata al posto dell'implementazione presente nella classe di base e tutti gli altri overload per tale membro risulteranno disponibili per le istanze della classe derivata.  
  
 Se la parola chiave `Overloads` viene omessa quando si esegue l'overload di un membro ereditato con un membro a cui sono associati identici parametri e tipi di parametri, l'overload verrà definito *shadowing in base al nome*.  Lo shadowing in base al nome consente di sostituire l'implementazione ereditata di un membro e rende tutti gli altri overload non disponibili per le istanze della classe derivata e i relativi discendenti.  
  
 Non è possibile utilizzare sia il modificatore `Overloads` che il modificatore `Shadows` con lo stesso metodo o proprietà.  
  
### Esempio  
 Nell'esempio che segue vengono creati metodi di overload che accettano rappresentazioni di tipo `String` o `Decimal` di un importo in dollari e restituiscono una stringa contenente l'imposta sul fatturato.  
  
##### Per utilizzare l'esempio che segue per creare un metodo di overload  
  
1.  Aprire un nuovo progetto e aggiungere una classe denominata `TaxClass`.  
  
2.  Aggiungere il seguente codice alla classe `TaxClass`.  
  
     [!code-vb[VbVbalrOOP#67](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_4.vb)]  
  
3.  Aggiungere la seguente routine al form:  
  
     [!code-vb[VbVbalrOOP#68](../../../../visual-basic/misc/codesnippet/VisualBasic/overloaded-properties-and-methods_5.vb)]  
  
4.  Aggiungere un pulsante al form e chiamare la routine `ShowTax` dall'evento `Button1_Click` del pulsante.  
  
5.  Eseguire il progetto e scegliere il pulsante sul form per eseguire il test della routine in overload `ShowTax`.  
  
 In fase di esecuzione, la funzione in overload appropriata viene scelta in base ai parametri utilizzati.  Quando si sceglie il pulsante, in primo luogo viene chiamato il metodo di overload con un parametro `Price` di tipo stringa e viene visualizzato un messaggio che indica che il prezzo è una stringa  e che l'imposta è pari a $5.12.  `TaxAmount` viene chiamato con un valore `Decimal` la seconda volta e viene visualizzato un messaggio che indica che il prezzo è un valore Decimal  e che l'imposta è pari a $5.12.  
  
## Vedere anche  
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Shadowing in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Inheritance Basics](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)   
 [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)