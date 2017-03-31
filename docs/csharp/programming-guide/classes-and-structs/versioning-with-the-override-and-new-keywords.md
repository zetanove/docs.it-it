---
title: Controllo delle versioni con le parole chiave Override e New (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, versioning
- C# language, override and new
ms.assetid: 88247d07-bd0d-49e9-a619-45ccbbfdf0c5
caps.latest.revision: 25
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b464b4c395af093bb9124bb671c5c212c750f497
ms.lasthandoff: 03/13/2017

---
# <a name="versioning-with-the-override-and-new-keywords-c-programming-guide"></a>Controllo delle versioni con le parole chiave Override e New (Guida per programmatori C#)
Il linguaggio C# è progettato in modo che il controllo delle versioni tra le classi [di base](../../../csharp/language-reference/keywords/base.md) e le classi derivate in diverse librerie possa svilupparsi e mantenere la compatibilità con le versioni precedenti. Ciò significa ad esempio che l'introduzione di un nuovo membro in una classe [di base](../../../csharp/language-reference/keywords/class.md) con lo stesso nome di un membro in una classe derivata è completamente supportata da C# e non causa comportamenti imprevisti. Significa inoltre che una classe deve dichiarare in modo esplicito se un metodo deve eseguire l'override di un metodo ereditato o se si tratta di un nuovo metodo che consente di nascondere un metodo ereditato con nome simile.  
  
 In C# le classi derivate possono contenere metodi con lo stesso nome dei metodi delle classi di base.  
  
-   Il metodo della classe di base deve essere definito come [virtuale](../../../csharp/language-reference/keywords/virtual.md).  
  
-   Se il metodo della classe derivata non è preceduto dalle parole chiave [new](../../../csharp/language-reference/keywords/new.md) o [override](../../../csharp/language-reference/keywords/override.md), il compilatore genera un avviso e il metodo si comporta come se fosse presente la parola chiave `new`.  
  
-   Se il metodo della classe derivata è preceduto dalla parola chiave `new`, il metodo è definito come indipendente dal metodo della classe di base.  
  
-   Se il metodo della classe derivata è preceduto dalla parola chiave `override`, gli oggetti della classe derivata chiameranno tale metodo anziché il metodo della classe di base.  
  
-   Il metodo della classe di base può essere chiamato dall'interno della classe derivata usando la parola chiave `base`.  
  
-   Le parole chiave `override`, `virtual` e `new` possono essere applicate anche a proprietà, indicizzatori ed eventi.  
  
 Per impostazione predefinita, i metodi C# non sono virtuali. Se un metodo viene dichiarato come virtuale, qualsiasi classe che eredita il metodo può implementare la propria versione. Per rendere un metodo virtuale, si usa il modificatore `virtual` nella dichiarazione del metodo della classe di base. La classe derivata può quindi eseguire l'override del metodo di base virtuale usando la parola chiave `override` oppure nascondere il metodo virtuale nella classe di base usando la parola chiave `new`. Se non si specifica né la parola chiave `override` né la parola chiave `new`, il compilatore genera un avviso e il metodo della classe derivata nasconde il metodo della classe di base.  
  
 Per dimostrare questo concetto in pratica, si supponga che la società A abbia creato una classe denominata `GraphicsClass` che viene usata dal programma. Di seguito è illustrata la classe `GraphicsClass`:  
  
 [!code-cs[csProgGuideInheritance#27](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_1.cs)]  
  
 La società usa questa classe e l'utente la usa per derivare la propria classe, aggiungendo un nuovo metodo:  
  
 [!code-cs[csProgGuideInheritance#28](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_2.cs)]  
  
 L'applicazione viene eseguita senza problemi, finché la società A rilascia una nuova versione di `GraphicsClass`, simile al codice seguente:  
  
 [!code-cs[csProgGuideInheritance#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_3.cs)]  
  
 La nuova versione di `GraphicsClass` ora contiene un metodo denominato `DrawRectangle`. Inizialmente non accade nulla. La nuova versione è ancora compatibile a livello binario con la versione precedente. Qualsiasi software già distribuito continuerà a funzionare, anche se la nuova classe viene installata nei relativi computer. Le eventuali chiamate al metodo `DrawRectangle` continueranno a fare riferimento alla versione in uso nella classe derivata.  
  
 Tuttavia, non appena l'applicazione viene ricompilata usando la nuova versione di `GraphicsClass`, si riceve un avviso del compilatore, CS0108. L'avviso informa che è necessario stabilire in che modo dovrà funzionare il metodo `DrawRectangle` nell'applicazione.  
  
 Se il metodo deve eseguire l'override del nuovo metodo della classe di base, usare la parola chiave `override`:  
  
 [!code-cs[csProgGuideInheritance#30](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_4.cs)]  
  
 La parola chiave `override` garantisce che qualsiasi oggetto derivato da `YourDerivedGraphicsClass` userà la versione della classe derivata di `DrawRectangle`. Gli oggetti derivati da `YourDerivedGraphicsClass` possono comunque accedere alla versione della classe di base `DrawRectangle` usando la parola chiave di base:  
  
 [!code-cs[csProgGuideInheritance#44](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_5.cs)]  
  
 Se si preferisce che il metodo non esegua l'override del nuovo metodo della classe di base, attenersi alle indicazioni che seguono. Per evitare confusione tra i due metodi, è possibile rinominare il metodo da usare. Questa operazione può richiedere molto tempo e causare errori e in alcuni casi è poco pratica. Tuttavia, se il progetto è relativamente piccolo, è possibile usare le opzioni di refactoring di Visual Studio per rinominare il metodo. Per altre informazioni, vedere [Refactoring di classi e tipi (Progettazione classi)](https://docs.microsoft.com/visualstudio/ide/refactoring-classes-and-types-class-designer).  
  
 In alternativa, è possibile evitare l'avviso usando la parola chiave `new` nella definizione della classe derivata:  
  
 [!code-cs[csProgGuideInheritance#31](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_6.cs)]  
  
 L'uso della parola chiave `new` indica al compilatore che la definizione nasconde la definizione contenuta nella classe di base. Comportamento predefinito.  
  
## <a name="override-and-method-selection"></a>Override e selezione del metodo  
 Quando un metodo è denominato in una classe, il compilatore C# seleziona il metodo migliore per la chiamata se più metodi sono compatibili con la chiamata, ad esempio quando esistono due metodi con lo stesso nome e parametri compatibili con il parametro passato. I seguenti metodi sarebbero compatibili:  
  
 [!code-cs[csProgGuideInheritance#32](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_7.cs)]  
  
 Quando si chiama `DoWork` per un'istanza di `Derived`, il compilatore C# tenta per prima cosa di rendere la chiamata compatibile con le versioni di `DoWork` originariamente dichiarate in `Derived`. I metodi di override non vengono considerati come dichiarati per una classe, sono nuove implementazioni di un metodo dichiarato per una classe di base. Solo se il compilatore C# non è in grado di associare la chiamata al metodo a un metodo originale in `Derived`, tenterà di associare la chiamata a un metodo sottoposto a override con lo stesso nome e parametri compatibili. Ad esempio:  
  
 [!code-cs[csProgGuideInheritance#33](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_8.cs)]  
  
 Poiché la variabile `val` può essere convertita in un valore double in modo implicito, il compilatore C# chiama `DoWork(double)` anziché `DoWork(int)`. Questa situazione può essere evitata in due modi. Primo, evitare di dichiarare i nuovi metodi con lo stesso nome dei metodi virtuali. Secondo, è possibile indicare al compilatore C# di chiamare il metodo virtuale facendo in modo che esegua una ricerca nell'elenco dei metodi della classe di base eseguendo il cast dell'istanza di `Derived` a `Base`. Poiché il metodo è virtuale, verrà chiamata l'implementazione di `DoWork(int)` per `Derived`. Ad esempio:  
  
 [!code-cs[csProgGuideInheritance#34](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/versioning-with-the-override-and-new-keywords_9.cs)]  
  
 Per altri esempi di `new` e `override`, vedere [Sapere quando usare le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)
