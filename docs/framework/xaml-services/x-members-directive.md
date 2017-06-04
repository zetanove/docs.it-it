---
title: "x:Members Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 155b393d-3b49-4c5a-8c9e-b3d9893af4e4
caps.latest.revision: 5
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 5
---
# x:Members Directive
Utilizza un set di membri che sono definiti nel markup, il che vale per la x:Class dell'elemento padre.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
  
<object x:Class="className">  
  <x:Members>  
    oneOrMoreMembers  
  </x:Members  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`className`|Nome della classe di supporto della classe parziale per la produzione di XAML.  Vedere la sezione Osservazioni.|  
|`oneOrMoreMembers`|Uno o più elementi oggetto che rappresentano le definizioni di membri.  In genere si tratta di elementi oggetto `x:Property`.  Vedere la sezione Osservazioni.|  
  
## Note  
 Nell'implementazione dei servizi XAML di .NET Framework, non è disponibile una classe di supporto o l'implementazione di un membro sottostante per `x:Members`.  `x:Members` è un membro speciale XAML che può esistere come membro su qualsiasi tipo.  In un flusso del nodo XAML, `x:Members` è rappresentato come un membro denominato `Members`, dallo spazio dei nomi XAML del linguaggio XAML.  Il membro `Members` contiene un elenco generico di sola lettura degli oggetti `Member`.  Nel markup tipico i singoli membri sono specificati come elementi della proprietà `x:Property`.  `x:Property` è un tipo più preciso da utilizzare in maniera specifica per le proprietà dei tipi ed è assegnabile a `x:Member`.  Per ulteriori informazioni, vedere [x:Property Directive](../../../docs/framework/xaml-services/x-property-directive.md).  
  
 Per supportare un utilizzo pratico di `x:Members` come mezzo per specificare le definizioni di membro nel markup, i membri devono essere associati a una classe che può essere modificata.  Il modello desiderato prevede che `x:Members` esista come membro di un tipo che specifica un oggetto `x:Class`.  Tuttavia, il meccanismo per l'associazione dei tipi e dei membri o per la produzione di definizioni dei membri dinamici non è supportato dal livello dei servizi XAML di .NET Framework.  Ciò è affidata ai singoli framework che dispongono di modelli di applicazione che supportano le definizioni di membro XAML.  In genere le operazioni di compilazione di MSBUILD che compilano codice XAML tramite markup e lo integrano con code\-behind o producono assembly puri da XAML sono necessarie per supportare tale funzionalità.  
  
## x:Members per Windows Workflow Foundation  
 Per Windows Workflow Foundation, `x:Members` contiene i membri di un'attività personalizzata creata interamente in XAML o membri dinamici definiti in XAML per un ActivityDesigner con code\-behind.  È necessario anche specificare `x:Class` sull'elemento radice della produzione XAML.  Non si tratta di un requisito a livello dei servizi XAML di .NET Framework, ma diventa un requisito quando la produzione di XAML viene caricata dalle operazioni di compilazione MSBUILD che supportano le attività personalizzate e Windows Workflow Foundation XAML in generale.  `x:Members` deve essere il primo elemento figlio dell'elemento nel markup dell'elemento oggetto che dichiara la `x:Class`.