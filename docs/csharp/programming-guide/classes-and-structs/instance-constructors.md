---
title: "Costruttori di istanze (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "costruttori [C#], costruttori di istanza"
  - "costruttori di istanze [C#]"
ms.assetid: 24663779-c1e5-4af4-a942-ca554e4c542d
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# Costruttori di istanze (Guida per programmatori C#)
I costruttori di istanza sono utilizzati per creare e inizializzare qualsiasi variabile membro di istanza quando si utilizza l'espressione [new](../../../csharp/language-reference/keywords/new.md) per creare un oggetto di una [classe](../../../csharp/language-reference/keywords/class.md).  Per inizializzare una classe [statica](../../../csharp/language-reference/keywords/static.md) o variabili statiche in una classe non statica, è necessario definire un costruttore statico.  Per ulteriori informazioni, vedere [Costruttori statici](../../../csharp/programming-guide/classes-and-structs/static-constructors.md).  
  
 Nell'esempio seguente viene illustrato un costruttore di istanza:  
  
 [!code-cs[csProgGuideObjects#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_1.cs)]  
  
> [!NOTE]
>  Per maggior chiarezza, questa classe contiene campi pubblici.  L'utilizzo di campi pubblici non è consigliato nella programmazione, perché consente a qualsiasi metodo in un punto qualsiasi di un programma di accedere senza restrizioni e senza alcuna verifica ai meccanismi interni di un oggetto.  I membri dati devono in genere essere privati e devono essere accessibili solo tramite metodi e proprietà di classi.  
  
 Questo costruttore di istanza viene chiamato quando viene creato un oggetto basato sulla classe `CoOrds`.  Un costruttore come questo, che non accetta argomenti, viene definito *costruttore predefinito*.  Tuttavia, risulta spesso utile per fornire costruttori aggiuntivi.  È ad esempio possibile aggiungere alla classe `CoOrds` un costruttore che consenta di specificare i valori iniziali per i membri dati:  
  
 [!code-cs[csProgGuideObjects#76](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_2.cs)]  
  
 In questo modo sarà possibile creare oggetti `CoOrd` con valori iniziali predefiniti o specifici, come illustrato di seguito:  
  
 [!code-cs[csProgGuideObjects#77](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_3.cs)]  
  
 Se una classe non dispone di un costruttore, viene generato automaticamente un costruttore predefinito e per inizializzare i campi dell'oggetto vengono utilizzati i valori predefiniti.  Ad esempio, un [int](../../../csharp/language-reference/keywords/int.md) viene inizializzato a 0.  Per ulteriori informazioni sui valori predefiniti, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  Poiché il costruttore predefinito della classe `CoOrds` inizializza tutti i membri dati su zero, può pertanto essere rimosso completamente senza modificare il funzionamento della classe.  Per un esempio completo sull'utilizzo di più costruttori, vedere l'Esempio 1 più avanti in questo argomento. Per un esempio di costruttore generato automaticamente, vedere l'Esempio 2.  
  
 I costruttori di istanza possono inoltre essere utilizzati per chiamare i costruttori di istanza delle classi base.  Il costruttore di classi può richiamare il costruttore della classe base mediante l'inizializzatore, ad esempio:  
  
 [!code-cs[csProgGuideObjects#78](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_4.cs)]  
  
 In questo esempio la classe `Circle` passa i valori che rappresentano il raggio e l'altezza al costruttore fornito da `Shape`, da cui deriva `Circle`.  Per un esempio completo sull'utilizzo di `Shape` e `Circle`, vedere l'Esempio 3 di questo argomento.  
  
## Esempio 1  
 Nell'esempio riportato di seguito viene illustrata una classe con due costruttori di classi, uno senza argomenti e uno con due argomenti.  
  
 [!code-cs[csProgGuideObjects#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_5.cs)]  
  
## Esempio 2  
 Nell'esempio riportato di seguito la classe `Person` non ha alcun costruttore. In questo caso viene fornito automaticamente un costruttore predefinito e i campi vengono inizializzati sui valori predefiniti.  
  
 [!code-cs[csProgGuideObjects#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_6.cs)]  
  
 Si noti che il valore predefinito di `age` è `0` e il valore predefinito di `name` è `null`.  Per ulteriori informazioni sui valori predefiniti, vedere [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md).  
  
## Esempio 3  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo dell'inizializzatore della classe base.  La classe `Circle` è derivata dalla classe generale `Shape` e la classe `Cylinder` è derivata dalla classe `Circle`.  Il costruttore di ciascuna classe derivata utilizza il relativo inizializzatore della classe base.  
  
 [!code-cs[csProgGuideObjects#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/instance-constructors_7.cs)]  
  
 Per ulteriori esempi su come richiamare i costruttori della classe base, vedere [virtuale](../../../csharp/language-reference/keywords/virtual.md), [override](../../../csharp/language-reference/keywords/override.md) e [base](../../../csharp/language-reference/keywords/base.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Classi e struct](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Costruttori](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Distruttori](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [statiche](../../../csharp/language-reference/keywords/static.md)