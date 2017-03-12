---
title: "Istruzione using (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "using (istruzione) [C#]"
ms.assetid: afc355e6-f0b9-4240-94dd-0d93f17d9fc3
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# Istruzione using (Riferimenti per C#)
Fornisce una sintassi utile che garantisce l'utilizzo corretto degli oggetti <xref:System.IDisposable>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare l'istruzione using.  
  
 [!code-cs[csrefKeywordsNamespace#4](../../../csharp/language-reference/keywords/codesnippet/csharp/using-statement_1.cs)]  
  
## Note  
 <xref:System.IO.File> e <xref:System.Drawing.Font> sono esempi di tipi gestiti che accedono a risorse non gestite, in questo caso handle di file e contesti di dispositivo.  Sono disponibili altri tipi di risorse e di librerie di classi non gestite che li incapsulano.  Tutti questi tipi devono implementare l'interfaccia <xref:System.IDisposable>.  
  
 Quando si utilizza un oggetto `IDisposable`, è di norma necessario dichiararlo e crearne un'istanza in un'istruzione `using`.  L'istruzione `using` chiama il metodo <xref:System.IDisposable.Dispose%2A> sull'oggetto nel modo corretta e, quando utilizzata come illustrato in precedenza, fa in modo che l'oggetto stesso esca dall'ambito non appena viene chiamato il metodo <xref:System.IDisposable.Dispose%2A>.  All'interno del blocco `using`, l'oggetto è di sola lettura e non può essere modificato né riassegnato.  
  
 L'istruzione `using` assicura che venga chiamato il metodo <xref:System.IDisposable.Dispose%2A> anche se si verifica un'eccezione mentre vengono chiamati metodi sull'oggetto.  È possibile ottenere lo stesso risultato inserendo l'oggetto in un blocco try e chiamando il metodo <xref:System.IDisposable.Dispose%2A> in un blocco finally, in quanto l'istruzione `using` viene tradotta in questo modo dal compilatore.  L'esempio di codice precedente viene esteso al codice riportato di seguito in fase di compilazione \(le parentesi graffe aggiuntive creano l'ambito limitato per l'oggetto\):  
  
 [!code-cs[csrefKeywordsNamespace#5](../../../csharp/language-reference/keywords/codesnippet/csharp/using-statement_2.cs)]  
  
 Più istanze di un tipo possono essere dichiarate in un'istruzione `using`, come illustrato nell'esempio riportato di seguito.  
  
 [!code-cs[csrefKeywordsNamespace#6](../../../csharp/language-reference/keywords/codesnippet/csharp/using-statement_3.cs)]  
  
 Benché sia possibile creare un'istanza dell'oggetto risorsa e passare la variabile all'istruzione `using`, non si tratta di una procedura consigliata.  In questo caso, l'oggetto rimane in ambito dopo il rilascio del blocco `using` da parte del controllo, anche se probabilmente non ha più accesso alle proprie risorse non gestite.  Ciò significa che non è più completamente inizializzato.  Il tentativo di utilizzare l'oggetto all'esterno del blocco `using` potrebbe causare la generazione di un'eccezione.  Per questo motivo, è in genere consigliabile creare un'istanza dell'oggetto nell'istruzione `using` e limitarne l'ambito al blocco `using`.  
  
 [!code-cs[csrefKeywordsNamespace#7](../../../csharp/language-reference/keywords/codesnippet/csharp/using-statement_4.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Direttiva using](../../../csharp/language-reference/keywords/using-directive.md)   
 [Garbage Collection](../Topic/Garbage%20Collection.md)   
 [Implementing a Dispose Method](../Topic/Implementing%20a%20Dispose%20Method.md)