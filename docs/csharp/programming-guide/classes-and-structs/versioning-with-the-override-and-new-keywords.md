---
title: "Controllo delle versioni con le parole chiave Override e New (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, override e new"
  - "linguaggio C#, controllo delle versioni"
ms.assetid: 88247d07-bd0d-49e9-a619-45ccbbfdf0c5
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# Controllo delle versioni con le parole chiave Override e New (Guida per programmatori C#)
Il linguaggio C\# è concepito in modo che le versioni di classi [base](../../../csharp/language-reference/keywords/base.md) e classi derivate presenti in librerie differenti possano essere aggiornate mantenendo la compatibilità con le versioni precedenti.  Questo significa, ad esempio, che l'introduzione in una [classe](../../../csharp/language-reference/keywords/class.md) base di un nuovo membro con lo stesso nome di un membro di una classe derivata è completamente supportata e non determina comportamenti imprevisti.  Significa inoltre che una classe deve indicare in modo esplicito se un metodo sostituisce un metodo ereditato oppure se è un nuovo metodo che nasconde un metodo ereditato con nome simile.  
  
 Nel linguaggio C\# le classi derivate possono contenere metodi con lo stesso nome di quelli della classe base.  
  
-   Il metodo della classe base deve essere definito come [virtual](../../../csharp/language-reference/keywords/virtual.md).  
  
-   Se il metodo della classe derivata non è preceduto dalla parola chiave [new](../../../csharp/language-reference/keywords/new.md) o [override](../../../csharp/language-reference/keywords/override.md), in fase di compilazione verrà generato un messaggio di avviso e il metodo si comporterà come se fosse presente la parola chiave `new`.  
  
-   Se il metodo della classe derivata è preceduto dalla parola chiave `new`, verrà definito come indipendente dal metodo della classe base.  
  
-   Se il metodo della classe derivata è preceduto dalla parola chiave `override`, gli oggetti della classe derivata chiameranno tale metodo anziché quello della classe base.  
  
-   È possibile chiamare il metodo della classe base dall'interno della classe derivata utilizzando la parola chiave `base`.  
  
-   Le parole chiave `override`, `virtual` e `new` possono essere applicate anche a proprietà, indicizzatori ed eventi.  
  
 Per impostazione predefinita, i metodi C\# non sono virtuali.  Se un metodo è dichiarato come virtuale, qualsiasi classe che eredita tale metodo può implementarne una versione specifica.  Per rendere virtuale un metodo, viene utilizzato il modificatore `virtual` nella dichiarazione del metodo della classe base.  La classe derivata può quindi eseguire l'override del metodo virtuale della classe base mediante la parola chiave `override` oppure nascondere tale metodo mediante la parola chiave `new`.  Se non viene specificata né `override` né `new`, in fase di compilazione verrà visualizzato un messaggio di avviso e il metodo della classe derivata nasconderà quello della classe base.  
  
 Per una dimostrazione pratica di questo comportamento, si supponga che la società A abbia creato una classe denominata `GraphicsClass`, che si decide di utilizzare nel programma che si sta sviluppando.  Di seguito è riportata `GraphicsClass`:  
  
 [!code-cs[csProgGuideInheritance#27](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_1.cs)]  
  
 Questa classe viene utilizzata dalla società per cui si lavora ed è quindi possibile utilizzarla per derivare la propria classe, aggiungendo un nuovo metodo:  
  
 [!code-cs[csProgGuideInheritance#28](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_2.cs)]  
  
 L'applicazione sviluppata viene eseguita senza problemi finché la società A non rilascia una nuova versione di `GraphicsClass`, simile al codice seguente:  
  
 [!code-cs[csProgGuideInheritance#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_3.cs)]  
  
 La nuova versione di `GraphicsClass` contiene ora un metodo denominato `DrawRectangle`.  Inizialmente non accade nulla.  Il codice binario della nuova versione è infatti ancora compatibile con quello della versione precedente.  Di conseguenza, l'eventuale applicazione software distribuita continuerà a funzionare, anche se nei sistemi viene installata la nuova classe.  Le eventuali chiamate al metodo `DrawRectangle` continueranno a fare riferimento alla versione definita nella classe derivata.  
  
 Se tuttavia si ricompila l'applicazione utilizzando la nuova versione di `GraphicsClass`, viene visualizzato dal compilatore l'avviso CS0108.  Nel messaggio viene indicato che è necessario definire il comportamento del metodo `DrawRectangle` nell'applicazione.  
  
 Se si desidera che il metodo esegua l'override del nuovo metodo della classe base, utilizzare la parola chiave `override`:  
  
 [!code-cs[csProgGuideInheritance#30](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_4.cs)]  
  
 Se si specifica la parola chiave `override`, gli oggetti derivati da `YourDerivedGraphicsClass` utilizzeranno la versione di `DrawRectangle` della classe derivata.  Gli oggetti derivati da `YourDerivedGraphicsClass` potranno comunque accedere alla versione di `DrawRectangle` della classe base utilizzando la parola chiave base:  
  
 [!code-cs[csProgGuideInheritance#44](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_5.cs)]  
  
 Se non si desidera che il metodo esegua l'override del nuovo metodo della classe base, si applicano le considerazioni riportate di seguito:  Per evitare confusione tra i due metodi, è possibile rinominare il proprio metodo.  Questa soluzione può richiedere tempo, è suscettibile di errori e di fatto è poco pratica in alcuni casi.  Se tuttavia il progetto è di dimensioni relativamente ridotte, è possibile utilizzare le opzioni di refactoring di Visual Studio per rinominare il metodo.  Per ulteriori informazioni, vedere [Refactoring Classes and Types \(Class Designer\)](/visual-studio/ide/refactoring-classes-and-types-class-designer).  
  
 In alternativa, è possibile evitare la visualizzazione del messaggio di avviso utilizzando la parola chiave `new` nella definizione della classe derivata:  
  
 [!code-cs[csProgGuideInheritance#31](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_6.cs)]  
  
 La parola chiave `new` consente di indicare al compilatore che la definizione nella classe derivata nasconde quella contenuta nella classe base.  Questo è il comportamento predefinito.  
  
## Override e selezione del metodo  
 Quando un metodo viene denominato in una classe, il compilatore C\# sceglie il metodo più appropriato da chiamare nel caso in cui più metodi siano compatibili con la chiamata, ad esempio se sono disponibili due metodi con lo stesso nome ed esistono parametri compatibili con quello passato.  Nel caso specifico, i seguenti metodi sarebbero compatibili:  
  
 [!code-cs[csProgGuideInheritance#32](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_7.cs)]  
  
 Quando `DoWork` viene chiamato in un'istanza di `Derived`, il compilatore C\# tenterà innanzitutto di rendere la chiamata compatibile con le versioni di `DoWork` originariamente dichiarate in `Derived`.  I metodi di override non vengono considerati come dichiarati in una classe, ma sono nuove implementazioni di un metodo dichiarato in una classe base.  Solo se non è possibile stabilire una corrispondenza tra la chiamata e un metodo originale in `Derived` il compilatore C\# tenterà di associare la chiamata a un metodo di cui è stato eseguito l'override, con lo stesso nome e parametri compatibili.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideInheritance#33](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_8.cs)]  
  
 Poiché la variabile `val` può essere convertita implicitamente in un valore double, in fase di compilazione verrà chiamato `DoWork(double)` anziché `DoWork(int)`.  È possibile ovviare a questo problema in due modi.  Innanzitutto, evitare di dichiarare come virtuali nuovi metodi con lo stesso nome.  In secondo luogo, indicare al compilatore C\# di eseguire la chiamata al metodo virtuale facendo in modo che esegua la ricerca nell'elenco dei metodi della classe base tramite il casting dell'istanza di `Derived` in `Base`.  Poiché il metodo è virtuale, verrà chiamata l'implementazione di `DoWork(int)` in `Derived`.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideInheritance#34](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_9.cs)]  
  
 Per ulteriori esempi di `new` e di `override`, vedere [Sapere quando utilizzare le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)