---
title: Tipi di base | Guida per programmatori C#
description: Informazioni sui tipi di base (dati numerici, stringhe e oggetto) in tutti i programmi C#
keywords: .NET, .NET Core, C#
author: stevehoag
ms.author: shoag
ms.date: 10/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 95c686ba-ae4f-440e-8e94-0dbd6e04d11f
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 57c5524a18535778db337500b0a7e9013ce93519
ms.lasthandoff: 03/13/2017

---

# <a name="types-variables-and-values"></a>Tipi, variabili e valori  
C# è un linguaggio fortemente tipizzato. Ogni variabile e costante ha un tipo, così come ogni espressione che restituisce un valore. Ogni firma del metodo specifica un tipo per ogni parametro di input e per il valore restituito. La libreria di classi di .NET Framework definisce un set di tipi numerici predefiniti, nonché tipi più complessi che rappresentano un'ampia gamma di costrutti logici, ad esempio il file system, le connessioni di rete, le raccolte e le matrici di oggetti e le date. Un tipico programma C# usa tipi dalla libreria di classi e tipi definiti dall'utente che modellano i concetti che sono specifici al dominio del problema del programma.  
  
Le informazioni archiviate in un tipo possono includere quanto segue:  
  
-   Lo spazio di archiviazione richiesto da una variabile di tipo.  
  
-   I valori minimi e massimi che può rappresentare.  
  
-   I membri (metodi, campi, eventi e così via) in essa contenuti.  
  
-   Il tipo di base da cui eredita.  
  
-   Il percorso in cui viene allocata la memoria per le variabili in fase di esecuzione.  
  
-   I tipi di operazioni consentite.  
  
Il compilatore usa le informazioni sul tipo per assicurarsi che tutte le operazioni che vengono eseguite nel codice siano *indipendenti dai tipi*. Ad esempio, se si dichiara una variabile di tipo [int](https://msdn.microsoft.com/library/5kzh1b5w.aspx), il compilatore consente di usare la variabile anche in operazioni di addizione e sottrazione. Se si prova a eseguire le stesse operazioni su una variabile di tipo [bool](https://msdn.microsoft.com/library/c8f5xwh7.aspx), il compilatore genera un errore, come illustrato nell'esempio seguente:  
  
[!code-csharp[Indipendenza dai tipi](../../samples/snippets/csharp/concepts/basic-types/type-safety.cs)]  
  
> [!NOTE]  
>  Gli sviluppatori C e C++ devono tenere presente che in C#, [bool](https://msdn.microsoft.com/library/c8f5xwh7.aspx) non è convertibile in [int](https://msdn.microsoft.com/library/5kzh1b5w.aspx).  
  
Il compilatore incorpora le informazioni sul tipo nel file eseguibile come metadati. Common Language Runtime (CLR) usa i metadati in fase di esecuzione per garantire ulteriormente l'indipendenza dai tipi quando alloca e recupera la memoria.  

## <a name="specifying-types-in-variable-declarations"></a>Specifica dei tipi nelle dichiarazioni di variabile  
Quando si dichiara una variabile o costante in un programma, è necessario specificarne il tipo oppure usare la parola chiave [var](https://msdn.microsoft.com/library/bb383973.aspx) per consentire al compilatore di dedurre il tipo. L'esempio seguente illustra alcune dichiarazioni di variabili che usano entrambi i tipi numerici predefiniti e i tipi complessi definiti dall'utente:  
  
[!code-csharp[Dichiarazione della variabile](../../samples/snippets/csharp/concepts/basic-types/variable-declaration.cs)]  
  
I tipi di parametri del metodo e valori restituiti sono specificati nella firma del metodo. La firma seguente illustra un metodo che richiede un [int](https://msdn.microsoft.com/library/5kzh1b5w.aspx) come argomento di input e restituisce una stringa:  
  
[!code-csharp[Firma del metodo](../../samples/snippets/csharp/concepts/basic-types/method-signature.cs)]  
  
Una variabile dichiarata non può essere dichiarata di nuovo con un tipo nuovo e non è possibile assegnarle un valore che non è compatibile con il relativo tipo dichiarato. Ad esempio, non è possibile dichiarare una variabile [int](https://msdn.microsoft.com/library/5kzh1b5w.aspx) e assegnarvi il valore booleano [true](https://msdn.microsoft.com/library/06d3w013.aspx). I valori possono tuttavia essere convertiti in altri tipi, ad esempio quando vengono assegnati a variabili nuove o passati come argomenti di metodo. Una *conversione del tipo* che non causa la perdita di dati viene eseguita automaticamente dal compilatore. Una conversione che potrebbe causare la perdita di dati richiede un *cast* nel codice sorgente. 

Per altre informazioni, vedere [Cast e conversioni di tipi](https://msdn.microsoft.com/library/ms173105.aspx).
 
## <a name="built-in-types"></a>Tipi incorporati
Il linguaggio C# offre un set standard di tipi numerici predefiniti per rappresentare numeri interi, valori a virgola mobile, espressioni booleane, caratteri di testo, valori decimali e altri tipi di dati. Sono anche disponibili tipi **string** e **object** predefiniti. Questi possono essere usati in qualsiasi programma C#. Per altre informazioni sui tipi predefiniti, vedere [Tabelle di riferimento ai tipi](https://msdn.microsoft.com/library/1dhd7f2x.aspx).  
  
## <a name="custom-types"></a>Tipi personalizzati  
Usare i costrutti [struct](https://msdn.microsoft.com/library/ah19swz4.aspx), [class](https://msdn.microsoft.com/library/0b0thckt.aspx), [interface](https://msdn.microsoft.com/library/87d83y5b.aspx) e [enum](https://msdn.microsoft.com/library/sbbt4032.aspx) per creare tipi personalizzati. La libreria di classi di .NET Framework è una raccolta di tipi personalizzati offerti da Microsoft che è possibile usare nelle applicazioni. Per impostazione predefinita, i tipi usati più frequentemente nella libreria di classi sono disponibili in qualsiasi programma C#. Altri diventano disponibili solo quando si aggiunge in modo esplicito un riferimento di progetto all'assembly in cui sono definiti. Dopo che il compilatore avrà un riferimento all'assembly, è possibile dichiarare variabili (e costanti) dei tipi dichiarati in tale assembly in codice sorgente. Per altre informazioni, vedere [Libreria di classi .NET Framework](https://msdn.microsoft.com/library/gg145045(v=vs.110).aspx).  
  
## <a name="generic-types"></a>Tipi generici  
Un tipo può essere dichiarato con uno o più *parametri di tipo* che fungono da segnaposto per il tipo effettivo (*tipo concreto*) che il codice client specifica quando si crea un'istanza del tipo. Tali tipi sono definiti *tipi generici*. Ad esempio, il tipo @System.Collections.Generic.List%601 di .NET Framework ha un solo parametro a cui, per convenzione, viene assegnato il nome *T*. Quando si crea un'istanza del tipo, si specifica il tipo degli oggetti che verrà contenuto nell'elenco, ad esempio, string:  
  
[!code-csharp[Tipi generici](../../samples/snippets/csharp/concepts/basic-types/generic-type.cs)] 
  
L'uso del parametro di tipo rende possibile il riuso della stessa classe per contenere qualsiasi tipo di elemento, senza la necessità di convertire ogni elemento in [object](https://msdn.microsoft.com/library/9kkx3h3c.aspx). Le classi di raccolte generiche sono dette *raccolte fortemente tipizzate* perché il compilatore conosce il tipo specifico di elementi della raccolta e può generare un errore in fase di compilazione se, ad esempio, si prova ad aggiungere un numero intero all'oggetto `strings` nell'esempio precedente. Per altre informazioni, vedere [Generics](programming-guide/generics/index.md). 

## <a name="implicit-types-anonymous-types-and-tuple-types"></a>Tipi impliciti, tipi anonimi e tipi di tupla  
Come indicato in precedenza, è possibile digitare una variabile locale in modo implicito usando la parola chiave [var](https://msdn.microsoft.com/library/bb383973.aspx). A tale variabile viene comunque assegnato un tipo in fase di compilazione, ma il tipo viene specificato dal compilatore. Per altre informazioni, vedere [Variabili locali tipizzate in modo implicito](https://msdn.microsoft.com/library/bb384061.aspx).  
  
In alcuni casi non è consigliabile creare un tipo denominato per set semplici di valori correlati che non si intende archiviare o passare fuori dai limiti del metodo. A questo scopo è possibile creare *tipi anonimi*. Per altre informazioni, vedere [Tipi anonimi](https://msdn.microsoft.com/library/bb397696.aspx).

È prassi comune voler restituire più valori da un metodo. È possibile creare *tipi di tupla* che restituiscono più valori in una singola chiamata al metodo. Per altre informazioni, vedere [Tuple](tuples.md)

## <a name="the-common-type-system"></a>Sistema dei tipi comuni  
È importante capire due punti fondamentali sul sistema dei tipi in .NET Framework:  
  
-   Il tipo supporta il principio di ereditarietà. I tipi possono derivare da altri tipi, denominati *tipi di base*. Il tipo derivato eredita (con alcune limitazioni) metodi, proprietà e altri membri del tipo di base. Il tipo di base può a sua volta derivare da un altro tipo, nel quale caso il tipo derivato eredita i membri di entrambi i tipi di base nella gerarchia di ereditarietà. Tutti i tipi, inclusi i tipi numerici predefiniti, ad esempio @System.Int32 (parola chiave C#: `int`), derivano in definitiva da un unico tipo di base, ovvero @System.Object (parola chiave C#: `object`). Questa gerarchia di tipi unificati viene chiamata [Common Type System](../standard/common-type-system.md) (CTS). Per altre informazioni sull'ereditarietà in C#, vedere [Ereditarietà](https://msdn.microsoft.com/library/ms173149.aspx).  
  
-   Ogni tipo in CTS è definito come *tipo di valore* o *tipo di riferimento*. Ciò include tutti i tipi personalizzati nella libreria di classi .NET Framework, nonché i tipi definiti dall'utente. I tipi definiti tramite la parola chiave [struct](https://msdn.microsoft.com/library/ah19swz4.aspx) sono tipi di valore e tutti i tipi numerici predefiniti sono tipi **struct**. Per altre informazioni sui tipi di valori, vedere [Struct](structs.md). I tipi definiti tramite la parola chiave [class](https://msdn.microsoft.com/library/0b0thckt.aspx) sono tipi di riferimento. Per altre informazioni sui tipi di riferimento, vedere [Classi](classes.md). I tipi di riferimento e i tipi di valore hanno regole diverse e un comportamento diverso in fase di esecuzione.
 
  
## <a name="see-also"></a>Vedere anche
[Struct](structs.md)

[Classi](classes.md)

