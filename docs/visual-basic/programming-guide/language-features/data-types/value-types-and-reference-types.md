---
title: "Value Types and Reference Types | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "reference data types"
  - "reference types"
  - "value types"
  - "value data types"
  - "types [Visual Basic]"
  - "data types [Visual Basic], value types"
  - "data types [Visual Basic], reference types"
ms.assetid: fc82ce15-5a40-4c5c-a1e1-a556830e7391
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Value Types and Reference Types
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In Visual Basic, i tipi di dati vengono implementati in base alla classificazione.  I tipi di dati [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] possono essere classificati a seconda che una variabile di un determinato tipo archivi i propri dati piuttosto che un puntatore ai dati.  Se la variabile memorizza internamente i propri dati si tratta di un *tipo di valore*; se contiene un puntatore a dati che si trovano altrove si tratta di un *tipo di riferimento*.  
  
## Tipi valore  
 Un tipo di dati è un *tipo valore* se contiene i dati nella propria allocazione di memoria.  Fra i tipi di valore sono inclusi i seguenti:  
  
-   Tutti i tipi di dati numerici  
  
-   `Boolean`, `Char` e `Date`  
  
-   Tutte le strutture, anche se i relativi membri sono tipi riferimento  
  
-   Le enumerazioni, in quanto il relativo tipo sottostante è sempre `SByte`, `Short`, `Integer`, `Long`, `Byte`, `UShort`, `UInteger`o `ULong`  
  
 Ogni struttura è un tipo di valore, anche se contiene membri di tipo riferimento.  Per questo motivo, i tipi di valore come `Char` e  `Integer` vengono implementati dalle strutture di .NET Framework.  
  
 È possibile dichiarare un tipo valore tramite la parola chiave riservata, ad esempio `Decimal`.  È inoltre possibile utilizzare la parola chiave `New` per inizializzare un tipo valore.  Questo risulta particolarmente utile se il tipo presenta un costruttore che richiede parametri.  Un esempio è rappresentato dal costruttore <xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29>, che compila un nuovo valore `Decimal` dalle parti fornite.  
  
## Tipi di riferimento  
 Un *tipo riferimento* contiene un puntatore a un'altra posizione di memoria contenente i dati.  Fra i tipi di riferimento sono inclusi i seguenti:  
  
-   `String`  
  
-   Tutte le matrici, anche se i relativi elementi sono tipi valore  
  
-   I tipi di classe, ad esempio <xref:System.Windows.Forms.Form>  
  
-   Delegati  
  
 Una classe è un *tipo di riferimento*.  Per questo motivo, i tipi di riferimento come `Object` e `String` sono supportati dalle classi [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].  Si noti che ogni matrice è un tipo di riferimento, anche se i suoi membri sono tipi valore.  
  
 Poiché ogni tipo di riferimento rappresenta una classe .NET Framework. sottostante, è necessario utilizzare [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md) parola chiave quando vengono inizializzate.  Di seguito è riportata un'istruzione per l'inizializzazione di una matrice.  
  
```  
Dim totals() As Single = New Single(8) {}  
```  
  
## Elementi diversi dai tipi  
 Gli elementi di programmazione riportati di seguito non si qualificano come tipi poiché non è possibile specificarli come tipi di dati per gli elementi dichiarati.  
  
-   Spazi dei nomi  
  
-   Moduli  
  
-   Eventi  
  
-   Proprietà e routine  
  
-   Variabili, costanti e campi  
  
## Utilizzo di tipi di dati Object  
 È possibile assegnare un tipo riferimento o un tipo valore a una variabile del tipo di dati `Object`.  Una variabile `Object` contiene sempre un puntatore ai dati, mai i dati stessi.  Se tuttavia si assegna un tipo valore a una variabile `Object`, essa funzionerà come se contenesse effettivamente i propri dati.  Per ulteriori informazioni, vedere [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md).  
  
 È possibile verificare se `Object` la variabile viene utilizzata come un tipo di riferimento o un tipo di valore passandola a  <xref:Microsoft.VisualBasic.Information.IsReference%2A> metodo in  <xref:Microsoft.VisualBasic.Information> classe di  <xref:Microsoft.VisualBasic?displayProperty=fullName> spazio dei nomi.  Se il contenuto della variabile `Object` rappresenta un tipo di riferimento, <xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName> restituisce `True`.  
  
## Vedere anche  
 [Nullable Value Types](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Efficient Use of Data Types](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)