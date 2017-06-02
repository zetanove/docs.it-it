---
title: "Estensione del markup RelativeSource | Microsoft Docs"
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
  - "RelativeSource"
helpviewer_keywords: 
  - "RelativeSource (estensioni di markup)"
  - "XAML, RelativeSource (estensione di markup)"
ms.assetid: 26be4721-49b5-4717-a92e-7d54ad0d3a81
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Estensione del markup RelativeSource
Specifica le proprietà di un'origine di associazione <xref:System.Windows.Data.RelativeSource>, da utilizzare in un [Associazione dell'estensione di markup](../../../../docs/framework/wpf/advanced/binding-markup-extension.md) o per l'impostazione della proprietà <xref:System.Windows.Data.Binding.RelativeSource%2A> di un elemento <xref:System.Windows.Data.Binding> in XAML.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<Binding RelativeSource="{RelativeSource modeEnumValue}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli attributi \(annidati nell'estensione Binding\)  
  
```  
<object property="{Binding RelativeSource={RelativeSource modeEnumValue} ...}" .../>  
```  
  
## Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<Binding>  
  <Binding.RelativeSource>  
    <RelativeSource Mode="modeEnumValue"/>  
  </Binding.RelativeSource>  
</Binding>  
- or   
<Binding>  
  <Binding.RelativeSource>  
    <RelativeSource  
      Mode="FindAncestor"  
      AncestorType="{x:Type typeName}"  
      AncestorLevel="intLevel"  
    />  
  </Binding.RelativeSource>  
</Binding>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`modeEnumValue`|Uno dei seguenti:<br /><br /> -   Token stringa `Self`; corrisponde a un oggetto <xref:System.Windows.Data.RelativeSource> creato con la proprietà <xref:System.Windows.Data.RelativeSource.Mode%2A> impostata su <xref:System.Windows.Data.RelativeSourceMode>.<br />-   Token stringa `TemplatedParent`; corrisponde a un oggetto <xref:System.Windows.Data.RelativeSource> creato con la proprietà <xref:System.Windows.Data.RelativeSource.Mode%2A> impostata su <xref:System.Windows.Data.RelativeSourceMode>.<br />-   Token stringa `PreviousData`; corrisponde a un oggetto <xref:System.Windows.Data.RelativeSource> creato con la proprietà <xref:System.Windows.Data.RelativeSource.Mode%2A> impostata su <xref:System.Windows.Data.RelativeSourceMode>.<br />-   Per informazioni sulla modalità `FindAncestor`, vedere di seguito.|  
|`FindAncestor`|Token stringa `FindAncestor`.  L'utilizzo di questo token consente di accedere a una modalità in cui `RelativeSource` specifica un tipo predecessore e facoltativamente un livello predecessore.  Corrisponde a un oggetto <xref:System.Windows.Data.RelativeSource> creato con la proprietà <xref:System.Windows.Data.RelativeSource.Mode%2A> impostata su <xref:System.Windows.Data.RelativeSourceMode>.|  
|`typeName`|Obbligatorio per la modalità `FindAncestor`.  Nome di un tipo che riempie la proprietà <xref:System.Windows.Data.RelativeSource.AncestorType%2A>.|  
|`intLevel`|Facoltativo per la modalità `FindAncestor`.  Livello predecessore \(valutato nella direzione padre dell'albero logico\).|  
  
## Note  
 Gli utilizzi dell'associazione `{RelativeSource TemplatedParent}` rappresentano una tecnica importante che risolve un concetto più ampio di separazione dell'interfaccia utente di un controllo e la logica di un controllo.  Ciò consente l'associazione dall'interno della definizione del modello al padre basato su modelli \(istanza dell'oggetto in fase di esecuzione alla quale è applicato il modello\).  In questo caso, [Estensione del markup TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) è in effetti una forma abbreviata della seguente espressione di associazione: `{Binding RelativeSource={RelativeSource TemplatedParent}}`.  Gli utilizzi di `TemplateBinding` o di `{RelativeSource TemplatedParent}` sono entrambi rilevanti solo all'interno del codice XAML che definisce un modello.  Per ulteriori informazioni, vedere [Estensione del markup TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md).  
  
 `{RelativeSource FindAncestor}` viene utilizzato prevalentemente nei modelli di controllo o nelle composizioni di interfaccia utente autonome prevedibili, per i casi in cui si prevede che un controllo sia sempre presente in una struttura ad albero visuale di un determinato tipo di predecessore.  Ad esempio, gli elementi di un controllo di elementi potrebbero utilizzare `FindAncestor` per associarsi alle proprietà del relativo predecessore padre del controllo di elementi.  In alternativa, gli elementi che fanno parte della composizione del controllo in un modello possono utilizzare le associazioni `FindAncestor` agli elementi padre nella stessa struttura della composizione.  
  
 Nella sintassi dell'elemento oggetto per la modalità `FindAncestor` illustrata nelle sezioni sulla sintassi XAML, la sintassi del secondo elemento oggetto viene utilizzata specificamente per la modalità `FindAncestor`.  La modalità `FindAncestor` richiede un valore <xref:System.Windows.Data.RelativeSource.AncestorType%2A>.  È necessario impostare <xref:System.Windows.Data.RelativeSource.AncestorType%2A> come attributo utilizzando un riferimento [Estensione del markup x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md) al tipo di predecessore da cercare.  Il valore <xref:System.Windows.Data.RelativeSource.AncestorType%2A> viene utilizzato quando la richiesta di associazione viene elaborata in fase di esecuzione.  
  
 Per la modalità `FindAncestor`, la proprietà facoltativa <xref:System.Windows.Data.RelativeSource.AncestorLevel%2A> consente di rendere meno ambigua la ricerca del predecessore laddove vi sono più predecessori di questo tipo nella struttura ad albero dell'elemento.  
  
 Per ulteriori informazioni su come utilizzare la modalità `FindAncestor`, vedere <xref:System.Windows.Data.RelativeSource>.  
  
 `{RelativeSource Self}` è utile per gli scenari in cui una proprietà di un'istanza deve dipendere dal valore di un'altra proprietà della stessa istanza e non esiste alcuna relazione generale di proprietà di dipendenza \(come la coercizione\) tra queste due proprietà.  Sebbene sia raro che esistano due proprietà su un oggetto con valori letteralmente identici \(e dello stesso tipo\), è possibile applicare anche un parametro `Converter` a un'associazione con `{RelativeSource Self}` e utilizzare il convertitore per eseguire la conversione tra i tipi di origine e di destinazione.  Un altro scenario per `{RelativeSource Self}` è una parte di un <xref:System.Windows.MultiDataTrigger>.  
  
 Ad esempio, nel codice XAML seguente viene definito un elemento <xref:System.Windows.Shapes.Rectangle> in modo che, indipendentemente dal valore inserito per <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.Shapes.Rectangle> sia sempre un quadrato: `<Rectangle Width="200" Height="{Binding RelativeSource={RelativeSource Self}, Path=Width}" .../>`  
  
 `{RelativeSource PreviousData}` è utile nei modelli di dati oppure nei casi in cui le associazioni utilizzano una raccolta come origine dati.  È possibile utilizzare `{RelativeSource PreviousData}` per evidenziare le relazioni tra gli elementi di dati adiacenti nella raccolta.  Una tecnica correlata consiste nel porre un oggetto <xref:System.Windows.Data.MultiBinding> tra l'elemento corrente e quello precedente nell'origine dati e utilizzare un convertitore su quell'associazione per determinare la differenza tra i due elementi e le relative proprietà.  
  
 Nell'esempio riportato di seguito, il primo <xref:System.Windows.Controls.TextBlock> in un modello di elementi visualizza il numero corrente.  La seconda associazione <xref:System.Windows.Controls.TextBlock> è un oggetto <xref:System.Windows.Data.MultiBinding> che nominalmente presenta due componenti <xref:System.Windows.Data.Binding>: il record corrente e un'associazione che utilizza intenzionalmente il record di dati precedente utilizzando `{RelativeSource PreviousData}`.  Quindi, un convertitore applicato a <xref:System.Windows.Data.MultiBinding> calcola la differenza e la restituisce all'associazione.  
  
```  
<ListBox Name="fibolist">  
    <ListBox.ItemTemplate>  
        <DataTemplate>  
            <StackPanel Orientation="Horizontal">  
            <TextBlock Text="{Binding}"/>  
            <TextBlock>, difference = </TextBlock>  
                <TextBlock>  
                    <TextBlock.Text>  
                        <MultiBinding Converter="{StaticResource DiffConverter}">  
                            <Binding/>  
                            <Binding RelativeSource="{RelativeSource PreviousData}"/>  
                        </MultiBinding>  
                    </TextBlock.Text>  
                </TextBlock>  
            </StackPanel>  
            </DataTemplate>  
    </ListBox.ItemTemplate>  
```  
  
 La descrizione dell'associazione dati come concetto non viene trattata in questo argomento; vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 Nell'implementazione del processore XAML di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la gestione di questa estensione di markup viene definita dalla classe <xref:System.Windows.Data.RelativeSource>.  
  
 `RelativeSource` è un'estensione di markup.  Le estensioni di markup in genere vengono implementate quando per i valori dell'attributo devono essere utilizzati caratteri escape in modo che non vengano considerati come valori letterali o nomi di gestori e il requisito è più globale del semplice utilizzo di convertitori dei tipi su alcuni tipi o proprietà.  Per tutte le estensioni di markup in XAML vengono utilizzati i caratteri `{` e `}` nella relativa sintassi degli attributi, vale a dire la convenzione in base alla quale il processore XAML riconosce che l'attributo deve essere elaborato da un'estensione di markup.  Per ulteriori informazioni, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
## Vedere anche  
 <xref:System.Windows.Data.Binding>   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sulle dichiarazioni di associazione](../../../../docs/framework/wpf/data/binding-declarations-overview.md)   
 [Estensione del markup x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md)