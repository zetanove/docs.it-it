---
title: "x:Class Directive | Microsoft Docs"
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
  - "x:Class"
  - "xClass"
  - "Class"
helpviewer_keywords: 
  - "Class attribute in XAML [XAML Services]"
  - "XAML [XAML Services], x:Class attribute"
  - "x:Class attribute [XAML Services]"
ms.assetid: bc4a3d8e-76e2-423e-a5d1-159a023e82ec
caps.latest.revision: 27
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 26
---
# x:Class Directive
Configura la compilazione del markup XAML per creare un join delle classi parziali tra markup e code\-behind.  La classe parziale del codice viene definita in un file di codice distinto in un linguaggio [!INCLUDE[TLA#tla_cls](../../../includes/tlasharptla-cls-md.md)], mentre la classe parziale del markup viene in genere creata dalla generazione del codice durante la compilazione XAML.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:Class="namespace.classname"...>  
  ...  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`namespace`|Parametro facoltativo.  Specifica uno spazio dei nomi [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] contenente la classe parziale identificata da `classname`.  Se l'oggetto `namespace` viene specificato, un punto \(.\) separa `namespace` e `classname`.  Vedere la sezione Osservazioni.|  
|`classname`|Obbligatorio.  Specifica il nome [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] della classe parziale che connette il codice XAML caricato e il code\-behind per tale codice XAML.|  
  
## Dipendenze  
 È possibile specificare `x:Class` solo sull'elemento radice di una produzione XAML.  `x:Class` non è valido su qualsiasi oggetto che dispone di un padre nella produzione XAML.  Per ulteriori informazioni, vedere[\[MS\-XAML\] Sezione 4.3.1.6](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
## Note  
 Il valore  `namespace` può contenere punti aggiuntivi per organizzare gli spazi dei nomi correlati in gerarchie di nomi, il che rappresenta una tecnica comune nella programmazione .NET Framework.  Solo il punto ultimo in una stringa di valori `x:Class` viene interpretato per separare `namespace` e `classname.` La classe utilizzata come `x:Class` non può essere una classe annidata.  Le classi annidate non sono consentite poiché in caso contrario la determinazione dei significati dei punti delle stringhe `x:Class` sarebbe ambigua.  
  
 Nei modelli di programmazione esistenti che utilizzano `x:Class`, `x:Class` è facoltativo in quanto la presenza di una pagina XAML senza alcun code\-behind rappresenta un comportamento del tutto valido.  Tuttavia, questa funzione interagisce con le operazioni di compilazione implementate da framework che utilizzano XAML.  La funzionalità di `x:Class` viene influenzata anche dai ruoli che le varie classificazioni di contenuto specificato da XAML hanno in un modello di applicazione e nelle azioni di compilazione corrispondenti.  Se XAML dichiara valori di attributi di gestione degli eventi o crea istanze di elementi personalizzati in cui le classi di definizione sono incluse nella classe code\-behind, è necessario fornire il riferimento della direttiva `x:Class`, o [x:Subclass](../../../docs/framework/xaml-services/x-subclass-directive.md), alla classe appropriata per il code\-behind.  
  
 Il valore della direttiva `x:Class` deve essere una stringa che specifica il nome completo di una classe, ma senza informazioni sull'assembly \(equivalente alla proprietà <xref:System.Type.FullName%2A?displayProperty=fullName>\).  Per le applicazioni semplici, è possibile omettere le informazioni sullo spazio dei nomi CLR se la struttura del code\-behind è la stessa \(la definizione del codice inizia a livello di classe\).  
  
 Il file code\-behind per la definizione di una pagina o di un'applicazione deve essere all'interno di un file di codice incluso come parte del progetto che genera un'applicazione compilata e comporta la compilazione del markup.  È necessario attenersi alle regole dei nomi per le classi CLR.  Per ulteriori informazioni, vedere [Linee guida](../../../ml/index.xml).  Per impostazione predefinita, la classe code\-behind deve essere `public`; tuttavia è possibile definirla in un livello di accesso diverso utilizzando [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md).  
  
 Questa interpretazione dell'attributo `x:Class` si applica solo a un'implementazione XAML basata su CLR, in particolare per quanto riguarda i Servizi XAML di .NET Framework.  Le altre implementazioni XAML non basate su CLR e che non utilizzano classi di servizi XAML di .NET Framework potrebbero utilizzare una formula di risoluzione diversa per la connessione al markup XAML e il supporto al codice runtime.  Per ulteriori informazioni su interpretazioni più generali di `x:Class`, vedere [\[MS\-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
 A un determinato livello di architettura, il significato di `x:Class` non è definito nei servizi XAML di .NET Framework.  Ciò è dovuto al fatto che i servizi XAML di .NET Framework non specificano il modello di programmazione complessivo mediante cui sono connessi il markup XAML e il codice di supporto.  Ulteriori utilizzi della direttiva `x:Class` potrebbero essere implementati da framework specifici che utilizzano modelli di programmazione o di applicazione per definire come connettere markup XAML e code\-behind basato su CLR.  Ciascuno di questi framework può disporre di operazioni di compilazione che abilitano alcuni comportamenti o componenti specifici da includere nell'ambiente di compilazione.  All'interno di un framework, le azioni di compilazione possono variare anche a seconda del linguaggio CLR specifico utilizzato per il code\-behind.  
  
## x:Class nel Modello di programmazione WPF  
 Nelle applicazioni WPF e nel modello applicativo WPF è possibile dichiarare `x:Class` come attributo per qualsiasi elemento che costituisce la radice di un file XAML e che viene compilato \(nei casi in cui il file XAML è incluso in un progetto di applicazione WPF con l'operazione di compilazione `Page`\) o per la radice di <xref:System.Windows.Application> nella definizione di un'applicazione WPF compilata.  La dichiarazione di `x:Class` in un elemento diverso da una radice della pagina o dell'applicazione, su un file XAMLWPF non compilato, provoca un errore in fase di compilazione nel compilatore XAML WPF [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] e [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)].  Per informazioni su altri aspetti della gestione di `x:Class` in WPF, vedere [Code\-behind e XAML in WPF](../../../ocs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md).  
  
## x:Class per Windows Workflow Foundation  
 Per Windows Workflow Foundation, `x:Class` nomina la classe di un'attività personalizzata creata interamente in XAML o nomina la classe parziale della pagina XAML per un ActivityDesigner con code\-behind.  
  
## Note sull'utilizzo di Silverlight.  
 `x:Class` per Silverlight è documentato separatamente.  Per ulteriori informazioni, vedere [Funzionalità del linguaggio dello spazio dei nomi XAML \(x:\)](http://msdn.microsoft.com/it-it/library/cc188995\(vs.95\).aspx).  
  
## Vedere anche  
 [x:Subclass Directive](../../../docs/framework/xaml-services/x-subclass-directive.md)   
 [Classi XAML e personalizzate per WPF](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [x:ClassModifier Directive](../../../docs/framework/xaml-services/x-classmodifier-directive.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)