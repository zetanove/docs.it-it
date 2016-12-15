---
title: "Utilizzo di costruttori (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "costruttori [C#], informazioni sui costruttori"
ms.assetid: 464253b2-fd5d-469a-836d-df0fdf2a43f7
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Utilizzo di costruttori (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando [classe](../../../csharp/language-reference/keywords/class.md) o [struttura](../../../csharp/language-reference/keywords/struct.md) viene creato, il costruttore viene chiamato.  I costruttori hanno lo stesso nome della classe o della struttura e in genere inizializzano i membri dati del nuovo oggetto.  
  
 Nell'esempio seguente viene definita una classe denominata `Taxi` con un costruttore semplice.  Viene quindi creata un'istanza di questa classe con l'operatore [new](../../../csharp/language-reference/keywords/new.md).  Il costruttore `Taxi` viene richiamato dall'operatore `new` immediatamente dopo l'allocazione della memoria per il nuovo oggetto.  
  
 [!code-cs[csProgGuideObjects#53](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_1.cs)]  
  
 I *costruttori predefiniti*, ossia che non accettano parametri,  vengono richiamati ogni volta che viene creata un'istanza di un oggetto utilizzando l'operatore `new` e non vengono forniti argomenti a `new`.  Per ulteriori informazioni, vedere [Costruttori di istanze](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md).  
  
 A meno che non siano [statiche](../../../csharp/language-reference/keywords/static.md), le classi senza costruttori ricevono un costruttore predefinito pubblico dal compilatore C\# per consentire la creazione di istanze.  Per ulteriori informazioni, vedere [Classi statiche e membri di classi statiche](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
 È possibile impedire la creazione di istanze di una classe rendendo privato il costruttore, come riportato di seguito:  
  
 [!code-cs[csProgGuideObjects#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_2.cs)]  
  
 Per ulteriori informazioni, vedere [Costruttori privati](../../../csharp/programming-guide/classes-and-structs/private-constructors.md).  
  
 I costruttori per i tipi [struct](../../../csharp/language-reference/keywords/struct.md) sono simili ai costruttori di classi, con la differenza che i tipi `structs` non possono contenere un costruttore predefinito esplicito perché ne viene automaticamente fornito uno dal compilatore.  Il costruttore inizializza ogni campo di `struct` in base ai valori predefiniti.  Per ulteriori informazioni, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  Questo costruttore predefinito viene tuttavia richiamato solo se viene creata un'istanza di `struct` con `new`.  Nel codice seguente viene ad esempio utilizzato il costruttore predefinito per <xref:System.Int32>, in modo da avere la certezza che venga inizializzato l'intero:  
  
```  
int i = new int();  
Console.WriteLine(i);  
```  
  
 Il codice seguente comporta tuttavia la generazione di un errore del compilatore in quanto non viene utilizzato l'oggetto `new` e in quanto viene eseguito un tentativo di utilizzare un oggetto non inizializzato.  
  
```  
int i;  
Console.WriteLine(i);  
```  
  
 In alternativa, gli oggetti basati su `structs` \(inclusi tutti i tipi numerici incorporati\) possono essere inizializzati o assegnati e quindi utilizzati, come illustrato nell'esempio seguente:  
  
```  
int a = 44;  // Initialize the value type...  
int b;  
b = 33;      // Or assign it before using it.  
Console.WriteLine("{0}, {1}", a, b);  
```  
  
 In questo caso non è necessario chiamare il costruttore predefinito per ottenere un tipo di valore.  
  
 Sia le classi che gli oggetti `structs` possono definire costruttori che accettano parametri.  I costruttori che accettano parametri devono essere chiamati tramite un'istruzione `new` o un'istruzione [base](../../../csharp/language-reference/keywords/base.md).  Le classi e gli oggetti `structs` possono inoltre definire più costruttori e non devono necessariamente definire un costruttore predefinito.  Ad esempio:  
  
 [!code-cs[csProgGuideObjects#54](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_3.cs)]  
  
 Per creare questa classe, è possibile utilizzare una delle seguenti istruzioni:  
  
 [!code-cs[csProgGuideObjects#55](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_4.cs)]  
  
 Un costruttore può utilizzare la parola chiave `base` per chiamare il costruttore di una classe base.  Ad esempio:  
  
 [!code-cs[csProgGuideObjects#56](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_5.cs)]  
  
 In questo esempio il costruttore della classe base viene chiamato prima dell'esecuzione del blocco per il costruttore.  La parola chiave `base` può essere utilizzata con o senza parametri.  Gli eventuali parametri del costruttore possono essere utilizzati come parametri per `base` oppure come parte di un'espressione.  Per ulteriori informazioni, vedere [base](../../../csharp/language-reference/keywords/base.md).  
  
 Se in una classe derivata non viene chiamato in modo esplicito il costruttore della classe di base mediante la parola chiave `base`, verrà chiamato in modo implicito l'eventuale costruttore predefinito disponibile.  Le seguenti dichiarazioni di costruttori sono quindi in realtà identiche:  
  
 [!code-cs[csProgGuideObjects#58](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_6.cs)]  
  
 [!code-cs[csProgGuideObjects#57](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_7.cs)]  
  
 Se una classe di base non include un costruttore predefinito, la classe derivata deve effettuare una chiamata esplicita a un costruttore di base utilizzando `base`.  
  
 Un costruttore può richiamare un altro costruttore nello stesso oggetto utilizzando la parola chiave [this](../../../csharp/language-reference/keywords/this.md).  Analogamente a `base`, è possibile utilizzare `this` con o senza parametri. Gli eventuali parametri del costruttore sono disponibili come parametri per `this` o come parte di un'espressione.  È ad esempio possibile riscrivere il secondo costruttore dell'esempio precedente utilizzando la parola chiave `this`:  
  
 [!code-cs[csProgGuideObjects#59](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_8.cs)]  
  
 Utilizzando la parola chiave `this` riportata nell'esempio precedente, verrà chiamato questo costruttore:  
  
 [!code-cs[csProgGuideObjects#60](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-constructors_9.cs)]  
  
 I costruttori possono essere contrassegnati come [public](../../../csharp/language-reference/keywords/public.md), [private](../../../csharp/language-reference/keywords/private.md), [protected](../../../csharp/language-reference/keywords/protected.md), [internal](../../../csharp/language-reference/keywords/internal.md) o `protected` `internal`.  Questi modificatori definiscono le modalità di costruzione della classe per gli utenti della classe.  Per ulteriori informazioni, vedere [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
 Un costruttore può essere dichiarato statico mediante la parola chiave [static](../../../csharp/language-reference/keywords/static.md).  I costruttori statici vengono chiamati automaticamente immediatamente prima dell'accesso a qualsiasi campo statico e vengono in genere utilizzati per inizializzare i membri di classi statiche.  Per ulteriori informazioni, vedere [Costruttori statici](../../../csharp/programming-guide/classes-and-structs/static-constructors.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)