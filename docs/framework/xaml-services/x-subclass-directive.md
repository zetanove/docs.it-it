---
title: "x:Subclass Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Subclass"
  - "xSubclass"
  - "x:Subclass"
helpviewer_keywords: 
  - "x:Subclass attribute [XAML Services]"
  - "XAML [XAML Services], x:Subclass attribute"
  - "Subclass attribute in XAML [XAML Services]"
ms.assetid: 99f66072-8107-4362-ab99-8171dc83b469
caps.latest.revision: 20
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 20
---
# x:Subclass Directive
Modifica il comportamento della compilazione di markup XAML nei casi in cui viene fornito anche `x:Class`.  Anziché creare una classe parziale basata sulla classe `x:Class`, l'oggetto `x:Class` fornito viene creato come classe intermedia, pertanto si prevede che la classe derivata si basi sull'attributo `x:Class`.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:Class="namespace.classname" x:Subclass="subclassNamespace.subclassName">  
   ...  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`namespace`|Parametro facoltativo.  Specifica uno spazio dei nomi CLR che contiene `classname`.  Se l'oggetto `namespace` viene specificato, un punto \(.\) separa `namespace` e `classname`.|  
|`classname`|Obbligatorio.  Specifica il nome CLR della classe parziale che connette il file XAML caricato e il code\-behind per tale XAML.  Vedere la sezione Osservazioni.|  
|`subclassNamespace`|Parametro facoltativo.  Può essere diverso da `namespace` se ogni spazio dei nomi è in grado di risolvere l'altro.  Specifica uno spazio dei nomi CLR che contiene `subclassName`.  Se l'oggetto `subclassName` viene specificato, un punto \(.\) separa `subclassNamespace` e `subclassName`.|  
|`subclassName`|Obbligatorio.  Specifica il nome CLR della sottoclasse.|  
  
## Dipendenze  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md) deve inoltre essere disponibile sullo stesso oggetto, che deve essere l'elemento radice della produzione XAML.  
  
## Note  
 L'utilizzo dell'attributo `x:Subclass` è destinato principalmente ai linguaggi che non supportano dichiarazioni di classe parziali.  
  
 La classe utilizzata come `x:Subclass` non può essere una classe annidata, e `x:Subclass` deve far riferimento all'oggetto radice come spiegato nella sezione "Dipendenze".  
  
 In caso contrario, il significato concettuale di `x:Subclass` non è definito da un'implementazione dei servizi XAML di .NET Framework.  Ciò è dovuto al fatto che il comportamento dei servizi XAML di .NET Framework non specifica il modello di programmazione complessivo tramite cui sono connessi il markup XAML e il codice di supporto.  Le implementazioni di ulteriori concetti correlati a `x:Class` e `x:Subclass` vengono eseguite da framework specifici che utilizzano modelli di programmazione o di applicazione per definire come connettere markup XAML, markup compilato e code\-behind basato su CLR.  Ciascun framework potrebbe disporre di operazioni di compilazione che abilitano alcuni comportamenti o componenti specifici da includere nell'ambiente di compilazione.  All'interno di un framework, le azioni di compilazione possono variare anche in base al linguaggio CLR specifico utilizzato per il code\-behind.  
  
## Note sull'utilizzo di WPF  
 `x:Subclass` può essere in una radice della pagina o nella radice <xref:System.Windows.Application> nella definizione di applicazione, che dispone già di `x:Class`.  La dichiarazione dell'attributo `x:Subclass`  in un elemento diverso dalla radice di una pagina o di un'applicazione oppure la specifica di questo attributo in assenza di un attributo `x:Class` causerà un errore in fase di compilazione.  
  
 La creazione di classi derivate che funzionano correttamente per lo scenario `x:Subclass` è abbastanza complessa.  Potrebbe essere necessario esaminare i file intermedi \(vale a dire i file g prodotti nella cartella obj del progetto tramite compilazione del markup, con nomi che incorporano i nomi file xaml\).  Questi file intermedi possono consentire di determinare l'origine di specifici costrutti di programmazione nelle classi parziali associate nell'applicazione compilata.  
  
 I gestori eventi nella classe derivata devono essere `internal override` \(`Friend Overrides` in [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)]\) per eseguire l'override degli stub per i gestori creati nella classe intermedia durante la compilazione.  In caso contrario, le implementazioni della classe derivata nascondono l'implementazione della classe intermedia e i gestori della classe intermedia non vengono richiamati.  
  
 Quando si definiscono gli oggetti `x:Class` e `x:Subclass`, non è necessario fornire alcuna implementazione per la classe a cui fa riferimento l'oggetto `x:Class`.  È sufficiente denominare la classe mediante l'attributo `x:Class`, in modo che il compilatore disponga di istruzioni per la classe che crea nei file intermedi \(il compilatore non seleziona un nome predefinito in questo caso\).  È possibile fornire un'implementazione alla classe `x:Class`; tuttavia questa operazione non fa parte dello scenario tipico dell'utilizzo combinato di `x:Class` e `x:Subclass`.  
  
## Vedere anche  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [Classi XAML e personalizzate per WPF](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)