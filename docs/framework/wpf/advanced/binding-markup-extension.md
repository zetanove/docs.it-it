---
title: "Associazione dell&#39;estensione di markup | Microsoft Docs"
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
  - "Binding"
helpviewer_keywords: 
  - "Binding (estensioni di markup)"
  - "XAML, Binding (estensione di markup)"
ms.assetid: 83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Associazione dell&#39;estensione di markup
Rinvia la trasformazione di un valore di proprietà in un valore associato a dati creando un oggetto espressione intermedio e interpretando il contesto dati applicato all'elemento e alla relativa associazione in fase di esecuzione.  
  
## Utilizzo dell'espressione Binding  
  
```  
<object property="{Binding}" .../>  
-or-  
<object property="{Binding  bindProp1=value1[, bindPropN=valueN]*}" ...  
/>  
-or-  
<object property="{Binding path}" .../>  
-or  
<object property="{Binding path[, bindPropN=valueN]*}" .../>  
```  
  
## Note sulla sintassi  
 In queste sintassi `[]` e `*` non sono valori letterali.  Sono parte di una notazione per indicare che è possibile utilizzare zero o più coppie *bindProp*`=`*valore*, in cui un separatore `,` delimita e precede ogni coppia *bindProp*`=`*valore*.  
  
 Tutte le proprietà elencate nella sezione "Proprietà Binding che possono essere impostate con l'estensione Binding" possono essere impostate anche tramite gli attributi di un elemento oggetto <xref:System.Windows.Data.Binding>.  Questa caratteristica, tuttavia, non costituisce l'effettivo utilizzo dell'estensione di markup di <xref:System.Windows.Data.Binding>, ma solo l'elaborazione generale di attributi che impostano proprietà della classe CLR <xref:System.Windows.Data.Binding>.  In altri termini, `<Binding` *propAss1*`="`*valore1*`"[` *propAssN*`="`*valoreN*`"]*/>` è una sintassi equivalente per gli attributi dell'utilizzo dell'elemento oggetto <xref:System.Windows.Data.Binding> anziché dell'utilizzo dell'espressione `Binding`.  Per ulteriori informazioni sull'utilizzo di attributi XAML per proprietà specifiche di <xref:System.Windows.Data.Binding>, vedere la sezione "Utilizzo della sintassi XAML per attributi" della proprietà pertinente di <xref:System.Windows.Data.Binding> nella libreria di classi .NET Framework.  
  
## Valori XAML  
  
|||  
|-|-|  
|`bindProp1, bindPropN`|Nome della proprietà <xref:System.Windows.Data.Binding> o <xref:System.Windows.Data.BindingBase> da impostare.  Non tutte le proprietà <xref:System.Windows.Data.Binding> possono essere impostate con l'estensione `Binding` e alcune proprietà possono essere impostate all'interno di un'espressione `Binding` solo utilizzando ulteriori estensioni di markup annidate.  Vedere la sezione "Proprietà Binding che possono essere impostate con l'estensione Binding".|  
|`value1, valueN`|Valore su cui impostare la proprietà.  La gestione del valore dell'attributo è essenzialmente specifica per il tipo e la logica della proprietà <xref:System.Windows.Data.Binding> specifica impostata.|  
|`path`|Stringa di percorso che imposta la proprietà <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> implicita.  Vedere anche [Sintassi XAML di PropertyPath](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md).|  
  
## {Binding} non qualificato  
 L'utilizzo di `{Binding}` illustrato in "Utilizzo dell'espressione Binding" crea un oggetto <xref:System.Windows.Data.Binding> con valori predefiniti, che include una proprietà <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> iniziale con valore `null`.  Si tratta di una caratteristica tuttora utile in molti scenari, in quanto l'oggetto <xref:System.Windows.Data.Binding> creato potrebbe basarsi su proprietà di associazione dati chiave, ad esempio le proprietà <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> e <xref:System.Windows.Data.Binding.Source%2A?displayProperty=fullName> impostate nel contesto dati di runtime.  Per ulteriori informazioni sul concetto di contesto dati, vedere [Data binding](../../../../docs/framework/wpf/data/data-binding-wpf.md).  
  
## Percorso implicito  
 L'estensione di markup `Binding` utilizza <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> come "proprietà predefinita" concettuale, in cui `Path=` non deve essere visualizzato nell'espressione.  Se si specifica un'espressione `Binding` con un percorso implicito, tale percorso implicito deve essere visualizzato innanzitutto nell'espressione, prima di qualsiasi altra coppia `bindProp`\=`value` in cui la proprietà <xref:System.Windows.Data.Binding> è specificata per nome.  Ad esempio: `{Binding PathString}`, dove `PathString` è una stringa che restituisce il valore di <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> nell'oggetto <xref:System.Windows.Data.Binding> creato dall'utilizzo dell'estensione di markup.  È possibile aggiungere un percorso implicito con altre proprietà denominate dopo il separatore virgola, ad esempio `{Binding LastName, Mode=TwoWay}`.  
  
## Proprietà Binding che possono essere impostate con l'estensione Binding  
 La sintassi illustrata in questo argomento utilizza l'approssimazione `bindProp`\=`value` generica, in quanto sono presenti molte proprietà di lettura\/scrittura di <xref:System.Windows.Data.BindingBase> o <xref:System.Windows.Data.Binding> che possono essere impostate tramite sintassi per estensioni di markup e\/o espressioni  `Binding`.  Queste proprietà possono essere impostate in qualsiasi ordine, ad eccezione di un oggetto <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> implicito.  È possibile specificare in modo esplicito `Path=`. In questo caso, questa proprietà potrà essere impostata in qualsiasi ordine.  Fondamentalmente, è possibile impostare zero o più proprietà incluse nell'elenco seguente utilizzando coppie `bindProp`\=`value` separate da virgole.  
  
 Alcuni di questi valori di proprietà richiedono tipi di oggetto che non supportano una conversione dei tipi nativi da una sintassi di testo in XAML. Sono pertanto necessarie estensioni di markup per impostare tali valori come valori di attributo.  Per ulteriori informazioni, controllare la sezione Utilizzo della sintassi XAML per attributi nella libreria di classi .NET Framework per ogni proprietà. La stringa utilizzata per la sintassi degli attributi XAML con o senza un ulteriore utilizzo di estensioni di markup è fondamentalmente identica al valore specificato in un'espressione `Binding`, ad eccezione del fatto che non è necessario racchiudere tra virgolette ogni coppia `bindProp`\=`value` nell'espressione  `Binding`.  
  
-   <xref:System.Windows.Data.BindingBase.BindingGroupName%2A>: stringa che identifica un possibile gruppo di associazione.  Si tratta di un concetto di associazione relativamente avanzato. Vedere la pagina di riferimento per <xref:System.Windows.Data.BindingBase.BindingGroupName%2A>.  
  
-   <xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A>: valore booleano, può essere `true` o `false`.  Il valore predefinito è `false`.  
  
-   <xref:System.Windows.Data.Binding.Converter%2A>: può essere impostata come stringa `bindProp`\=`value` nell'espressione, ma a tale scopo è necessario un riferimento a un oggetto per il valore, ad esempio un'[Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md).  Il valore in questo caso è un'istanza di una classe del convertitore personalizzata.  
  
-   <xref:System.Windows.Data.Binding.ConverterCulture%2A>: può essere impostata nell'espressione come identificativo basato su standard. Vedere l'argomento di riferimento per <xref:System.Windows.Data.Binding.ConverterCulture%2A>.  
  
-   <xref:System.Windows.Data.Binding.ConverterParameter%2A>: può essere impostata come stringa `bindProp`\=`value` nell'espressione, ma ciò dipende dal tipo del parametro passato.  Se viene passato un tipo di riferimento per il valore, è necessario un riferimento a un oggetto, ad esempio un oggetto [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) annidato.  
  
-   <xref:System.Windows.Data.Binding.ElementName%2A>: si esclude reciprocamente con le proprietà di associazione <xref:System.Windows.Data.Binding.RelativeSource%2A> e <xref:System.Windows.Data.Binding.Source%2A>, ciascuna delle quali rappresenta una metodologia di associazione specifica.  Vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
-   <xref:System.Windows.Data.BindingBase.FallbackValue%2A>: può essere impostata come stringa `bindProp`\=`value` nell'espressione, ma ciò dipende dal tipo del valore passato.  Se viene passato un tipo di riferimento, è necessario un riferimento a un oggetto, ad esempio un oggetto [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) annidato.  
  
-   <xref:System.Windows.Data.Binding.IsAsync%2A>: valore booleano, può essere `true` o `false`.  Il valore predefinito è `false`.  
  
-   <xref:System.Windows.Data.Binding.Mode%2A>: *valore* è un nome di costante dell'enumerazione <xref:System.Windows.Data.BindingMode>.  Ad esempio `{Binding Mode=OneWay}`.  
  
-   <xref:System.Windows.Data.Binding.NotifyOnSourceUpdated%2A>: valore booleano, può essere `true` o `false`.  Il valore predefinito è `false`.  
  
-   <xref:System.Windows.Data.Binding.NotifyOnTargetUpdated%2A>: valore booleano, può essere `true` o `false`.  Il valore predefinito è `false`.  
  
-   <xref:System.Windows.Data.Binding.NotifyOnValidationError%2A>: valore booleano, può essere `true` o `false`.  Il valore predefinito è `false`.  
  
-   <xref:System.Windows.Data.Binding.Path%2A>: stringa che descrive un percorso in un oggetto dati o un modello a oggetti generale.  Il formato fornisce molte convenzioni diverse per attraversare un modello a oggetti, che non possono essere descritte in modo adeguato in questa sede.  Vedere [Sintassi XAML di PropertyPath](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md).  
  
-   <xref:System.Windows.Data.Binding.RelativeSource%2A>: si esclude reciprocamente con le proprietà <xref:System.Windows.Data.Binding.ElementName%2A> e <xref:System.Windows.Data.Binding.Source%2A>; ciascuna di queste proprietà di associazione rappresenta una metodologia di associazione specifica.  Vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  Richiede l'utilizzo di un'[Estensione del markup RelativeSource](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md) annidata per specificare il valore.  
  
-   <xref:System.Windows.Data.Binding.Source%2A>: si esclude reciprocamente con le proprietà di associazione <xref:System.Windows.Data.Binding.RelativeSource%2A> e <xref:System.Windows.Data.Binding.ElementName%2A>, ciascuna delle quali rappresenta una metodologia di associazione specifica.  Vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  Richiede l'utilizzo di un'estensione annidata, in genere un'[Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) che fa riferimento a un'origine dati oggetto da un dizionario risorse con chiave.  
  
-   <xref:System.Windows.Data.BindingBase.StringFormat%2A>: stringa che descrive una convenzione del formato stringa per i dati associati.  Si tratta di un concetto di associazione relativamente avanzato. Vedere la pagina di riferimento per <xref:System.Windows.Data.BindingBase.StringFormat%2A>.  
  
-   <xref:System.Windows.Data.BindingBase.TargetNullValue%2A>: può essere impostata come stringa `bindProp`\=`value` nell'espressione, ma ciò dipende dal tipo del parametro passato.  Se viene passato un tipo di riferimento per il valore, è necessario un riferimento a un oggetto, ad esempio un oggetto [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) annidato.  
  
-   <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>: *valore* è un nome di costante dell'enumerazione <xref:System.Windows.Data.UpdateSourceTrigger>.  Ad esempio `{Binding UpdateSourceTrigger=LostFocus}`.  I controlli specifici possono presentare valori predefiniti diversi per questa proprietà di associazione.  Vedere <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>.  
  
-   <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A>: valore booleano, può essere `true` o `false`.  Il valore predefinito è `false`.  Vedere la sezione Osservazioni.  
  
-   <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A>: valore booleano, può essere `true` o `false`.  Il valore predefinito è `false`.  Vedere la sezione Osservazioni.  
  
-   <xref:System.Windows.Data.Binding.XPath%2A>: stringa che descrive un percorso nell'oggetto XMLDOM di un'origine dati XML.  Vedere [Eseguire l'associazione ai dati XML utilizzando un oggetto XMLDataProvider e le query XPath](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md).  
  
 Di seguito sono riportate le proprietà di <xref:System.Windows.Data.Binding> che non possono essere impostate utilizzando l'estensione di markup `Binding` o il formato di espressione `{Binding}`.  
  
-   <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A>: questa proprietà prevede un riferimento a un'implementazione di callback.  Nella sintassi XAML non è possibile fare riferimento a callback\/metodi diversi dai gestori eventi.  
  
-   <xref:System.Windows.Data.Binding.ValidationRules%2A>: proprietà che accetta una raccolta generica di oggetti <xref:System.Windows.Controls.ValidationRule>.  Tale insieme può essere espresso come elemento proprietà in un elemento oggetto <xref:System.Windows.Data.Binding>, ma non dispone tempestivamente di alcuna tecnica di analisi degli attributi per l'utilizzo in un'espressione `Binding`.  Vedere l'argomento di riferimento per <xref:System.Windows.Data.Binding.ValidationRules%2A>.  
  
-   <xref:System.Windows.Data.Binding.XmlNamespaceManager%2A>  
  
## Note  
  
> [!IMPORTANT]
>  In termini di precedenza della proprietà di dipendenza, un'espressione `Binding` equivale a un valore impostato localmente.  Se viene impostato un valore locale per una proprietà che in precedenza conteneva un'espressione `Binding`, `Binding` viene completamente rimosso.  Per informazioni dettagliate, vedere [Precedenza del valore della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md).  
  
 La descrizione dell'associazione dati a un livello di base non è discussa in questo argomento.  Vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
> [!NOTE]
>  <xref:System.Windows.Data.MultiBinding> e <xref:System.Windows.Data.PriorityBinding> non supportano la sintassi di estensione di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. Si utilizzano invece gli elementi di proprietà.  Vedere gli argomenti di riferimento per <xref:System.Windows.Data.MultiBinding> e <xref:System.Windows.Data.PriorityBinding>.  
  
 I valori booleani di XAML non prevedono la distinzione tra maiuscole e minuscole.  Ad esempio è possibile specificare `{Binding NotifyOnValidationError=true}` oppure `{Binding NotifyOnValidationError=True}`.  
  
 Le associazioni che comportano la convalida dei dati in genere vengono specificate da un elemento `Binding` esplicito piuttosto che come un'espressione `{Binding ...}` e impostare <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> o <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> in un'espressione non è comune.  Ciò è dovuto al fatto che non è possibile impostare prontamente la proprietà <xref:System.Windows.Data.Binding.ValidationRules%2A> complementare nel formato di espressione.  Per ulteriori informazioni, vedere [Implementare la convalida dell'associazione](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md).  
  
 `Binding` è un'estensione di markup.  Le estensioni di markup vengono in genere implementate quando un requisito stabilisce che i valori degli attributi non devono essere diversi da valori letterali o nomi di gestori e tale requisito è più globale dei convertitori di tipi assegnati come attribuito ad alcuni tipi o proprietà.  Tutte le estensioni di markup in XAML utilizzano i caratteri `{` e `}` nella relativa sintassi degli attributi. Si tratta della convenzione che consente al processore XAML di determinare che un'estensione di markup deve elaborare il contenuto della stringa.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
 `Binding` è un'estensione di markup insolita, nel senso che la classe <xref:System.Windows.Data.Binding> che implementa la funzionalità dell'estensione per l'implementazione XAML di WPF implementa anche numerosi altri metodi e proprietà non correlati a XAML.  Gli altri membri vengono utilizzati per rendere <xref:System.Windows.Data.Binding> una classe più versatile e indipendente in grado di gestire molti scenari di associazione dati, nonché di fungere da estensione di markup XAML.  
  
## Vedere anche  
 <xref:System.Windows.Data.Binding>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)