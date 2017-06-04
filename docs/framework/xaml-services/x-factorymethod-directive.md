---
title: "x:FactoryMethod Directive | Microsoft Docs"
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
  - "XAML. x:FactoryMethod directive [XAML Services]"
  - "FactoryMethod directive in XAML [XAML Services]"
  - "x:FactoryMethod directive [XAML Services]"
ms.assetid: 829bcbdf-5318-4afb-9a03-c310e0d2f23d
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# x:FactoryMethod Directive
Specifica un metodo diverso da un costruttore che un processore XAML deve utilizzare per inizializzare un oggetto dopo avere risolto il tipo di supporto.  
  
## Utilizzo dell'attributo XAML, nessun x:Arguments  
  
```  
<object x:FactoryMethod="methodname"...>  
  ...  
</object>  
```  
  
## Utilizzo dell'attributo XAML, x:Arguments come elemento\(i\)  
  
```  
<object x:FactoryMethod="methodname"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`methodname`|Il nome del metodo della stringa di un metodo che i processori XAML chiamano per inizializzare l'istanza specificato come `object`.  Vedere la sezione Osservazioni.|  
|`oneOrMoreObjectElements`|Uno o più elementi oggetto per gli oggetti che specificano parametri del metodo di factory.  L'ordine è significativo, significa che l'ordine che argomenta deve essere passato al metodo factory.|  
  
## Note  
 Se `methodname` è un metodo di istanza, non può essere qualificato.  
  
 I metodi statici sono supportati come i metodi factory.  Se `methodname` è un metodo statico, `methodname` viene fornito come una combinazione di *typeName*.*methodName*, dove *typeName* assegna un nome alla classe che definisce il metodo factory statico.  *typeName* possono essere qualificati dal prefisso se riferendosi a un tipo in un xmlns mappato.  *typeName* può essere un tipo diverso che `typeof(``object``)`.  
  
 Il metodo factory deve essere un metodo pubblico dichiarato del tipo che supporta l'elemento oggetto pertinente.  
  
 Il metodo factory deve restituire un'istanza che è assegnabile all'oggetto pertinente.  I metodi factory non devono mai restituire null.  
  
 `x:Arguments` funziona su un principio di migliore corrispondenza per le firme di metodi factory.  La corrispondenza prima valuta il conteggio del parametro.  Se c'è più di una possibile corrispondenza per un conteggio del parametro, il tipo di parametro viene valutato e la migliore corrispondenza viene determinata.  Se c'è ancora ambiguità dopo questa fase di valutazione, il comportamento di processore di XAML non è definito.  
  
 L'utilizzo di un elemento `x:FactoryMethod` non è l'utilizzo di un elemento proprietà in senso tradizionale, perché il markup della direttiva non fa riferimento al tipo dell'elemento oggetto contenitore.  È previsto che l'utilizzo dell'elemento sia meno comune dell'utilizzo dell'attributo.  `x:Arguments` \(utilizzo dell'attributo o dell'elemento\) possono essere utilizzati insieme all'utilizzo dell'elemento `x:FactoryMethod`, ma questo non viene visualizzato in maniera specifica nelle sezioni relative agli utilizzi.  
  
 `x:FactoryMethod` come un elemento deve precedere qualsiasi altro elemento della proprietà e deve precedere qualsiasi `x:Arguments` fornito anche come elemento e deve precedere qualsiasi contenuto, testo interno o testo di inizializzazione.  
  
## Vedere anche  
 [x:Arguments Directive](../../../docs/framework/xaml-services/x-arguments-directive.md)