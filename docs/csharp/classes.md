---
title: Classi | Guida per programmatori C#
description: Informazioni sui tipi di classe e su come crearli
keywords: .NET, .NET Core, C#
author: BillWagner
ms.author: wiwagn
ms.date: 10/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 95c686ba-ae4f-440e-8e94-0dbd6e04d11f
ms.translationtype: Human Translation
ms.sourcegitcommit: a5ed524a1b17f7be8903f998cbd732594faab831
ms.openlocfilehash: f2cfeac321860a609c21046818c36fbc6aa3c636
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---

# <a name="classes"></a>Classi
Una *classe* è un costrutto che consente di creare tipi personalizzati raggruppando insieme variabili di altri tipi, metodi e eventi. Una classe è simile a un progetto. Definisce i dati e il comportamento di un tipo. Se la classe non è dichiarata come statica, il codice client può usarla creando *oggetti* o *istanze* che vengono assegnate a una variabile. La variabile rimane in memoria fino a quando tutti i riferimenti non escono dall'ambito. In questa fase, CLR la contrassegna come idonea per Garbage Collection. Se la classe viene dichiarata come [statica](https://msdn.microsoft.com/library/98f28cdx.aspx), viene mantenuta in memoria solo una copia e il codice client può accedervi solo tramite la classe stessa, non con una *variabile di istanza*. Per altre informazioni, vedere [Classi statiche e membri di classi statiche](https://msdn.microsoft.com/library/79b3xss3.aspx).  

## <a name="reference-types"></a>Tipi di riferimento  
Un tipo definito come [classe](https://msdn.microsoft.com/library/0b0thckt.aspx) è un *tipo di riferimento*. In fase di esecuzione, quando si dichiara una variabile di un tipo di riferimento, la variabile contiene il valore [null](https://msdn.microsoft.com/library/edakx9da.aspx) fino a quando non si crea in modo esplicito un'istanza dell'oggetto usando l'operatore [new](https://msdn.microsoft.com/library/51y09td4.aspx), o fino a quando non gli viene assegnato un oggetto creato in un altro posto tramite [new](https://msdn.microsoft.com/library/51y09td4.aspx), come illustrato nell'esempio seguente:  

[!code-csharp[Tipi di riferimenti](../../samples/snippets/csharp/concepts/classes/reference-type.cs)]
  
Quando viene creato l'oggetto, la memoria viene allocata nell'heap gestito e la variabile mantiene solo un riferimento al percorso dell'oggetto. I tipi nell'heap gestito richiedono un overhead quando vengono allocati e recuperati dalla funzionalità di gestione automatica della memoria di CLR, nota come *Garbage Collection*. La Garbage Collection è tuttavia anche altamente ottimizzata e, nella maggior parte degli scenari, non causa un problema di prestazioni. Per altre informazioni sulla Garbage Collection, vedere [Gestione automatica della memoria e Garbage Collection](../standard/garbage-collection/gc.md).  
  
I tipi di riferimenti supportano completamente l'*ereditarietà*, una caratteristica fondamentale nella programmazione orientata a oggetti. Quando si crea una classe, è possibile ereditare da qualsiasi altra interfaccia o classe che non è definita come [sealed](https://msdn.microsoft.com/library/88c54tsw.aspx), e altre classi possono ereditare dalla classe ed eseguire l'override dei metodi virtuali. Per altre informazioni, vedere [Ereditarietà](https://msdn.microsoft.com/library/ms173149.aspx).

## <a name="declaring-classes"></a>Dichiarazione di classi  
Le classi vengono dichiarate usando la parola chiave [class](https://msdn.microsoft.com/library/0b0thckt.aspx), come illustrato nell'esempio seguente:  
  
[!code-csharp[Dichiarazione di classi](../../samples/snippets/csharp/concepts/classes/declaring-classes.cs)]  
  
La parola chiave **class** è preceduta dal modificatore di accesso. Poiché in questo caso viene usata la parola chiave [public](https://msdn.microsoft.com/library/yzh058ae.aspx), chiunque può creare oggetti da questa classe. Il nome della classe segue la parola chiave **class**. Il resto della definizione è il corpo della classe, in cui vengono definiti il comportamento e i dati. I campi, le proprietà, i metodi e gli eventi in una classe vengono collettivamente definiti *membri della classe*.  
  
## <a name="creating-objects"></a>Creazione di oggetti  
Una classe definisce un tipo di oggetto, ma non è un oggetto. Un oggetto è un'entità concreta ed è basato su una classe. Talvolta si fa riferimento all'oggetto come istanza di una classe.  
  
Gli oggetti possono essere creati tramite la parola chiave [new](https://msdn.microsoft.com/library/51y09td4.aspx) seguita dal nome della classe su cui si baserà l'oggetto, nel modo seguente:  
  
[!code-csharp[Creazione di oggetti](../../samples/snippets/csharp/concepts/classes/creating-objects.cs)]   
  
Quando viene creata un'istanza di una classe, viene passato al programmatore un riferimento all'oggetto. Nell'esempio precedente, `object1` è un riferimento a un oggetto basato su `Customer`. Questo riferimento indica il nuovo oggetto, ma non contiene i dati dell'oggetto. Infatti, è possibile creare un riferimento all'oggetto senza creare un oggetto:  
  
[!code-csharp[Creazione di oggetti](../../samples/snippets/csharp/concepts/classes/creating-objects2.cs)]  
  
Non è consigliabile creare riferimenti a oggetti come questo che non fanno riferimento a un oggetto reale perché il tentativo di accedere a un oggetto tramite tale riferimento avrà esito negativo in fase di esecuzione. Tuttavia, tale riferimento può essere creato per fare riferimento a un oggetto, creando un nuovo oggetto oppure assegnandolo a un oggetto esistente, come illustrato di seguito:  
  
[!code-csharp[Creazione di oggetti](../../samples/snippets/csharp/concepts/classes/creating-objects3.cs)]  
  
Questo codice crea due riferimenti a oggetti che fanno entrambi riferimento allo stesso oggetto. Tutte le modifiche effettuate all'oggetto tramite `object3` si rifletteranno tuttavia nei successivi usi di `object4`. Poiché gli oggetti che si basano su classi vengono indicati tramite riferimenti, le classi sono note come tipi di riferimento.  
  
## <a name="class-inheritance"></a>Ereditarietà delle classi  
L'ereditarietà si ottiene usando una *derivazione*, vale a dire che una classe viene dichiarata usando una *classe di base* da cui eredita dati e comportamento. Una classe di base viene specificata tramite l'aggiunta di due punti e il nome della classe di base dopo il nome della classe derivata, nel modo seguente:  
  
[!code-csharp[Ereditarietà](../../samples/snippets/csharp/concepts/classes/inheritance.cs)]  
  
Quando una classe dichiara una classe di base, eredita tutti i membri della classe di base, a eccezione dei costruttori.  
  
Diversamente da C++, una classe di C# può ereditare direttamente solo da una classe di base. Tuttavia, poiché una classe di base può ereditare da un'altra classe, una classe può ereditare indirettamente più classi di base. Una classe può anche implementare direttamente più di un'interfaccia. Per altre informazioni, vedere [Interfacce](programming-guide/interfaces/index.md).  
  
Una classe può essere dichiarata come [astratta](https://msdn.microsoft.com/library/sf985hc5.aspx). Una classe astratta contiene metodi astratti che hanno una definizione di firma, ma senza implementazione. Non è possibile creare un'istanza di classi astratte. Le classi astratte possono essere usate solo tramite classi derivate che implementano i metodi astratti. Al contrario, una classe [sealed](https://msdn.microsoft.com/library/88c54tsw.aspx) non consente ad altre classi di derivare da tale classe. Per altre informazioni, vedere [Classi e membri delle classi astratte e sealed](https://msdn.microsoft.com/library/ms173150.aspx).  
  
Le definizioni di classe possono essere suddivise tra file di origine diversa. Per altre informazioni, vedere [Definizioni di classi parziali](https://msdn.microsoft.com/library/wa80x488.aspx).  
  
 
## <a name="example"></a>Esempio
Nell'esempio seguente vengono definiti una classe pubblica che contiene un singolo campo, un metodo e un metodo speciale denominato costruttore. Per altre informazioni, vedere [Costruttori](https://msdn.microsoft.com/library/ace5hbzh.aspx). Viene quindi creata un'istanza alla classe con la parola chiave **new**.

[!code-csharp[Esempio di classe](../../samples/snippets/csharp/concepts/classes/class-example.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
Per altre informazioni, vedere le [specifiche del linguaggio C#](https://msdn.microsoft.com/library/ms228593.aspx). La specifica del linguaggio costituisce il riferimento ufficiale principale per la sintassi e l'uso di C#.
  
## <a name="see-also"></a>Vedere anche  
[Guida per programmatori C#](https://msdn.microsoft.com/library/67ef8sbd.aspx)   
[Polimorfismo](https://msdn.microsoft.com/library/ms173152.aspx)   
[Membri di classi e struct](https://msdn.microsoft.com/library/ms173113.aspx)   
[Metodi di classi e struct](https://msdn.microsoft.com/library/ms173114.aspx)   
[Costruttori](https://msdn.microsoft.com/library/ace5hbzh.aspx)   
[Finalizzatori](https://msdn.microsoft.com/library/66x5fx1b.aspx)   
[Oggetti](https://msdn.microsoft.com/library/ms173110.aspx)


