---
title: "x:Arguments Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "x:Arguments directive [XAML Services]"
  - "Arguments directive in XAML [XAML Services]"
  - "XAML [XAML Services], x:Arguments directive"
ms.assetid: 87cc10b0-b610-4025-b6b0-ab27ca27c92e
caps.latest.revision: 12
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# x:Arguments Directive
Crea pacchetti di argomenti di costruzione per una dichiarazione di elemento oggetto del costruttore non predefinita in XAML oppure per una dichiarazione di oggetto del metodo factory.  
  
## Utilizzo dell'elemento XAML \(costruttore non predefinito\)  
  
```  
<object ...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## Utilizzo dell'elemento XAML \(metodo factory\)  
  
```  
<object x:FactoryMethod="methodName"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`oneOrMoreObjectElements`|Una stringa o più elementi oggetto che specificano argomenti da passare al costruttore sottostante non predefinito o al metodo factory.<br /><br /> Tipicamente si utilizza il testo di inizializzazione all'interno degli elementi oggetto per specificare i valori dell'argomento effettivo.  Vedere la sezione Esempi.<br /><br /> L'ordine degli elementi è significativo.  I tipi XAML in ordine devono corrispondere ai tipi o all'ordine dei tipi del costruttore di supporto o all'overload del metodo factory.|  
|`methodName`|Il nome del metodo factory che deve elaborare tutti gli argomenti di `x:Arguments`.|  
  
## Dipendenze  
 `x:FactoryMethod` può modificare l'ambito e il comportamento dove `x:Arguments` si applica.  
  
 Se non è specificato alcun `x:FactoryMethod`, `x:Arguments` si applica a firme alternative \(non predefinito\) dei costruttori del supporto.  
  
 Se `x:FactoryMethod`, `x:Arguments` viene specificato, viene applicato a un overload del metodo denominato.  
  
## Note  
 XAML 2006 può supportare l'inizializzazione non predefinita, tramite il testo di inizializzazione.  Tuttavia, l'applicazione pratica di una tecnica di costruzione di testo di inizializzazione è limitata.  Il testo di inizializzazione viene trattato come una singola stringa di testo: di conseguenza, aggiunge solo la funzionalità per un singolo parametro di inizializzazione a meno che un convertitore di tipi sia definito per il comportamento di costruzione che può analizzare gli elementi delle informazioni personalizzate e i delimitatori personalizzati dalla stringa.  Inoltre, la stringa di testo alla logica dell'oggetto è potenzialmente il convertitore di tipi predefiniti nativo di un parser XAML fornito per le primitive diverse da una stringa true.  
  
 L'utilizzo di XAML `x:Arguments` non è l'utilizzo di un elemento proprietà in senso tradizionale, perché il markup della direttiva non fa riferimento al tipo dell'elemento oggetto che lo contiene.  È più simile alle altre direttive quale `x:Code` dove l'elemento delimita un intervallo in cui il markup deve essere interpretato come diverso dall'impostazione predefinita per i contenuti figli.  In questo caso, il tipo XAML di ogni elemento oggetto passa le informazioni sui tipi di argomento, che vengono utilizzate dai parser XAML per determinare a quale utilizzo specifico della firma del metodo factory del costruttore `x:Arguments` si stia tentando di fare riferimento.  
  
 `x:Arguments` per un elemento oggetto da costruire deve precedere qualsiasi altro elemento della proprietà, contenuto, testo interno o stringa di inizializzazione dell'elemento oggetto.  Gli elementi oggetto in `x:Arguments` possono includere attributi e stringhe di inizializzazione, come consentito dal tipo XAML e dal relativo costruttore sottostante o metodo factory.  Per l'oggetto o per gli argomenti, è possibile specificare i tipi personalizzati XAML o i tipi XAML che altrimenti risultano fuori dello spazio dei nomi XAML predefinito facendo riferimento ai mapping del prefisso stabiliti.  
  
 I processori XAML utilizzano le seguenti linee guida per determinare quali argomenti specificati in `x:Arguments` devono essere utilizzati per costruire un oggetto.  Se `x:FactoryMethod` è specificato, le informazioni vengono confrontate al `x:FactoryMethod` specificato \(si noti che il valore di `x:FactoryMethod` corrisponde al nome del metodo e il metodo denominato può disporre di overload.  Se `x:FactoryMethod` non è specificato, le informazioni vengono confrontate al set di tutti gli overload del costruttore pubblico dell'oggetto.  La logica di elaborazione XAML confronta quindi il numero di parametri e seleziona l'overload con il grado corrispondente.  Se c'è più di una corrispondenza, il processore XAML deve confrontare i tipi dei parametri basati sui tipi XAML degli elementi oggetto forniti.  Se c'è ancora più di una corrispondenza, il comportamento del processore XAML non è definito.  Se viene specificato `x:FactoryMethod` ma non è possibile risolvere il metodo, un processore XAML deve generare un'eccezione.  
  
 Utilizzo dell'attributo XAML `<x:Arguments>string</x:Arguments>` è tecnicamente possibile.  Tuttavia, questo non fornisce alcuna funzionalità oltre a ciò che può essere eseguito in caso contrario tramite il testo e i convertitori di tipi di inizializzazione e utilizzando questa sintassi non rientra negli intenti di progettazione delle funzionalità del metodo factory di XAML 2009.  
  
## Esempi  
 Nell'esempio seguente viene illustrata una firma del costruttore non predefinita, quindi l'utilizzo XAML di `x:Arguments` che accede alla firma.  
  
```csharp  
public class Food {  
    private string _name;  
    private Int32 _calories;  
    public Food(string name, Int32 calories) {  
        _name=name;  
        _calories=calories;  
    }  
}  
```  
  
```  
<my:Food>  
    <x:Arguments>  
        <x:String>Apple</x:String>  
        <x:Int32>150</x:Int32>  
    </x:Arguments>  
</my:Food>  
```  
  
 Nell'esempio seguente viene illustrata una firma del metodo factory di destinazione, quindi l'utilizzo XAML di `x:Arguments` che accede alla firma.  
  
```csharp  
public Food TryLookupFood(string name)  
{  
  switch (name) {  
    case "Apple": return new Food("Apple",150);  
    case "Chocolate": return new Food("Chocolate",200);  
    case "Cheese": return new Food("Cheese", 450);  
    default: {return new Food(name,0);  
  }  
}  
```  
  
```  
<my:Food x:FactoryMethod="TryLookupFood">  
    <x:Arguments>  
        <x:String>Apple</x:String>  
    </x:Arguments>  
</my:Food>  
```  
  
## Vedere anche  
 [Defining Custom Types for Use with .NET Framework XAML Services](../../../docs/framework/xaml-services/defining-custom-types-for-use-with-net-framework-xaml-services.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)