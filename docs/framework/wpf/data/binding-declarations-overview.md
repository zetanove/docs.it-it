---
title: "Cenni preliminari sulle dichiarazioni di associazione | Microsoft Docs"
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
  - "associazione dati, dichiarazioni"
  - "associazione di dichiarazioni"
  - "associazione dati, dichiarazioni"
  - "estensioni di markup"
  - "sintassi degli elementi oggetto"
  - "sintassi, elementi oggetto"
ms.assetid: b97fd626-4c0d-4761-872a-2bca5820da2c
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# Cenni preliminari sulle dichiarazioni di associazione
In questo argomento vengono presentati i diversi modi in cui è possibile dichiarare un'associazione.  
  
   
  
<a name="Prereq"></a>   
## Prerequisiti  
 Prima di leggere questo argomento, è importante avere familiarità con il concetto e l'utilizzo delle estensioni di markup.  Per ulteriori informazioni sulle estensioni di markup, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
 In questo argomento non vengono illustrati i concetti relativi all'associazione dati.  Per informazioni sui concetti relativi all'associazione dati, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
<a name="BindinginXAML"></a>   
## Dichiarazione di un'associazione in XAML  
 In questa sezione viene illustrata la modalità di dichiarazione di un'associazione in XAML.  
  
<a name="MarkupExtensionSyntax"></a>   
### Utilizzo delle estensioni di markup  
 <xref:System.Windows.Data.Binding> è un'estensione di markup.  Quando si utilizza l'estensione dell'associazione per dichiarare un'associazione, tale dichiarazione sarà costituita da una serie di clausole che seguono la parola chiave `Binding` e sono separate tramite virgole \(,\).  Le clausole della dichiarazione di associazione possono essere disposte in qualsiasi ordine, fornendo così molte possibili combinazioni.  Le clausole sono composte da coppie *Nome*\=*Valore*, dove *Nome* corrisponde al nome della proprietà <xref:System.Windows.Data.Binding> e *Valore* corrisponde al valore che si imposta per la proprietà.  
  
 Quando si creano stringhe di dichiarazione di associazione nel markup, queste devono essere associate alla [proprietà di dipendenza](GTMT) specifica di un oggetto di destinazione.  Nell'esempio seguente viene illustrato come associare la proprietà <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName> utilizzando l'estensione dell'associazione e specificando le proprietà <xref:System.Windows.Data.Binding.Source%2A> e <xref:System.Windows.Data.Binding.Path%2A>.  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 È possibile specificare la maggior parte delle proprietà della classe <xref:System.Windows.Data.Binding> in questo modo.  Per ulteriori informazioni sull'estensione dell'associazione e per un elenco di proprietà <xref:System.Windows.Data.Binding> che non possono essere impostate utilizzando l'estensione dell'associazione, vedere i cenni preliminari su [Associazione dell'estensione di markup](../../../../docs/framework/wpf/advanced/binding-markup-extension.md).  
  
<a name="ObjectElementSyntax"></a>   
### Sintassi per elementi oggetto  
 La sintassi per elementi oggetto rappresenta un'alternativa alla creazione della dichiarazione di associazione.  Nella maggior parte dei casi, l'utilizzo dell'estensione di markup rispetto alla sintassi per elementi oggetto non presenta specifici vantaggi.  Tuttavia, nei casi in cui l'estensione di markup non supporta uno specifico scenario, ad esempio quando il valore della proprietà è di un tipo non stringa per il quale non sono previste conversioni di tipo, sarà necessario utilizzare la sintassi per elementi oggetto.  
  
 Di seguito viene riportato un esempio dell'utilizzo sia della sintassi per elementi oggetto, sia dell'estensione di markup:  
  
 [!code-xml[BindConversionMarkup#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindConversionMarkup/CSharp/Page1.xaml#1)]  
  
 Nell'esempio, la proprietà <xref:System.Windows.Controls.TextBlock.Foreground%2A> viene associata dichiarando un'associazione tramite la sintassi di estensione.  La dichiarazione di associazione per la proprietà <xref:System.Windows.Controls.TextBlock.Text%2A> utilizza la sintassi per elementi oggetto.  
  
 Per ulteriori informazioni sui diversi termini, vedere [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
<a name="MBandPB"></a>   
### MultiBinding e PriorityBinding  
 <xref:System.Windows.Data.MultiBinding> e <xref:System.Windows.Data.PriorityBinding> non supportano la sintassi di estensione XAML.  Pertanto, se si sta dichiarando un oggetto <xref:System.Windows.Data.MultiBinding> o <xref:System.Windows.Data.PriorityBinding> in XAML, è necessario utilizzare la sintassi per elementi oggetto.  
  
<a name="BindinginCode"></a>   
## Creazione di un'associazione nel codice  
 Un altro modo per specificare un'associazione consiste nell'impostare le proprietà direttamente su un oggetto <xref:System.Windows.Data.Binding> nel codice.  Nell'esempio seguente viene illustrato come creare un oggetto <xref:System.Windows.Data.Binding> e specificare le proprietà nel codice.  In questo esempio `TheConverter` è un oggetto che implementa l'interfaccia <xref:System.Windows.Data.IValueConverter>.  
  
 [!code-csharp[BindConversion#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#1)]
 [!code-vb[BindConversion#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#1)]  
[!code-csharp[BindConversion#end1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#end1)]
[!code-vb[BindConversion#end1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#end1)]  
  
 Se l'oggetto di cui si esegue l'associazione è <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>, è possibile chiamare il metodo `SetBinding` direttamente sull'oggetto anziché utilizzare <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=fullName>.  Per un esempio, vedere [Creare un'associazione nel codice](../../../../docs/framework/wpf/data/how-to-create-a-binding-in-code.md).  
  
<a name="Path_Syntax"></a>   
## Sintassi del percorso di associazione  
 Utilizzare la proprietà <xref:System.Windows.Data.Binding.Path%2A> per specificare il valore di origine al quale si desidera eseguire l'associazione:  
  
-   Nel caso più semplice, il valore della proprietà <xref:System.Windows.Data.Binding.Path%2A> è il nome della proprietà dell'oggetto di origine da utilizzare per l'associazione, ad esempio `Path=PropertyName`.  
  
-   Le sottoproprietà di una proprietà possono essere specificate tramite una sintassi simile a quella utilizzata in [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)].  La clausola `Path=ShoppingCart.Order`, ad esempio, imposta l'associazione sulla sottoproprietà `Order` dell'oggetto o sulla proprietà `ShoppingCart`.  
  
-   Per eseguire l'associazione a una [proprietà associata](GTMT), racchiuderla tra parentesi.  Per eseguire, ad esempio, l'associazione alla [proprietà associata](GTMT) <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>, la sintassi utilizzata sarà `Path=(DockPanel.Dock)`.  
  
-   Gli indicizzatori di una proprietà possono essere specificati all'interno di parentesi quadre dopo il nome della proprietà in cui viene applicato l'indicizzatore.  Ad esempio, con la clausola `Path=ShoppingCart[0]` viene impostata l'associazione all'indice corrispondente al modo in cui l'indicizzazione interna della proprietà gestisce la stringa letterale "0".  Sono supportati anche indicizzatori annidati.  
  
-   È possibile combinare indicizzatori e sottoproprietà all'interno di una clausola `Path`; ad esempio, `Path=ShoppingCart.ShippingInfo[MailingAddress,Street].`  
  
-   All'interno degli indicizzatori possono essere presenti più parametri dell'indicizzatore separati da virgole \(,\).  Il tipo di ogni parametro può essere specificato tra parentesi.  Nel caso di `Path="[(sys:Int32)42,(sys:Int32)24]"`, ad esempio, è stato eseguito il mapping di `sys` allo spazio dei nomi `System`.  
  
-   Quando l'origine è una visualizzazione di raccolta, l'elemento corrente può essere specificato con una barra \(\/\).  Ad esempio, la clausola `Path=/` imposta l'associazione sull'elemento corrente nella visualizzazione.  Quando l'origine è una raccolta, questa sintassi specifica l'elemento corrente della visualizzazione di raccolta predefinita.  
  
-   Le barre e i nomi delle proprietà possono essere combinati per attraversare proprietà che corrispondono a raccolte.  Ad esempio, `Path=/Offices/ManagerName` specifica l'elemento corrente della raccolta di origine contenente una proprietà `Offices` che corrisponde anche a una raccolta.  L'elemento corrente è un oggetto che contiene una proprietà `ManagerName`.  
  
-   Facoltativamente, è possibile utilizzare un percorso con il punto \(.\) per eseguire l'associazione all'origine corrente.  Ad esempio `Text="{Binding}"` è equivalente a `Text="{Binding Path=.}"`.  
  
### Meccanismo di escape  
  
-   All'interno degli indicizzatori \(\[ \]\), l'accento circonflesso \(^\) funge da escape per il carattere successivo.  
  
-   Se si imposta <xref:System.Windows.Data.Binding.Path%2A> in XAML, sarà necessario utilizzare caratteri di escape \(con entità XML\) anche per alcuni caratteri specifici della definizione del linguaggio XML:  
  
    -   Utilizzare `&` come carattere di escape per il carattere "&".  
  
    -   Utilizzare `>` come carattere di escape per il tag di fine "\>".  
  
-   Inoltre, se si descrive l'intera associazione di un attributo utilizzando la sintassi dell'estensione di markup, sarà necessario utilizzare un carattere di escape \(una barra rovesciata \\\), per i caratteri speciali del parser dell'estensione di markup [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
    -   La stessa barra rovesciata \(\\\) costituisce il carattere di escape.  
  
    -   Il segno di uguale \(\=\) separa il nome della proprietà dal valore della proprietà.  
  
    -   Le proprietà vengono separate tramite virgola \(,\).  
  
    -   La parentesi graffa di destra \(}\) rappresenta la fine di un'estensione di markup.  
  
<a name="Default"></a>   
## Comportamenti predefiniti  
 Di seguito viene indicato il comportamento predefinito nel caso in cui non sia specificato nella dichiarazione.  
  
-   Viene creato un convertitore predefinito che tenta di eseguire una conversione di tipo tra il valore dell'[origine dell'associazione](GTMT) e il valore della [destinazione dell'associazione](GTMT).  Se non è possibile eseguire una conversione, il convertitore predefinito restituisce `null`.  
  
-   Se non viene impostato <xref:System.Windows.Data.Binding.ConverterCulture%2A>, il motore di associazione utilizza la proprietà `Language` dell'oggetto di [destinazione dell'associazione](GTMT).  In XAML quest'ultimo viene impostato in modalità predefinita su "en\-US" oppure eredita il valore dall'elemento radice \(o da qualsiasi elemento\) della pagina, qualora ne sia stato impostato uno in modo esplicito.  
  
-   Se l'associazione dispone già di un contesto dati \(ad esempio, il contesto dati ereditato da un elemento padre\) e indipendentemente da quale elemento, o raccolta, restituito da quel contesto risulti adatto all'associazione senza richiedere ulteriori modifiche del percorso, una dichiarazione di associazione può essere del tutto priva di clausole: `{Binding}`. Si tratta della modalità con la quale viene spesso specificata un'associazione per l'applicazione di stili ai dati, se l'associazione agisce su una raccolta.  Per ulteriori informazioni, vedere la sezione "Oggetti interi utilizzati come origine di associazione" in [Cenni preliminari sulle origini di associazione](../../../../docs/framework/wpf/data/binding-sources-overview.md).  
  
-   L'oggetto <xref:System.Windows.Data.Binding.Mode%2A> predefinito può essere unidirezionale o bidirezionale a seconda della [proprietà di dipendenza](GTMT) di cui si esegue l'associazione.  È sempre possibile dichiarare in modo esplicito la modalità di associazione per garantire che il relativo comportamento sia quello desiderato.  In generale, le proprietà di controllo modificabili dall'utente, ad esempio <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName> e <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A?displayProperty=fullName> sono impostate in modalità predefinita su associazioni bidirezionali, mentre la maggior parte delle altre proprietà sono impostate in modalità predefinita su associazioni unidirezionali.  
  
-   Il valore predefinito di <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> può variare da <xref:System.Windows.Data.UpdateSourceTrigger> a <xref:System.Windows.Data.UpdateSourceTrigger> anche in questo caso a seconda della [proprietà di dipendenza](GTMT) associata.  Il valore predefinito per la maggior parte delle [proprietà di dipendenza](GTMT) è <xref:System.Windows.Data.UpdateSourceTrigger>, mentre la proprietà <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName> ha un valore predefinito di <xref:System.Windows.Data.UpdateSourceTrigger>.  
  
## Vedere anche  
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Sintassi XAML di PropertyPath](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md)