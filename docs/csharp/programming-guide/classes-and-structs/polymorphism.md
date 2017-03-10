---
title: "Polimorfismo (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "linguaggio C#, polimorfismo"
  - "polimorfismo [C#]"
ms.assetid: 086af969-29a5-4ce8-a993-0b7d53839dab
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# Polimorfismo (Guida per programmatori C#)
Il polimorfismo è spesso definito il terzo pilastro della programmazione orientata a oggetti, dopo l'incapsulamento e l'ereditarietà.  Polimorfismo è una parola che deriva dal greco e significa "multiforme". Il polimorfismo presenta due aspetti distinti:  
  
-   In fase di esecuzione, oggetti di una classe derivata possono essere trattati come oggetti di una classe base in posizioni quali parametri del metodo e raccolte o matrici.  In questo caso, il tipo dichiarato dell'oggetto non è più identico al tipo in fase di esecuzione.  
  
-   Le classi base possono definire e implementare *metodi* [virtuali](../../../csharp/language-reference/keywords/virtual.md) e le classi derivate possono eseguirne l'[override](../../../csharp/language-reference/keywords/override.md), ovvero ne forniscono una propria definizione e implementazione.  Durante la fase di esecuzione, quando il codice client chiama il metodo, CLR cerca il tipo in fase di esecuzione dell'oggetto e richiama quell'override del metodo virtuale.  Quindi, nel codice sorgente è possibile chiamare un metodo su una classe base, causando l'esecuzione di una versione di tale metodo definita in una classe derivata.  
  
 I metodi virtuali consentono di usare gruppi di oggetti correlati in modo uniforme.  Si supponga ad esempio di avere un'applicazione di disegno che consenta a un utente di creare vari tipi di forme in un'area di disegno.  In fase di compilazione non è possibile sapere i tipi specifici di forme che l'utente creerà.  L'applicazione deve tuttavia tenere traccia di tutti i vari tipi di forme create e deve aggiornarli in risposta alle azioni del mouse dell'utente.  È possibile usare il polimorfismo per risolvere questo problema in due passaggi di base:  
  
1.  Creare una gerarchia di classi nella quale ogni classe della forma specifica deriva da una classe base comune.  
  
2.  Usare un metodo virtuale per richiamare il metodo adatto su qualsiasi classe derivata tramite una sola chiamata al metodo della classe base.  
  
 Prima di tutto, creare una classe base denominata `Shape` e delle classi derivate quali `Rectangle`, `Circle` e `Triangle`.  Definire nella classe `Shape` un metodo virtuale denominato `Draw` ed eseguirne l'override in ogni classe derivata per disegnare la particolare forma che la classe rappresenta.  Creare un oggetto `List<Shape>` e aggiungervi un cerchio, un triangolo e un rettangolo.  Per aggiornare l'area di disegno, usare un ciclo [foreach](../../../csharp/language-reference/keywords/foreach-in.md) per scorrere l'elenco e chiamare il metodo `Draw` su ogni oggetto `Shape` nell'elenco.  Anche se ogni oggetto nella lista è dichiarato di tipo `Shape`, sarà il tipo della fase di esecuzione \(la versione del metodo di cui è stato eseguito l'override in ogni classe derivata\) che verrà richiamato.  
  
 [!code-cs[csProgGuideInheritance#50](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_1.cs)]  
  
 In C\# ogni tipo è polimorfico perché tutti i tipi, incluso i tipi definiti dall'utente, ereditano da <xref:System.Object>.  
  
## Panoramica sul polimorfismo  
  
### Membri virtuali  
 Quando una classe derivata eredita da una classe base, ottiene tutti i metodi, i campi, le proprietà e gli eventi della classe base.  Il progettista della classe derivata può scegliere se:  
  
-   eseguire l'override di membri virtuali nella classe base;  
  
-   ereditare il metodo della classe di base più vicino senza eseguirne l'override;  
  
-   definire la nuova implementazione non virtuale di quei membri che nascondono le implementazioni della classe base.  
  
 Una classe derivata può eseguire l'override di un membro della classe base solo se quest'ultimo è dichiarato come [virtuale](../../../csharp/language-reference/keywords/virtual.md) o [astratto](../../../csharp/language-reference/keywords/abstract.md).  Il membro derivato deve usare la parola chiave [override](../../../csharp/language-reference/keywords/override.md) per indicare esplicitamente che il metodo deve partecipare nella chiamata virtuale.  Nel codice seguente ne viene illustrato un esempio:  
  
 [!code-cs[csProgGuideInheritance#20](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_2.cs)]  
  
 A differenza di metodi, proprietà, eventi e indicizzatori, i campi non possono essere virtuali.  Quando una classe derivata esegue l'override di un membro virtuale, quest'ultimo viene chiamato anche nel caso in cui si acceda a un'istanza di tale classe come istanza della classe base.  Nel codice seguente ne viene illustrato un esempio:  
  
 [!code-cs[csProgGuideInheritance#21](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_3.cs)]  
  
 Metodi virtuali e proprietà consentono alle classi derivate di estendere una classe base senza dover usare l'implementazione della classe base di un metodo.  Per altre informazioni, vedere [Controllo delle versioni con le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md).  Un'interfaccia fornisce un'altra modalità per definire un metodo o un insieme di metodi la cui implementazione è lasciata alle classi derivate.  Per altre informazioni, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
### Nascondere un membro di una classe base con nuovi membri  
 Se si vuole che il membro derivato abbia lo stesso nome di un membro in una classe di base, ma non si vuole che partecipi in chiamata virtuale, è possibile usare la parola chiave [new](../../../csharp/language-reference/keywords/new.md).  La parola chiave `new` viene inserita prima del tipo restituito di un membro di classe che viene sostituito.  Nel codice seguente ne viene illustrato un esempio:  
  
 [!code-cs[csProgGuideInheritance#18](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_4.cs)]  
  
 I membri nascosti della classe base sono comunque accessibili dal codice client se si esegue il cast di un'istanza della classe derivata in un'istanza della classe base.  Ad esempio:  
  
 [!code-cs[csProgGuideInheritance#19](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_5.cs)]  
  
### Impedire alle classi derivate di eseguire l'override di membri virtuali  
 I membri virtuali rimangono sempre tali, indipendentemente dal numero di classi dichiarate fra i membri virtuali e la classe in cui è stato originariamente dichiarato il membro virtuale.  Se nella classe A è dichiarato un membro virtuale, la classe B deriva da A e la classe C deriva da B, la classe C erediterà il membro virtuale e potrà eseguirne l'override, indipendentemente dal fatto che nella classe B sia dichiarato un override per tale membro.  Nel codice seguente ne viene illustrato un esempio:  
  
 [!code-cs[csProgGuideInheritance#22](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_6.cs)]  
  
 Una classe derivata può interrompere l'ereditarietà virtuale dichiarando un override come [sealed](../../../csharp/language-reference/keywords/sealed.md).  A tale scopo, è necessario inserire la parola chiave `sealed` prima della parola chiave `override` nella dichiarazione del membro della classe.  Nel codice seguente ne viene illustrato un esempio:  
  
 [!code-cs[csProgGuideInheritance#24](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_7.cs)]  
  
 Nell'esempio riportato in precedenza, il metodo `DoWork` non è più virtuale per nessuna classe derivata da C.  È ancora virtuale per le istanze di C, anche se ne è stato eseguito il cast nel tipo B o A.  I metodi sealed possono essere sostituiti da classi derivate tramite la parola chiave `new`, come illustrato nell'esempio seguente:  
  
 [!code-cs[csProgGuideInheritance#25](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_8.cs)]  
  
 In questo caso, se viene chiamato `DoWork` su D usando una variabile di tipo D, verrà chiamato il nuovo `DoWork`.  Se per accedere a un'istanza di D viene usata una variabile di tipo C, B o A, una chiamata a `DoWork` seguirà le regole dell'ereditarietà virtuale, indirizzando queste chiamate all'implementazione di `DoWork` sulla classe C.  
  
### Accedere a membri virtuali di una classe base dalle classi derivate  
 Una classe derivata che ha sostituito un metodo o una proprietà, o ne ha eseguito l'override, può ancora accedere al metodo o alla proprietà sulla classe base usando la parola chiave base.  Nel codice seguente ne viene illustrato un esempio:  
  
 [!code-cs[csProgGuideInheritance#26](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/polymorphism_9.cs)]  
  
 Per altre informazioni, vedere [base](../../../csharp/language-reference/keywords/base.md).  
  
> [!NOTE]
>  Nell'implementazione dei membri virtuali è consigliabile l'uso della parola chiave `base` per le chiamate all'implementazione della classe base di tali membri.  In questo modo, nella classe derivata sarà possibile definire la sola implementazione del comportamento specifico per tale classe.  Se l'implementazione della classe base non viene chiamata, spetterà alla classe derivata rendere il proprio comportamento compatibile con quello della classe base.  
  
## Argomenti della sezione  
  
-   [Controllo delle versioni con le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)  
  
-   [Sapere quando utilizzare le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)  
  
-   [Procedura: eseguire l'override del metodo ToString](../../../csharp/programming-guide/classes-and-structs/how-to-override-the-tostring-method.md)  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Ereditarietà](../../../csharp/programming-guide/classes-and-structs/inheritance.md)   
 [Classi e membri delle classi astratte e sealed](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)   
 [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Indicizzatori](../../../csharp/programming-guide/indexers/index.md)   
 [Tipi](../../../csharp/programming-guide/types/index.md)