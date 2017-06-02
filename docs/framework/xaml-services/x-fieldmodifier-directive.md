---
title: "x:FieldModifier Directive | Microsoft Docs"
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
  - "FieldModifier attribute in XAML [XAML Services]"
  - "x:FieldModifier attribute [XAML Services]"
  - "XAML [XAML Services], x:FieldModifier attribute"
ms.assetid: ed427cd4-2f35-4d24-bd2f-0fa7b71ec248
caps.latest.revision: 15
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 14
---
# x:FieldModifier Directive
Modifica il comportamento di compilazione XAML in modo che i campi per riferimenti a oggetti denominati vengano impostati con accesso <xref:System.Reflection.TypeAttributes?displayProperty=fullName> anziché <xref:System.Reflection.TypeAttributes?displayProperty=fullName>, che rappresenta il comportamento predefinito.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:FieldModifier="Public".../>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|*Public*|Stringa esatta da passare per specificare la differenza tra <xref:System.Reflection.TypeAttributes?displayProperty=fullName> e <xref:System.Reflection.TypeAttributes?displayProperty=fullName> in base al linguaggio di programmazione code\-behind utilizzato.  Vedere la sezione Osservazioni.|  
  
## Dipendenze  
 Se una produzione XAML utilizza `x:FieldModifier` dovunque, l'elemento radice di quella produzione XAML deve dichiarare un [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md).  
  
## Note  
 `x:FieldModifier` non è pertinente per la dichiarazione del livello di accesso generale di una classe o dei relativi membri.  È invece pertinente solo per il comportamento di elaborazione XAML quando viene elaborato un determinato oggetto XAML che fa parte di una produzione XAML e diventa un oggetto potenzialmente accessibile nell'oggetto grafico di un'applicazione.  Per impostazione predefinita, il riferimento al campo per un oggetto di questo tipo viene mantenuto privato, impedendo ai consumer dei controlli di modificare direttamente la struttura ad albero di oggetti grafici.  I consumer dei controlli potranno invece modificare oggetti grafici utilizzando modelli standard abilitati da modelli di programmazione, ad esempio ottenendo la radice di layout, le raccolte di elementi figlio, le proprietà pubbliche dedicate e così via.  
  
 Il valore per l'attributo `x:FieldModifier` varia in base al linguaggio di programmazione e il relativo scopo potrà variare in framework specifici.  La stringa da utilizzare dipende dal modo in cui ciascun linguaggio implementa <xref:System.CodeDom.Compiler.CodeDomProvider> e dai convertitori dei tipi restituiti per definire i significati per <xref:System.Reflection.TypeAttributes?displayProperty=fullName> e <xref:System.Reflection.TypeAttributes?displayProperty=fullName>, nonché dal rilevamento della distinzione tra maiuscole e minuscole nel linguaggio specifico.  
  
-   Per [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)], la stringa da passare per definire <xref:System.Reflection.TypeAttributes?displayProperty=fullName> è `public`.  
  
-   Per [!INCLUDE[TLA2#tla_visualbnet](../../../includes/tla2sharptla-visualbnet-md.md)], la stringa da passare per definire <xref:System.Reflection.TypeAttributes?displayProperty=fullName> è `Public`.  
  
-   Per [!INCLUDE[TLA2#tla_cppcli](../../../includes/tla2sharptla-cppcli-md.md)], non sono disponibili attualmente destinazioni per XAML, pertanto la stringa da passare non è definita.  
  
 È inoltre possibile specificare <xref:System.Reflection.TypeAttributes?displayProperty=fullName> \(`internal` in [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)] e `Friend` in [!INCLUDE[TLA2#tla_visualb](../../../includes/tla2sharptla-visualb-md.md)]\), ma la specifica di <xref:System.Reflection.TypeAttributes?displayProperty=fullName> è una scelta insolita, in quanto il comportamento di `NotPublic` è già quello predefinito.  
  
 <xref:System.Reflection.TypeAttributes?displayProperty=fullName> è l'impostazione predefinita in quanto è insolito che il codice esterno all'assembly che ha compilato il XAML debba accedere a un elemento creato in XAML.  Grazie all'architettura di sicurezza WPF e al comportamento di compilazione XAML, i campi in cui vengono archiviate istanze dell'elemento non vengono dichiarati come pubblici, a meno che non si imposti in modo specifico l'attributo `x:FieldModifier` per consentire l'accesso pubblico.  
  
 L'attributo `x:FieldModifier` è rilevante solo per gli elementi con un attributo [x:Name Directive](../../../docs/framework/xaml-services/x-name-directive.md), poiché tale nome viene utilizzato per fare riferimento al campo dopo che è pubblico.  
  
 Per impostazione predefinita, la classe parziale per l'elemento radice è pubblica, per impostazione predefinita tuttavia è possibile renderla non pubblica utilizzando [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md).  [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md) influisce anche sul livello di accesso dell'istanza della classe di elementi radice.  È possibile inserire `x:Name` e `x:FieldModifier` nell'elemento radice, tuttavia questa operazione consente solo di creare una copia del campo pubblico dell'elemento radice, mentre il livello di accesso della classe del vero elemento radice è ancora controllato da [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md).  
  
## Vedere anche  
 [Classi XAML e personalizzate per WPF](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [Code\-behind e XAML in WPF](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)   
 [x:Name Directive](../../../docs/framework/xaml-services/x-name-directive.md)   
 [Compilazione di un'applicazione WPF \(WPF\)](../../../ocs/framework/wpf/app-development/building-a-wpf-application-wpf.md)   
 [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)