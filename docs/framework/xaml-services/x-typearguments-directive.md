---
title: "x:TypeArguments Directive | Microsoft Docs"
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
  - "x:TypeArguments"
  - "xTypeArguments"
  - "TypeArguments"
helpviewer_keywords: 
  - "x:TypeArguments attribute [XAML Services]"
  - "TypeArguments attribute in XAML [XAML Services]"
  - "XAML [XAML Services], x:TypeArguments attribute"
ms.assetid: 86561058-d393-4a44-b5c3-993a4513ea74
caps.latest.revision: 18
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 18
---
# x:TypeArguments Directive
Passa vincoli di tipo generico al costruttore di tipo generico.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:TypeArguments="typeString" .../>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`object`|Una dichiarazione dell'elemento oggetto di un tipo XAML, appoggiata da un tipo generico CLR.  Se `object` fa riferimento al tipo XAML non proveniente dallo spazio dei nomi XAML predefinito, `object` richiede un prefisso per indicare lo spazio dei nomi XAML dove `object` è presente.|  
|`typeString`|Stringa che dichiara uno o più nomi del tipo XAML come stringhe che forniscono gli argomenti di tipo per il tipo generico CLR.  Vedere Commenti per le ulteriori note della sintassi.|  
  
## Note  
 Nella maggior parte dei casi, i tipi XAML utilizzati come un elemento di informazione in una stringa `typeString` sono premessi.  Tipi comuni di vincoli CLR generici, ad esempio <xref:System.Int32> e <xref:System.String>, provengono dalle librerie di classe di base di CLR.  Queste librerie non vengono mappate agli spazi dei nomi XAML predefiniti specifici del framework tipici e pertanto richiedono un mapping del prefisso per l'utilizzo di XAML.  
  
 È possibile specificare più di un nome del tipo XAML utilizzando una virgola di delimitazione.  
  
 Se i vincoli generici utilizzano tipi generici, gli argomenti dei tipi dei vincoli annidati possono essere contenuti tra parentesi \(\):  
  
 Notare che questa definizione di `x:TypeArguments` è specifica dei Servizi XAML di .NET Framework, utilizzando il supporto CLR.  Una definizione del livello del linguaggio XAML può essere trovata in [\[MS\-XAML\] Sezione 5.3.11](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
## Esempi di utilizzo  
 Per questi esempi, presupporre che le seguenti definizioni dello spazio dei nomi XAML vengano dichiarate:  
  
```  
xmlns:sys="clr-namespace:System;assembly=mscorlib"  
xmlns:scg="clr-namespace:System.Collections.Generic;assembly=mscorlib"  
```  
  
### List\<String\>  
 `<scg:List x:TypeArguments="sys:String" ...>` crea un'istanza di un nuovo <xref:System.Collections.Generic.List%601> con un argomento di tipo <xref:System.String>.  
  
### Dictionary\<String,String\>  
 `<scg:Dictionary x:TypeArguments="sys:String,sys:String" ...>` crea un'istanza di un nuovo <xref:System.Collections.Generic.Dictionary%602> con due argomenti di tipo <xref:System.String>.  
  
### Queue\<KeyValuePair\<String,String\>\>  
 `<scg:Queue x:TypeArguments="scg:KeyValuePair(sys:String,sys:String)" ...>` crea un'istanza di un nuovo <xref:System.Collections.Generic.Queue%601> che dispone di un vincolo di <xref:System.Collections.Generic.KeyValuePair%602> con gli argomenti del tipo di vincolo interni <xref:System.String> e <xref:System.String>.  
  
## XAML 2006 e utilizzi di XAML generici WPF  
 Per l'utilizzo di XAML 2006 e XAML utilizzato per le applicazioni WPF, le restrizioni seguenti sono generalmente disponibili per utilizzi di `x:TypeArguments` e del tipo generico da XAML:  
  
-   Solo l'elemento radice di un file XAML può supportare un utilizzo di XAML generico che fa riferimento a un tipo generico.  
  
-   L'elemento radice deve eseguire il mapping a un tipo generico con almeno un argomento di tipo.  <xref:System.Windows.Navigation.PageFunction%601> è un esempio.  Le funzioni della pagina sono lo scenario primario per il supporto dell'utilizzo generico di XAML in WPF.  
  
-   L'elemento oggetto XAML dell'elemento radice deve dichiarare anche una classe parziale utilizzando `x:Class`.  Questo è vero anche se si definisce un'azione di compilazione WPF.  
  
-   `x:TypeArguments` non può fare riferimento a vincoli generici annidati.  
  
## XAML 2009 o XAML 2006 senza dipendenza WPF 3.0 o WPF 3.5  
 In Servizi .NET Framework XAML per XAML 2006 o XAML 2009, le restrizioni relative al WPF sull'utilizzo generico di XAML sono meno rigide.  È possibile creare un'istanza di un elemento oggetto generico in qualsiasi posizione in markup XAML che il sistema del tipo di supporto e il modello a oggetti possono supportare.  
  
 Se si utilizza XAML 2009, anziché eseguire il mapping dei tipi di base CLR per ottenere tipi XAML per le primitive di linguaggio comuni, è possibile utilizzare [Tipi incorporati per primitive del linguaggio XAML comuni](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md) come elementi di informazione in `typeString`.  Ad esempio, è possibile dichiarare quanto segue \(mapping dei prefissi non indicati, ma x è lo spazio dei nomi XAML del linguaggio XAML per XAML 2009\):  
  
```  
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>  
```  
  
 In WPF e con [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], è possibile utilizzare le funzionalità di XAML 2009 insieme a `x:TypeArguments` soltanto però per codice XAML separato \(e non per codice XAML compilato dal markup\).  Il codice XAML compilato dal markup per WPF e il modulo BAML di XAML non supportano attualmente le parole chiave e le funzionalità di XAML 2009.  Se si ha bisogno di una compilazione di markup di XAML, è necessario operare sotto le restrizioni annotate nella sezione "Utilizzi di XAML 2006 e XAML Generici".  
  
## Vedere anche  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [x:Type Markup Extension](../../../docs/framework/xaml-services/x-type-markup-extension.md)   
 [Tipi incorporati per primitive del linguaggio XAML comuni](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md)   
 [Generics in XAML](../../../docs/framework/xaml-services/generics-in-xaml.md)