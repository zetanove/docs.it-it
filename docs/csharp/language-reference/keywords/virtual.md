---
title: "virtual (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "virtual_CSharpKeyword"
  - "virtual"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "virtual (parola chiave) [C#]"
ms.assetid: 5da9abae-bc1e-434f-8bea-3601b8dcb3b2
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# virtual (Riferimenti per C#)
La parola chiave `virtual` viene utilizzata per modificare un metodo, una proprietà, un indicizzatore o una dichiarazione di evento e consente di sottoporli a override in una classe derivata.  Ad esempio, è possibile effettuare l'override di questo metodo tramite qualsiasi classe che lo eredita:  
  
```  
public virtual double Area()   
{  
    return x * y;  
}  
```  
  
 In una classe derivata l'implementazione di un membro virtuale può essere modificata [tramite override da un membro](../../../csharp/language-reference/keywords/override.md) di una classe derivata.  Per ulteriori informazioni sull'utilizzo della parola chiave `virtual`, vedere [Controllo delle versioni con le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md) e [Sapere quando utilizzare le parole chiave Override e New](../../../csharp/programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md).  
  
## Note  
 Quando si richiama un metodo virtuale, in fase di esecuzione viene verificata la presenza di un membro per l'esecuzione di override per il tipo dell'oggetto.  Viene chiamato il membro per l'esecuzione di override nella classe derivata di livello più basso, che potrebbe coincidere con il membro originale nel caso in cui nessuna classe derivata abbia sottoposto il membro a override.  
  
 In base all'impostazione predefinita, i metodi sono non virtuali  e non possono essere sottoposti a override.  
  
 Non è possibile utilizzare il modificatore `virtual` insieme ai modificatori `static`, `abstract, private` o `override`.  Nell'esempio seguente viene illustrata una proprietà virtuale:  
  
 [!code-cs[csrefKeywordsModifiers#26](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#26)]  
  
 Le proprietà virtuali hanno un comportamento analogo a quello dei metodi astratti, ma presentano delle differenze nella sintassi della dichiarazione e delle chiamate.  
  
-   È errato utilizzare il modificatore `virtual` per una proprietà statica.  
  
-   È possibile sottoporre a override una proprietà virtuale ereditata in una classe derivata includendo una dichiarazione di proprietà che utilizza il modificatore `override`.  
  
## Esempio  
 In questo esempio, la classe `Shape` contiene le due coordinate `x` e `y` e il metodo virtuale `Area()`.  Le diverse classi relative alle forme, come `Circle`, `Cylinder` e `Sphere`, ereditano la classe `Shape` e per ciascuna figura viene calcolata l'area della superficie.  Ogni classe derivata ha la propria implementazione di override per `Area()`.  
  
 Si noti che le classi ereditate `Circle`,  `Sphere`e  `Cylinder` tutti i costruttori di utilizzo che consentono di inizializzare la classe base, come illustrato nella seguente dichiarazione.  
  
```  
public Cylinder(double r, double h): base(r, h) {}  
```  
  
 Il seguente programma calcola e visualizza l'area appropriata per ogni figura richiamando l'implementazione appropriata di `Area()` metodo, a seconda dell'oggetto associato al metodo.  
  
 [!code-cs[csrefKeywordsModifiers#23](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefKeywordsModifiers/csrefKeywordsModifiers.cs#23)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Polimorfismo](../../../csharp/programming-guide/classes-and-structs/polymorphism.md)   
 [abstract](../../../csharp/language-reference/keywords/abstract.md)   
 [override](../../../csharp/language-reference/keywords/override.md)   
 [new](../../../csharp/language-reference/keywords/new.md)