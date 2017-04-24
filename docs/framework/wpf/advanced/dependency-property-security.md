---
title: "Sicurezza della propriet&#224; di dipendenza | Microsoft Docs"
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
  - "proprietà di dipendenza, access"
  - "proprietà di dipendenza, sicurezza"
  - "sicurezza, proprietà di dipendenza"
  - "sicurezza, wrapper"
  - "convalida, proprietà di dipendenza"
  - "wrapper, access"
  - "wrapper, sicurezza"
ms.assetid: d10150ec-90c5-4571-8d35-84bafa2429a4
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Sicurezza della propriet&#224; di dipendenza
Le proprietà di dipendenza in genere devono essere considerate come proprietà pubbliche.  A causa della natura stessa del sistema di proprietà di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], è impossibile avere delle garanzie di sicurezza sul valore di una proprietà di dipendenza.  
  
   
  
<a name="AccessSecurity"></a>   
## Accesso e sicurezza delle proprietà wrapper e di dipendenza  
 In genere, le proprietà di dipendenza vengono implementate insieme alle proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] "wrapper" che consentono di ottenere o impostare la proprietà da un'istanza in modo più semplice.  Ma i wrapper in realtà sono solo dei metodi di convenienza per l'implementazione delle chiamate statiche <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A> sottostanti utilizzate nelle interazioni con le proprietà di dipendenza.  Considerando la situazione da un altro punto di vista, le proprietà sono esposte come proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] che risultano supportate da una proprietà di dipendenza piuttosto che da un campo privato.  I meccanismi di sicurezza applicati ai wrapper non sono paralleli al comportamento del sistema di proprietà e all'accesso della proprietà di dipendenza sottostante.  La specifica di una richiesta di sicurezza sul wrapper eviterà solo l'utilizzo del metodo di convenienza, ma non impedirà le chiamate a <xref:System.Windows.DependencyObject.GetValue%2A> oppure a <xref:System.Windows.DependencyObject.SetValue%2A>.  Analogamente, inserendo un livello di accesso protetto o privato sui wrapper non viene garantita alcuna sicurezza effettiva.  
  
 Quando si scrivono proprietà di dipendenza personalizzate, è necessario dichiarare i wrapper e il campo dell'identificatore <xref:System.Windows.DependencyProperty> come membri pubblici, in modo che i chiamanti non ottengano informazioni fuorvianti sul reale livello di accesso di quella proprietà, dal momento che l'archivio è stato implementato come proprietà di dipendenza.  
  
 Per quanto riguarda le proprietà di dipendenza personalizzate, è possibile registrarle come proprietà di dipendenza di sola lettura, impedendo così in maniera efficace che una proprietà venga impostata da qualsiasi utente che non dispone di un riferimento a <xref:System.Windows.DependencyPropertyKey> per quella proprietà.  Per ulteriori informazioni, vedere [Proprietà di dipendenza di sola lettura](../../../../docs/framework/wpf/advanced/read-only-dependency-properties.md).  
  
> [!NOTE]
>  È consentito dichiarare un campo dell'identificatore <xref:System.Windows.DependencyProperty> privato, che sarà utilizzato presumibilmente per ridurre lo spazio dei nomi esposto immediatamente di una classe personalizzata; tuttavia, tale proprietà non deve essere considerata "privata" nello stesso senso specificato dalle definizioni del linguaggio [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] per il livello di accesso, per i motivi illustrati nella prossima sezione.  
  
<a name="PropertySystemExposure"></a>   
## Esposizione di proprietà di dipendenza del sistema di proprietà  
 Dichiarare un oggetto <xref:System.Windows.DependencyProperty> come livello di accesso diverso da Public in genere non è utile ed è potenzialmente fuorviante.  L'impostazione di tale livello di accesso impedisce solo che qualcuno possa ottenere un riferimento all'istanza dalla classe dichiarante.  Tuttavia, esistono diversi aspetti del sistema di proprietà che restituiscono un oggetto <xref:System.Windows.DependencyProperty> come mezzo di identificazione di una particolare proprietà esistente in un'istanza di una classe o in un'istanza della classe derivata e questo identificatore potrà essere utilizzato in una chiamata <xref:System.Windows.DependencyObject.SetValue%2A> anche se l'identificatore statico originale è stato dichiarato come NonPublic.  Inoltre, i metodi virtuali <xref:System.Windows.DependencyObject.OnPropertyChanged%2A> ricevono le informazioni di qualsiasi proprietà di dipendenza esistente di cui venga modificato il valore.  Il metodo <xref:System.Windows.DependencyObject.GetLocalValueEnumerator%2A> restituisce gli identificatori per qualsiasi proprietà nelle istanze con valore impostato localmente.  
  
### Convalida e sicurezza  
 L'applicazione di una richiesta a un oggetto <xref:System.Windows.DependencyProperty.ValidateValueCallback%2A>, nella previsione che l'impostazione di una proprietà venga impedita tramite l'errore di convalida provocato da un esito negativo della richiesta, non costituisce un meccanismo di sicurezza adeguato.  L'annullamento della convalida del valore impostato applicato tramite <xref:System.Windows.DependencyProperty.ValidateValueCallback%2A> potrebbe essere evitato dai chiamanti non autorizzati, se questi operano all'interno del dominio dell'applicazione.  
  
## Vedere anche  
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)