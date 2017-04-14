---
title: "Attributo mc:Ignorable | Microsoft Docs"
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
  - "mc (prefisso dello spazio dei nomi XML)"
  - "mc:Ignorable (attributo)"
  - "mc:ProcessContents (attributo)"
  - "XAML, mc:Ignorable (attributo)"
  - "XAML, mc:ProcessContents (attributo)"
  - "XML, mc (prefisso dello spazio dei nomi)"
ms.assetid: acd9a6ef-b7ca-4146-abb6-60f3b366e9ec
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Attributo mc:Ignorable
Specifica quali prefissi dello spazio dei nomi [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] rilevati in un file di markup possono essere ignorati da un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  L'attributo `mc:Ignorable` supporta la compatibilità dei markup sia per il mapping dello spazio dei nomi personalizzato, sia per il controllo della versione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
## Utilizzo della sintassi XAML per gli attributi \(prefisso singolo\)  
  
```  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## Utilizzo della sintassi XAML per gli attributi \(due prefissi\)  
  
```  
<object  
  xmlns:ignorablePrefix1="ignorableUri"  
  xmlns:ignorablePrefix2="ignorableUri2"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix1 ignorablePrefix2"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|*ignorablePrefix, ignorablePrefix1 ecc.*|Qualsiasi stringa di prefisso valida, per la specifica XML 1.0.|  
|*ignorableUri*|Qualsiasi URI valido per la definizione di un spazio dei nomi, per la specifica XML 1.0.|  
|*ThisElementCanBeIgnored*|Elemento che può essere ignorato dalle implementazioni del processore [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], se il tipo sottostante non può essere risolto.|  
  
## Note  
 Il prefisso dello spazio dei nomi `mc` [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] è la convenzione dei prefissi consigliata da utilizzare quando si esegue il mapping dello spazio dei nomi per la compatibilità [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA#tla_mcxmlnsv1](../../../../includes/tlasharptla-mcxmlnsv1-md.md)].  
  
 Gli elementi o gli attributi in cui la parte del prefisso del nome dell'elemento viene identificata come `mc:Ignorable` non generano errori quando vengono elaborati da un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Se quell'attributo non può essere risolto in un tipo o costrutto di programmazione sottostante, quell'elemento viene ignorato.  Notare, tuttavia, che gli elementi ignorati potrebbero ancora generare ulteriori errori di analisi relativi ad altri requisiti dell'elemento che vengono considerati effetti collaterali della mancata elaborazione dell'elemento.  Ad esempio, un modello di contenuto particolare dell'elemento potrebbe richiedere un elemento figlio, tuttavia se l'elemento figlio specificato si trovava in un prefisso `mc:Ignorable` e non è stato possibile risolverlo in un tipo, il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] potrebbe generare un errore.  
  
 `mc:Ignorable` si applica solo ai mapping dello spazio dei nomi alle stringhe dell'identificatore.  `mc:Ignorable` non si applica ai mapping dello spazio dei nomi agli assembly che specificano uno spazio dei nomi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] e un assembly \(oppure utilizzano come assembly il file eseguibile corrente, per impostazione predefinita\).  
  
 Se si implementa un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], tale operazione non deve generare errori di analisi o di elaborazione durante la risoluzione del tipo per qualsiasi elemento o attributo qualificato da un prefisso identificato come `mc:Ignorable`.  Tuttavia, l'implementazione del processore può ancora generare eccezioni che rappresentano un risultato secondario della mancata l'elaborazione o del caricamento non riuscito di un elemento, quale l'esempio dell'elemento che dispone di un solo elemento figlio, fornito in precedenza.  
  
 Per impostazione predefinita, un processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ignorerà il contenuto di un elemento ignorato.  Tuttavia, è possibile specificare un attributo aggiuntivo, [Attributo mc:ProcessContent](../../../../docs/framework/wpf/advanced/mc-processcontent-attribute.md) al fine di richiedere che il successivo elemento padre disponibile continui l'elaborazione del contenuto all'interno di un elemento ignorato.  
  
 All'interno dell'attributo è possibile specificare diversi prefissi, utilizzando uno o più spazi come separatore, ad esempio `mc:Ignorable="ignore1 ignore2"`.  
  
 Lo spazio dei nomi [!INCLUDE[TLA#tla_mcxmlnsv1](../../../../includes/tlasharptla-mcxmlnsv1-md.md)] definisce altri elementi e attributi che non sono documentati all'interno di questa area del [!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)].  Per ulteriori informazioni, vedere [XML Markup Compatibility Specification](http://go.microsoft.com/fwlink/?LinkId=73824) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Markup.XamlReader>   
 [Attributo PresentationOptions:Freeze](../../../../docs/framework/wpf/advanced/presentationoptions-freeze-attribute.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)