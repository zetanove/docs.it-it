---
title: "x:Key Directive | Microsoft Docs"
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
  - "xKey"
  - "Key"
  - "x:Key"
helpviewer_keywords: 
  - "x:Key attribute [XAML Services]"
  - "Key attribute in XAML [XAML Services]"
  - "XAML [XAML Services], x:Key attribute"
ms.assetid: 1985cd45-f197-42d5-b75e-886add64b248
caps.latest.revision: 25
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 25
---
# x:Key Directive
Identifica in modo univoco gli elementi creati a cui viene fatto riferimento in un dizionario definito in XAML.  L'aggiunta di un valore `x:Key` a un elemento oggetto XAML è il metodo più comune per identificare una risorsa in un dizionario risorse, ad esempio in <xref:System.Windows.ResourceDictionary>WPF.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:Key="stringKeyValue".../>  
-or-  
<object x:Key="{markupExtensionUsage}".../>  
```  
  
## Utilizzo degli attributi XAML \(specifico per WPF\)  
  
```  
<object.Resources>  
  <object x:Key="stringKeyValue".../>  
</object.Resources>  
-or-  
<object.Resources>  
  <object x:Key="{markupExtensionUsage}".../>  
</object.Resources>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`stringKeyValue`|Stringa da utilizzare come chiave.  La stringa del testo deve essere conforme a [Grammatica XamlName](../../../docs/framework/xaml-services/xamlname-grammar.md).|  
|`markupExtensionUsage`|All'interno dei delimitatori dell'estensione di markup {}, un utilizzo dell'estensione di markup che fornisce un oggetto da utilizzare come chiave.  Vedere la sezione Osservazioni.|  
  
## Note  
 `x:Key` supporta il concetto di dizionario risorse XAML.  XAML come linguaggio non definisce un'implementazione del dizionario risorse, ciò è lasciato a framework specifici dell'interfaccia utente.  Per ulteriori informazioni sull'implementazione dei dizionari delle risorse XAML in WPF, vedere [Risorse XAML](../../../ocs/framework/wpf/advanced/xaml-resources.md).  
  
 In XAML 2006 e WPF, è necessario fornire `x:Key` come attributo.  È possibile ancora utilizzare chiavi non di tipo stringa, ma questo richiede un utilizzo dell'estensione di markup per fornire il valore non di tipo stringa sotto forma d'attributo.  Se si utilizza XAML 2009, è possibile specificare `x:Key` come elemento, per supportare in modo esplicito dizionari adattati dai tipi di oggetti diversi dalle stringhe senza richiedere un'estensione di markup intermedio.  Vedere la sezione "XAML 2009" in questo argomento.  Il resto della sezione Osservazioni si applica in maniera specifica all'implementazione XAML 2006.  
  
 Il valore di attributo di `x:Key` può essere qualsiasi stringa definita nella [Grammatica XamlName](../../../docs/framework/xaml-services/xamlname-grammar.md) o un oggetto valutato tramite un'estensione di markup.  Per avere un esempio, vedere in WPF "Note di utilizzo WPF".  
  
 Gli elementi figlio di un elemento padre che è un'implementazione di <xref:System.Collections.IDictionary> devono in genere includere un attributo `x:Key` che specifica un valore di chiave univoco in tale dizionario.  I framework potrebbero implementare le proprietà della chiave con alias da sostituire per `x:Key` sui particolari tipi; tipi che definiscono ad esempio le proprietà che dovrebbero essere attribuite con <xref:System.Windows.Markup.DictionaryKeyPropertyAttribute>.  
  
 L'equivalente della specifica di `x:Key` nel codice è la chiave, così come viene utilizzata con l'oggetto <xref:System.Collections.IDictionary> sottostante.  Ad esempio, `x:Key` applicato nel markup a una risorsa in WPF equivale al valore del parametro `key` di <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=fullName> quando si aggiunge la risorsa a un WPF <xref:System.Windows.ResourceDictionary> nel codice.  
  
## Note sull'utilizzo di WPF  
 Gli oggetti figlio di un oggetto padre che è un'implementazione di <xref:System.Collections.IDictionary>, come ad esempio il <xref:System.Windows.ResourceDictionary> WPF, devono in genere includere un attributo `x:Key` e un valore di chiave univoco in tale dizionario.  Esistono due importanti eccezioni:  
  
-   Alcuni tipi WPF dichiarano una chiave implicita per l'utilizzo di dizionario.  Ad esempio, un <xref:System.Windows.Style> con un <xref:System.Windows.Style.TargetType%2A> o un <xref:System.Windows.DataTemplate> con un <xref:System.Windows.DataTemplate.DataType%2A>, può essere presente in un <xref:System.Windows.ResourceDictionary> ed utilizzare la chiave implicita.  
  
-   WPF supporta un concetto di dizionario delle risorse unito.  Le chiavi possono essere condivise tra i dizionari uniti e l'accesso al comportamento principale condiviso può essere eseguito utilizzando <xref:System.Windows.FrameworkContentElement.FindResource%2A>.  Per ulteriori informazioni, vedere [Dizionari risorse uniti](../../../ocs/framework/wpf/advanced/merged-resource-dictionaries.md).  
  
 Nell'implementazione XAML WPF complessiva e nel modello dell'applicazione, l'univocità delle chiavi non è controllata dal compilatore del markup XAML.  Invece, i valori `x:Key` mancanti e\/o non univoci generano errori del parser XAML in fase di caricamento.  Tuttavia, la gestione di [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] dei dizionari per WPF può spesso riscontrare tali errori in fase di progettazione.  
  
 Si noti che nella sintassi illustrata l'oggetto <xref:System.Windows.ResourceDictionary> è implicito nel modo in cui il processore XAML WPF produce una raccolta per popolare una raccolta <xref:System.Windows.FrameworkElement.Resources%2A>.  <xref:System.Windows.ResourceDictionary> non viene in genere fornito in modo esplicito come elemento nel markup, benché ciò sia possibile in alcuni casi se lo si ritiene opportuno per motivi di chiarezza \(si tratterebbe di un elemento dell'oggetto Collection tra l'elemento di proprietà <xref:System.Windows.FrameworkElement.Resources%2A> e le voci al suo interno che compilano il dizionario\).  Per informazioni sul motivo per cui un oggetto Collection sia quasi sempre un elemento implicito nel markup, vedere [Descrizione dettagliata della sintassi XAML](../../../ocs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
 Nell'implementazione WPF XAML, la gestione delle chiavi di dizionario risorse è definita dalla classe astratta <xref:System.Windows.ResourceKey>.  Il processore XAML WPF, tuttavia, produce diversi tipi di estensione sottostanti per le chiavi in base al relativo utilizzo.  Ad esempio, la chiave per <xref:System.Windows.DataTemplate> o per qualsiasi classi derivata viene gestita separatamente e produce un oggetto <xref:System.Windows.DataTemplateKey> distinto.  
  
 Chiavi e nomi utilizzano direttive ed elementi di linguaggio \(`x:Key` contro `x:Name`\) diversi nella definizione XAML di base.  Chiavi e nomi sono utilizzati anche in situazioni diverse dalla definizione WPF e dall'applicazione di questi concetti.  Per informazioni dettagliate, vedere [NameScope XAML WPF](../../../ocs/framework/wpf/advanced/wpf-xaml-namescopes.md).  
  
 Come dichiarato precedentemente, il valore di una chiave può essere fornito tramite un'estensione di markup e può essere diverso da un valore stringa.  Un scenario WPF di esempio è quello in cui il valore di `x:Key` può essere un [ComponentResourceKey](../../../ocs/framework/wpf/advanced/componentresourcekey-markup-extension.md).  Determinati controlli espongono una chiave di stile del tipo per creare una risorsa di stile personalizzata che influenza in parte l'aspetto e il comportamento di tale controllo senza sostituirne totalmente lo stile.  Un esempio di questo tipo di chiave è <xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A>.  
  
 Le funzionalità del dizionario unito WPF introducono considerazioni aggiuntive riguardo all'univocità delle chiavi e al comportamento della ricerca della chiave.  Per ulteriori informazioni, vedere [Dizionari risorse uniti](../../../ocs/framework/wpf/advanced/merged-resource-dictionaries.md).  
  
## XAML 2009  
 XAML 2009 rilassa la restrizione che `x:Key` venga fornito sempre in formato attributo.  
  
 In WPF è possibile utilizzare le funzionalità di XAML 2009, ma solo per il codice XAML non compilato dal markup.  Il codice XAML compilato dal markup per WPF e il modulo BAML di XAML non supportano attualmente le parole chiave e le funzionalità di XAML 2009.  
  
 In XAML 2009, è possibile specificare gli elementi `x:Key` tramite l'utilizzo seguente:  
  
### Utilizzo della sintassi XAML per gli elementi \(solo XAML 2009\)  
  
```  
<object>  
  <x:Key>  
     keyObject  
  </x:Key>  
...  
</object>  
```  
  
### Valori XAML  
  
|||  
|-|-|  
|`keyObject`|L'elemento oggetto per l'oggetto utilizzato come chiave per un `object` specificato in un dizionario specializzato.|  
  
-   Il contenitore\/padre per questo tipo di utilizzo non viene visualizzato qui.  E' previsto che `object` sia figlio di un elemento oggetto che rappresenta un'implementazione di dizionario specializzato.  `keyObject` è previsto che sia un'istanza dell'oggetto \(o un valore di un tipo di valore\) che è appropriata come chiave per quella particolare implementazione del dizionario specializzato.  
  
-   WPF non implementa dizionari che richiedono questo utilizzo.  Gli oggetti utilizzati come chiavi sono una funzionalità generale del linguaggio XAML, utile per determinati scenari di dizionario personalizzato dove la creazione del dizionario in XAML è preferibile.  Per le funzionalità WPF quali stili impliciti che utilizzano chiavi non di tipo stringa per le risorse, altre tecniche per stabilire o  specificare che le chiavi esistono, in modo che l'utilizzo di una chiave dell'oggetto non è necessario.  
  
-   *keyObject* potrebbe essere anche un utilizzo dell'estensione di markup nel formato dell'elemento oggetto, piuttosto che un'istanza dell'oggetto diretta.  
  
## Note sull'utilizzo di Silverlight.  
 `x:Key` per Silverlight è documentato separatamente.  Per ulteriori informazioni, vedere la pagina relativa alle [funzionalità del linguaggio \(Silverlight\) dello spazio dei nomi XAML \(x:\)](http://go.microsoft.com/fwlink/?LinkId=199081).  
  
## Vedere anche  
 [Risorse XAML](../../../ocs/framework/wpf/advanced/xaml-resources.md)   
 [Risorse e codice](../../../ocs/framework/wpf/advanced/resources-and-code.md)   
 [Estensione del markup StaticResource](../../../ocs/framework/wpf/advanced/staticresource-markup-extension.md)