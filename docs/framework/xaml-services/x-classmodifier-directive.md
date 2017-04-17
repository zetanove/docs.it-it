---
title: "x:ClassModifier Directive | Microsoft Docs"
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
  - "xClassModifier"
  - "x:ClassModifier"
  - "ClassModifier"
helpviewer_keywords: 
  - "XAML [XAML Services], x:ClassModifier attribute"
  - "x:ClassModifier attribute [XAML Services]"
  - "ClassModifier attribute in XAML [XAML Services]"
ms.assetid: ef30ab78-d334-4668-917d-c9f66c3b6aea
caps.latest.revision: 22
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 21
---
# x:ClassModifier Directive
Modifica il comportamento della compilazione XAML nei casi in cui viene fornito anche `x:Class`.  In particolare, anziché creare una `class` parziale con un livello di accesso `Public` \(impostazione predefinita\), l'oggetto `x:Class` fornito viene creato con un livello di accesso `NotPublic`.  Questo comportamento influisce sul livello di accesso per la classe negli assembly generati.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:Class="namespace.classname" x:ClassModifier="NotPublic">  
   ...  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|*NotPublic*|Stringa esatta da passare per specificare la differenza tra <xref:System.Reflection.TypeAttributes?displayProperty=fullName> e <xref:System.Reflection.TypeAttributes?displayProperty=fullName> in base al linguaggio di programmazione code\-behind utilizzato.  Vedere la sezione Osservazioni.|  
  
## Dipendenze  
 L'attributo [x:Class](../../../docs/framework/xaml-services/x-class-directive.md) deve inoltre essere disponibile nello stesso elemento, che deve trovarsi nell'elemento radice di una pagina.  Per ulteriori informazioni, vedere[\[MS\-XAML\] Sezione 4.3.1.8](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
## Note  
 Il valore di `x:ClassModifier` nell'utilizzo dei servizi XAML di .NET Framework varia in base al linguaggio di programmazione.  La stringa da utilizzare dipende dal modo in cui ciascun linguaggio implementa <xref:System.CodeDom.Compiler.CodeDomProvider> e dai convertitori dei tipi restituiti per definire i significati per <xref:System.Reflection.TypeAttributes?displayProperty=fullName> e <xref:System.Reflection.TypeAttributes?displayProperty=fullName>, nonché dal rilevamento della distinzione tra maiuscole e minuscole nel linguaggio specifico.  
  
-   Per [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)], la stringa da passare per definire <xref:System.Reflection.TypeAttributes?displayProperty=fullName> è `internal`.  
  
-   Per [!INCLUDE[TLA2#tla_visualbnet](../../../includes/tla2sharptla-visualbnet-md.md)], la stringa da passare per definire <xref:System.Reflection.TypeAttributes?displayProperty=fullName> è `Friend`.  
  
-   Per [!INCLUDE[TLA2#tla_cppcli](../../../includes/tla2sharptla-cppcli-md.md)], non sono disponibili destinazioni che supportano la compilazione di XAML, pertanto il valore da passare è non specificato.  
  
 È inoltre possibile specificare <xref:System.Reflection.TypeAttributes?displayProperty=fullName> \(`public` in [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)], `Public` in [!INCLUDE[TLA2#tla_visualb](../../../includes/tla2sharptla-visualb-md.md)]\); tuttavia, solitamente non si specifica <xref:System.Reflection.TypeAttributes?displayProperty=fullName> dal momento che <xref:System.Reflection.TypeAttributes?displayProperty=fullName> è già il comportamento predefinito.  
  
 Altri valori con restrizioni di accesso al codice a livello di utente equivalenti, come `private` in [!INCLUDE[TLA2#tla_cshrp](../../../includes/tla2sharptla-cshrp-md.md)], non interessano `x:ClassModifier`, in quanto i riferimenti a classi annidate non sono supportati in XAML e pertanto il modificatore <xref:System.Reflection.TypeAttributes?displayProperty=fullName> avrà lo stesso effetto.  
  
## Nota sulla sicurezza  
 Il livello di accesso dichiarato in `x:ClassModifier` è comunque soggetto a interpretazione da parte di determinati framework e delle relative funzionalità.  WPF include funzionalità per caricare e creare un'istanza di tipi dove `x:ClassModifier` è `internal`, se a tale classe si fa riferimento da una risorsa WPF tramite un riferimento URI di tipo pack.  A seguito di questo caso e possibilmente di altri casi analoghi in cui si è eseguita l'implementazione da parte di altri framework, evitare di basarsi esclusivamente su `x:ClassModifier` per bloccare tutti i possibili tentativi di creazione di istanze.  
  
## Vedere anche  
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [Code\-behind e XAML in WPF](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)   
 [x:FieldModifier Directive](../../../docs/framework/xaml-services/x-fieldmodifier-directive.md)   
 [Sicurezza \(WPF\)](../../../ocs/framework/wpf/security-wpf.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)