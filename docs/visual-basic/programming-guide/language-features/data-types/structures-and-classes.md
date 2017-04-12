---
title: Strutture e classi (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- classes [Visual Basic], vs. structures
- structures
- classes [Visual Basic]
- structures, compared to classes
- structures, structure variables
- structure variables
ms.assetid: a221e74a-ffcf-4bdc-a0f6-a088a9bf26cc
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e7402ec0fcfc279470d39a4919d3b5ec8b5d9dff
ms.lasthandoff: 03/13/2017

---
# <a name="structures-and-classes-visual-basic"></a>Strutture e classi (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Unisce la sintassi per le strutture e classi, con il risultato che entrambe le entità supportano la maggior parte delle stesse funzionalità. Tuttavia, esistono anche differenze importanti tra strutture e classi.  
  
 Presentano il vantaggio di essere tipi di riferimento, passando un riferimento è più efficiente passare una variabile di struttura con tutti i relativi dati. D'altra parte, le strutture non richiedono l'allocazione di memoria nell'heap globale.  
  
 Poiché non è possibile ereditare da una struttura, utilizzare strutture solo per gli oggetti che non è necessario essere esteso. Utilizzare le strutture quando l'oggetto che si desidera creare ha una dimensione di un'istanza ridotta e prendere in considerazione le caratteristiche delle classi e strutture di prestazioni.  
  
## <a name="similarities"></a>Analogie  
 Classi e strutture sono simili per i seguenti aspetti:  
  
-   Entrambi sono *contenitore* tipi, vale a dire che contengono altri tipi come membri.  
  
-   Entrambi sono membri, che possono includere costruttori, metodi, proprietà, campi, costanti, enumerazioni, eventi e gestori di eventi. Tuttavia, non confondere questi membri con il dichiarato *elementi* di una struttura.  
  
-   I membri di entrambe possono avere livelli di accesso personalizzati. Ad esempio, è possibile dichiarare un membro `Public` e un altro `Private`.  
  
-   Entrambi possono implementare interfacce.  
  
-   Entrambe possono avere condivisi costruttori, con o senza parametri.  
  
-   Entrambe possono esporre un *predefiniti delle proprietà*, a condizione che accetti almeno un parametro.  
  
-   Entrambe possono dichiarare e generare eventi e sia possibile dichiarare i delegati.  
  
## <a name="differences"></a>Differenze  
 Classi e strutture sono diversi per le seguenti indicazioni:  
  
-   Le strutture sono *i tipi di valore*; le classi sono *tipi di riferimento*. Una variabile di un tipo di struttura contiene i dati della struttura, anziché contenente un riferimento a dati come un tipo di classe.  
  
-   Strutture di utilizzano l'allocazione dello stack; le classi utilizzano l'allocazione di heap.  
  
-   Tutti gli elementi di struttura sono `Public` per impostazione predefinita; classe variabili e costanti sono `Private` per impostazione predefinita, mentre altri membri della classe sono `Public` per impostazione predefinita. Questo comportamento per i membri di classe fornisce la compatibilità con il sistema di Visual Basic 6.0 di valori predefiniti.  
  
-   Una struttura deve contenere almeno uno non personalizzato non condiviso di variabile o condiviso, elemento di un evento; una classe può essere completamente vuota.  
  
-   Elementi di struttura non possono essere dichiarati come `Protected`; i membri di classe possono.  
  
-   Una routine di struttura può gestire eventi solo se è un [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) `Sub` procedura e solo per mezzo di [AddHandler (istruzione)](../../../../visual-basic/language-reference/statements/addhandler-statement.md); qualsiasi routine di classe può gestire gli eventi utilizzando il [gestisce](../../../../visual-basic/language-reference/statements/handles-clause.md) (parola chiave) o `AddHandler` istruzione. Per ulteriori informazioni, vedere [eventi](../../../../visual-basic/programming-guide/language-features/events/index.md).  
  
-   Dichiarazioni di variabili di struttura non possono specificare inizializzatori o dimensioni iniziali per le matrici. dichiarazioni di variabili di classe possono.  
  
-   Le strutture ereditano in modo implicito dalla <xref:System.ValueType?displayProperty=fullName>classe e non può ereditare da qualsiasi altro tipo; le classi possono ereditare da qualsiasi classe o una classe diversa da <xref:System.ValueType?displayProperty=fullName>.</xref:System.ValueType?displayProperty=fullName> </xref:System.ValueType?displayProperty=fullName>  
  
-   Strutture non sono ereditabili; le classi sono.  
  
-   Le strutture non vengono mai terminate, common language runtime (CLR) non chiama mai il <xref:System.Object.Finalize%2A>metodo in una struttura; le classi vengono terminate dal garbage collector (GC), che chiama <xref:System.Object.Finalize%2A>su una classe quando rilevato che non sono presenti riferimenti attivi.</xref:System.Object.Finalize%2A> </xref:System.Object.Finalize%2A>  
  
-   Una struttura non richiede un costruttore. esegue una classe.  
  
-   Strutture possono disporre di costruttori non condivisi solo se hanno parametri. le classi possono avere li con o senza parametri.  
  
 Ogni struttura dispone di un costruttore pubblico senza parametri. Questo costruttore inizializza gli elementi di dati della struttura sui valori predefiniti. È possibile ridefinire il problema.  
  
## <a name="instances-and-variables"></a>Istanze e variabili  
 Poiché le strutture sono tipi di valore, ogni variabile di struttura in modo permanente è associato a un'istanza di struttura individuale. Tuttavia, le classi sono tipi di riferimento e una variabile oggetto può fare riferimento a diverse istanze di classi in momenti diversi. Questa differenza influisce sull'utilizzo di strutture e classi nei modi seguenti:  
  
-   **Inizializzazione.** Una variabile di struttura include implicitamente un'inizializzazione degli elementi utilizzando il costruttore della struttura senza parametri. Di conseguenza, `Dim s As struct1` equivale a `Dim s As struct1 = New struct1()`.  
  
-   **Assegnazione di variabili.** Quando si assegna una variabile di struttura a un altro, o passa un'istanza della struttura a un argomento di routine, i valori correnti di tutti gli elementi variabile vengono copiati nella nuova struttura. Quando si assegna una variabile oggetto a un altro o si passa una variabile oggetto a una routine, viene copiato solo il puntatore di riferimento.  
  
-   **Assegnare il valore Nothing.** È possibile assegnare il valore [nulla](../../../../visual-basic/language-reference/nothing.md) a una struttura variabile, ma l'istanza continua a essere associato alla variabile. È comunque possibile chiamarne i metodi e accedere ai relativi elementi di dati, anche se gli elementi variabile vengano reinizializzati dall'assegnazione.  
  
     Al contrario, se si imposta una variabile oggetto su `Nothing`, si dissocia tale variabile da qualsiasi istanza della classe e non può accedere ad alcun membro tramite la variabile finché non verrà assegnato un'altra istanza.  
  
-   **Più istanze.** Una variabile oggetto può disporre di istanze di classe diversi in momenti diversi, e diverse variabili di oggetto possono fare riferimento alla stessa istanza di classe nello stesso momento. Le modifiche apportate ai valori dei membri della classe influiscono su tali membri quando si accede tramite un'altra variabile che punta alla stessa istanza.  
  
     Elementi della struttura, tuttavia, sono isolati all'interno della relativa istanza. In base ai valori non vengono riflesse in altre variabili di struttura, anche in altre istanze dello stesso `Structure` dichiarazione.  
  
-   **Uguaglianza.** Test di uguaglianza di due strutture deve essere eseguito con un elemento per elemento test. Due variabili di oggetto possono essere confrontate utilizzando il <xref:System.Object.Equals%2A>(metodo).</xref:System.Object.Equals%2A> <xref:System.Object.Equals%2A>indica se le due variabili puntano alla stessa istanza.</xref:System.Object.Equals%2A>  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Tipi di dati compositi](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Strutture](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Strutture e altri elementi di programmazione](../../../../visual-basic/programming-guide/language-features/data-types/structures-and-other-programming-elements.md)   
 [Oggetti e classi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
