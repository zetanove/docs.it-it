---
title: "Estensione del markup ComponentResourceKey | Microsoft Docs"
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
  - "ComponentResourceKey"
  - "ComponentResourceKeyExtension"
helpviewer_keywords: 
  - "ComponentResourceKey (estensione di markup)"
  - "XAML, ComponentResourceKey (estensione di markup)"
ms.assetid: d6bcdbe6-61b3-40a7-b381-4e02185b5a85
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Estensione del markup ComponentResourceKey
Definisce le chiavi per le risorse caricate da assembly esterni e ne creato un riferimento.  In questo modo viene abilitata una ricerca di risorse per specificare un tipo di destinazione in un assembly, piuttosto che un dizionario di risorse esplicito in un assembly o in una classe.  
  
## Utilizzo della sintassi XAML per gli attributi \(impostazione chiave, abbreviata\)  
  
```  
<object x:Key="{ComponentResourceKey {x:Type targetTypeName}, targetID}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli attributi \(impostazione chiave, dettagliata\)  
  
```  
<object x:Key="{ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli attributi \(richiesta risorsa, abbreviata\)  
  
```  
<object property="{DynamicResource {ComponentResourceKey {x:Type targetTypeName}, targetID}}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli attributi \(richiesta risorsa, dettagliata\)  
  
```  
<object property="{DynamicResource {ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}}" .../>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`targetTypeName`|Nome del tipo [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] pubblico definito nell'assembly di risorse.|  
|`targetID`|Chiave della risorsa.  Durante la ricerca delle risorse, `targetID` sarà analogo all'attributo [Direttiva x:Key](../../../../docs/framework/xaml-services/x-key-directive.md) della risorsa.|  
  
## Note  
 Come visto negli utilizzi sopra, un utilizzo dell'estensione di markup {`ComponentResourceKey` } viene trovato in due posti:  
  
-   Definizione di una chiave all'interno di un dizionario di risorse del tema, come fornita da un autore dei controlli.  
  
-   Accedere a una risorsa del tema dall'assembly, quando si sono applicati nuovamente i modelli il controllo ma si desidera utilizzare valori della proprietà che vengono da risorse fornite dai temi del controllo.  
  
 Per fare riferimento a risorse del componente che vengono dai temi, generalmente si consiglia di utilizzare `{DynamicResource}` piuttosto che `{StaticResource}`.  Viene mostrato negli utilizzi.  `{DynamicResource}` è raccomandata, perché il tema stesso può essere modificato dall'utente.  Se si desidera la risorsa del componente che più da vicino corrisponde all'intenzione dell'autore dei controlli per supportare un tema, è necessario consentire al riferimento alla risorsa del componente di essere anche dinamico.  
  
 L'oggetto <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> identifica un tipo esistente nell'assembly di destinazione in cui la risorsa è effettivamente definita.  È possibile definire e utilizzare `ComponentResourceKey` indipendentemente dalla conoscenza della posizione esatta in cui l'oggetto <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> è definito, ma il tipo deve essere risolto tramite gli assembly a cui si fa riferimento.  
  
 L'oggetto <xref:System.Windows.ComponentResourceKey> viene comunemente utilizzato per definire le chiavi che vengono quindi esposte come membri di una classe.  A tal fine, si utilizza il costruttore della classe <xref:System.Windows.ComponentResourceKey>, non l'estensione del markup.  Per ulteriori informazioni, vedere <xref:System.Windows.ComponentResourceKey> o la sezione "Chiavi di definizione e riferimento per Risorse dei temi " dell'argomento [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
 Per le chiavi di definizione e le risorse con chiave di riferimento, la sintassi degli attributi è di uso comune per l'estensione di markup `ComponentResourceKey`.  
  
 La sintassi abbreviata mostrata si basa sulla firma del costruttore <xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=fullName> e sull'utilizzo di parametri posizionali nell'estensione di markup.  L'ordine in cui sono elencati `targetTypeName` e `targetID` è fondamentale.  La sintassi dettagliata si basa sul costruttore predefinito <xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=fullName> e imposta quindi le proprietà <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> e <xref:System.Windows.ComponentResourceKey.ResourceId%2A> in modo analogo alla sintassi vera e propria dell'attributo su un elemento oggetto.  Nella sintassi dettagliata, l'ordine in cui sono impostate le proprietà non è importante.  La relazione e i meccanismi di queste due alternative \(abbreviata e dettagliata\) sono descritti più approfonditamente nell'argomento [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
 Tecnicamente, il valore per `targetID` può essere qualsiasi oggetto, non deve essere una stringa.  Tuttavia, l'utilizzo più comune in WPF consiste nell'allineare il valore `targetID` con form che sono stringhe, e dove tali stringhe sono valide nel [Grammatica XamlName](../../../../docs/framework/xaml-services/xamlname-grammar.md).  
  
 L'oggetto `ComponentResourceKey` può essere utilizzato nella sintassi per gli elementi oggetto.  In questo caso, è richiesta la specifica del valore di entrambe le proprietà <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> e <xref:System.Windows.ComponentResourceKey.ResourceId%2A> per inizializzare correttamente l'estensione.  
  
 Nell'implementazione del lettore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.ComponentResourceKey>.  
  
 `ComponentResourceKey` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  Tutte le estensioni di markup di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzano i caratteri { e } nella relativa sintassi degli attributi. Grazie a questa convenzione il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è in grado di rilevare la necessità che l'attributo venga elaborato da un'estensione di markup.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## Vedere anche  
 <xref:System.Windows.ComponentResourceKey>   
 <xref:System.Windows.Controls.ControlTemplate>   
 [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)