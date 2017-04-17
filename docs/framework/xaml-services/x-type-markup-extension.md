---
title: "x:Type Markup Extension | Microsoft Docs"
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
  - "x:TypeExtension"
  - "Type"
  - "x:Type"
  - "xType"
  - "TypeExtension"
helpviewer_keywords: 
  - "x:Type markup extension [XAML Services]"
  - "XAML [XAML Services], x:Type markup extension"
  - "XAML [XAML Services], TargetType attribute"
  - "TargetType attribute [XAML Services]"
  - "Type markup extension in XAML [XAML Services]"
ms.assetid: e0e0ce6f-e873-49c7-8ad7-8b840eb353ec
caps.latest.revision: 27
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 27
---
# x:Type Markup Extension
Fornisce l'oggetto <xref:System.Type> CLR che è il tipo sottostante per un tipo XAML specificato.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object property="{x:Type prefix:typeNameValue}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<x:Type TypeName="prefix:typeNameValue"/>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`prefix`|Parametro facoltativo.  Prefisso che esegue il mapping di uno spazio dei nomi XAML non predefinito.  La specifica di un prefisso spesso non è necessaria.  Vedere la sezione Osservazioni.|  
|`typeNameValue`|Obbligatorio.  Un nome di tipo risolvibile nello spazio dei nomi XAML predefinito corrente oppure il prefisso specificato del quale è stato eseguito il mapping se viene fornito il parametro `prefix`.|  
  
## Note  
 L'estensione di markup `x:Type` dispone di una funzione simile all'operatore `typeof()` in [!INCLUDE[TLA#tla_cshrp](../../../includes/tlasharptla-cshrp-md.md)] o all'operatore `GetType` in [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)].  
  
 L'estensione di markup `x:Type` fornisce il comportamento di conversione da stringa per proprietà che prendono il tipo <xref:System.Type>.  L'input è un tipo XAML.  La relazione tra il tipo XAML di input e il CLR di output <xref:System.Type> è che l'output <xref:System.Type> è il <xref:System.Xaml.XamlType.UnderlyingType%2A> dell'input <xref:System.Xaml.XamlType>, dopo avere cercato il <xref:System.Xaml.XamlType> basato sul contesto dello schema XAML e sul servizio <xref:System.Windows.Markup.IXamlTypeResolver> fornito dal contesto.  
  
 Nei servizi XAML di .NET Framework la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.Markup.TypeExtension>.  
  
 In implementazioni framework specifiche, alcune proprietà che prendono <xref:System.Type> come un valore sono in grado di accettare direttamente il nome del tipo \(il valore della stringa del tipo `Name`\).  Tuttavia, l'implementazione di questo comportamento è uno scenario complesso.  Ad esempio, vedere la sezione "Note di utilizzo WPF" riportata di seguito.  
  
 La sintassi per gli attributi è quella più comunemente utilizzata con questa estensione di markup.  Il token di stringa fornito dopo la stringa dell'identificatore `x:Type` viene assegnato come valore <xref:System.Windows.Markup.TypeExtension.TypeName%2A> della classe dell'estensione <xref:System.Windows.Markup.TypeExtension> sottostante.  Sotto il contesto dello schema XAML predefinito per i Servizi XAML di .NET Framework, basati sui tipi CLR, il valore di questo attributo è <xref:System.Reflection.MemberInfo.Name%2A> del tipo desiderato o contiene <xref:System.Reflection.MemberInfo.Name%2A> preceduto da un prefisso per un mapping dello spazio dei nomi XAML non predefinito.  
  
 L'estensione di markup `x:Type` può essere utilizzata nella sintassi per gli elementi oggetto.  In questo caso, è richiesta la specifica del valore della proprietà <xref:System.Windows.Markup.TypeExtension.TypeName%2A> per inizializzare correttamente l'estensione.  
  
 L'estensione di markup `x:Type` può essere utilizzata anche come attributo dettagliato. tuttavia, questo utilizzo non è tipico: `<``object` `property``="{x:Type TypeName=``typeNameValue``}" .../>`  
  
## Note sull'utilizzo di WPF  
  
### Spazio dei nomi XAML e mapping del tipo predefiniti  
 Lo spazio dei nomi XAML predefinito per la programmazione WPF contiene la maggior parte dei tipi XAML di cui si ha bisogno per gli scenari XAML tipici; pertanto è spesso possibile evitare prefissi quando si fa riferimento a valori di tipo XAML.  È possibile che sia necessario eseguire il mapping di un prefisso se si fa riferimento a un tipo da un assembly personalizzato oppure per i tipi che esistono in un assembly WPF ma provengono da uno spazio dei nomi CLR per il quale non è stato eseguito il mapping allo spazio dei nomi XAML predefinito.  Per ulteriori informazioni sui prefissi, spazi dei nomi XAML e mapping degli spazi dei nomi CLR, vedere [Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF](../../../ocs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md).  
  
### Proprietà di tipi che supportano Nometipo\-come\-Stringa  
 WPF supporta tecniche che consentono di specificare il valore di alcune proprietà di tipo <xref:System.Type> senza richiedere un utilizzo dell'estensione di markup `x:Type`.  Al contrario, è possibile specificare il valore come una stringa che nomini il tipo.  Esempi di oggetti includono <xref:System.Windows.Controls.ControlTemplate.TargetType%2A?displayProperty=fullName> e <xref:System.Windows.Style.TargetType%2A?displayProperty=fullName>.  Il supporto per questo comportamento non è fornito mediante convertitori di tipi o estensioni di markup.  Al contrario, questo è un comportamento della proroga implementato mediante <xref:System.Windows.FrameworkElementFactory>.  
  
 Silverlight supporta una convenzione simile.  Infatti, Silverlight attualmente non supporta `{x:Type}` nel supporto del linguaggio XAML e non accetta gli utilizzi di `{x:Type}` all'esterno di alcune condizioni che sono concepite per supportare la migrazione tra WPF e Silverlight XAML.  Di conseguenza, il comportamento che prevede il nome del tipo come stringa è incorporato in tutte le valutazioni delle proprietà native di Silverlight, dove <xref:System.Type> è il valore.  
  
## XAML 2009  
 XAML 2009 fornisce supporto aggiuntivo per i tipi generici e modifica il comportamento della funzionalità di `x:TypeArguments` e `x:Type` per fornire questo supporto.  
  
-   `x:TypeArguments` e l'elemento oggetto associato per una creazione di istanze dell'oggetto generica possono essere sugli elementi diversi dalla radice.  Per ulteriori informazioni, vedere la sezione "XAML 2009" di [x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md).  
  
-   XAML 2009 supporta una sintassi per la specifica del vincolo di un tipo generico in markup.  Può essere utilizzato da `x:TypeArguments`, da `x:Type` o dalle due funzionalità in combinazione.  
  
-   Implementazione WPF XAML quando l'elaborazione di XAML 2009 per il caricamento aggiunge anche questa funzionalità al comportamento implicito della conversione dei tipi per determinate proprietà del framework che utilizzano il tipo <xref:System.Type>.  
  
 In WPF, è possibile utilizzare le funzionalità XAML 2009, ma solo per XAML separato \(XAML non compilato dal markup\).  Il codice XAML compilato dal markup per WPF e il modulo BAML di XAML non supportano attualmente le parole chiave e le funzionalità di XAML 2009.  
  
## Vedere anche  
 <xref:System.Windows.Style>   
 [Applicazione di stili e modelli](../../../ocs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)