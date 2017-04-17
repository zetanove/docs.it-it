---
title: "x:Uid Directive | Microsoft Docs"
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
  - "XAML [XAML Services], localizable content attribute"
  - "XAML [XAML Services], x:Uid attribute"
  - "x:Uid attribute [XAML Services]"
  - "Uid attribute [XAML Services]"
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
caps.latest.revision: 12
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# x:Uid Directive
Fornisce un identificatore univoco per gli elementi di markup  In molti scenari, questo identificatore univoco viene utilizzato da strumenti e processi della localizzazione di XAML.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:Uid="identifier"... />  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`identifier`|Stringa creata manualmente o generata automaticamente che dovrebbe essere univoca all'interno di un file quando viene interpretata da un consumer `x:Uid`.|  
  
## Note  
 In \[MS\-XAML\], `x:Uid` viene definito come direttiva.  Per ulteriori informazioni, vedere[\[MS\-XAML\] Sezione 5.3.6](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
 `x:Uid` è separato da `x:Name` a causa dello scenario di localizzazione di XAML dichiarato e in modo che gli identificatori utilizzati per la localizzazione non dipendano dalle implicazioni del modello di programmazione di `x:Name`.  Inoltre, `x:Name` viene governato dal concetto di un NameScope XAML; tuttavia, `x:Uid` non viene governato da nessun linguaggio XAML definito concetto di imposizione di unicità.  I processori XAML in senso generico \(vale a dire i processori che non fanno necessariamente parte del processo di localizzazione\) non devono, normalmente, applicare l'unicità dei valori `x:Uid`.  Questa responsabilità riguarda concettualmente il generatore dei valori.  La prospettiva di univocità dei valori `x:Uid` con una singola origine XAML, ad esempio, è ragionevole per consumer dei valori, come ad esempio strumenti o processi di globalizzazione dedicati.  Il modello di univocità tipico è quello in cui i valori `x:Uid` sono univoci all'interno di un file con codifica XML che rappresenta XAML.  
  
 Strumenti che dispongono di conoscenza significativa di un particolare schema XAML possono scegliere di applicare `x:Uid` solo per le vere stringhe localizzabili, invece che per tutti i casi dove un valore della stringa di testo viene incontrato in markup.  
  
 I framework possono specificare una particolare proprietà nel modello a oggetti per essere un alias per `x:Uid`, applicando l'attributo <xref:System.Windows.Markup.UidPropertyAttribute> al tipo di definizione.  Se un framework specifica una proprietà particolare, non è consentito specificare né `x:Uid` né il membro con alias sullo stesso oggetto.  Se sono specificati sia `x:Uid` che il membro con alias, l'API dei servizi XAML di .NET Framework API genera di solito <xref:System.Xaml.XamlDuplicateMemberException> per questo evento.  
  
## Note sull'utilizzo di WPF  
 Per ulteriori informazioni sul ruolo di `x:Uid` nel processo di localizzazione WPF e nel form BAML di XAML, vedere [Globalizzazione per WPF](../../../ocs/framework/wpf/advanced/globalization-for-wpf.md) o <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>  
  
## Vedere anche  
 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>   
 <xref:Microsoft.Build.Tasks.Windows.UidManager>   
 [Globalizzazione per WPF](../../../ocs/framework/wpf/advanced/globalization-for-wpf.md)