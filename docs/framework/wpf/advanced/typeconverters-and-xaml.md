---
title: "TypeConverter e XAML | Microsoft Docs"
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
  - "classi, TypeConverter"
  - "TypeConverter (classe)"
  - "XAML, TypeConverter (classe)"
ms.assetid: f6313e4d-e89d-497d-ac87-b43511a1ae4b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# TypeConverter e XAML
In questo argomento viene presentato lo scopo della conversione del tipo da stringa come funzionalità generale del linguaggio XAML.  In .NET Framework, la classe <xref:System.ComponentModel.TypeConverter> svolge un ruolo particolare come parte dell'implementazione per una classe personalizzata gestita che può essere utilizzata come valore della proprietà nell'utilizzo degli attributi XAML.  Se si scrive una classe personalizzata e si desidera che le istanze della classe siano utilizzabili come valori di attributi XAML che è possibile impostare, potrebbe essere necessario applicare un oggetto <xref:System.ComponentModel.TypeConverterAttribute> alla classe, scrivere una classe <xref:System.ComponentModel.TypeConverter> personalizzata o eseguire entrambe le operazioni.  
  
   
  
## Concetti relativi alla conversione di tipi  
  
### Valori XAML e di stringa  
 Quando si imposta un valore dell'attributo in un file XAML, il tipo iniziale di tale valore è una stringa in solo testo.  Anche altre primitive, ad esempio <xref:System.Double>, sono inizialmente stringhe di testo per un processore XAML.  
  
 Un processore XAML deve disporre di due informazioni per elaborare un valore di attributo.  La prima informazione è il tipo di valore della proprietà che si imposta.  Qualsiasi stringa che definisce un valore di attributo e che viene elaborata in XAML deve essere convertita o risolta in un valore di quel tipo.  Se il valore è una primitiva riconosciuta dal parser XAML \(ad esempio un valore numerico\), viene eseguito un tentativo di conversione diretta della stringa.  Se il valore è costituito da un'enumerazione, la stringa viene utilizzata per verificare se un nome corrisponde a una costante denominata in tale enumerazione.  Se il valore non è rappresentato né da una primitiva riconosciuta dal parser né da un'enumerazione, il tipo in questione deve essere in grado di fornire un'istanza del tipo o un valore basato su una stringa convertita.  A questo scopo, è necessario indicare una classe del convertitore di tipi.  Il convertitore di tipi è una classe di supporto che fornisce i valori di un'altra classe, tanto negli scenari XAML quanto, eventualmente, per le chiamate al codice nel codice .NET.  
  
### Utilizzo del comportamento di conversione del tipo esistente in XAML  
 In base alla familiarità acquisita con i concetti XAML sottostanti. è possibile che si utilizzi già il comportamento di conversione dei tipi nel codice XAML dell'applicazione di base senza averne la consapevolezza.  Ad esempio, in WPF vengono definite centinaia di proprietà che accettano un valore del tipo <xref:System.Windows.Point>.  <xref:System.Windows.Point> è un valore che descrive una coordinata in uno spazio delle coordinate bidimensionale e che dispone di due sole proprietà realmente rilevanti: <xref:System.Windows.Point.X%2A> e <xref:System.Windows.Point.Y%2A>.  In XAML, un tipo Point viene specificato come stringa con un delimitatore \(in genere, una virgola\) tra il valore <xref:System.Windows.Point.X%2A> e il valore <xref:System.Windows.Point.Y%2A>.  Ad esempio: `<LinearGradientBrush StartPoint="0,0" EndPoint="1,1">`.  
  
 Anche questo tipo semplice di <xref:System.Windows.Point> e il relativo utilizzo di base in XAML implicano un convertitore di tipi.  In questo caso, la classe <xref:System.Windows.PointConverter>.  
  
 Il convertitore di tipi per <xref:System.Windows.Point> definito a livello di classe semplifica gli utilizzi del markup di tutte le proprietà che accettano <xref:System.Windows.Point>.  Nell'esempio precedentemente illustrato, senza un convertitore di tipi sarebbe necessario ricorrere a markup molto più dettagliato:  
  
 `<LinearGradientBrush>`  
  
 `<LinearGradientBrush.StartPoint>`  
  
 `<Point X="0" Y="0"/>`  
  
 `</LinearGradientBrush.StartPoint>`  
  
 `<LinearGradientBrush.EndPoint>`  
  
 `<Point X="1" Y="1"/>`  
  
 `</LinearGradientBrush.EndPoint>`  
  
 `<LinearGradientBrush>`  
  
 La scelta tra l'utilizzo di una stringa di conversione del tipo o quello di una sintassi equivalente più dettagliata è, in genere, una questione di stile di codifica.  Anche il flusso di lavoro degli strumenti XAML può influire sul modo di impostare i valori.  Alcuni strumenti XAML tendono a generare la forma più dettagliata del markup perché è più facile eseguirne il round trip nelle visualizzazioni delle finestre di progettazione o nel meccanismo di serializzazione.  
  
 In genere, è possibile individuare i convertitori di tipi esistenti nei tipi WPF e .NET Framework verificando l'applicazione di <xref:System.ComponentModel.TypeConverterAttribute> in una classe o in una proprietà.  Questo attributo denominerà la classe che costituisce il convertitore di tipi di supporto per i valori del tipo in questione, sia per gli scenari XAML sia, eventualmente, per altri scopi.  
  
### Convertitori di tipi ed estensioni di markup  
 Le estensioni di markup e i convertitori di tipi riempiono ruoli ortogonali in termini di comportamento del processore XAML e di scenari ai quali sono applicati.  Sebbene il contesto sia disponibile per gli utilizzi di estensioni di markup, il comportamento di conversione dei tipi di proprietà in cui un'estensione di markup fornisce un valore non viene in genere controllato nelle implementazioni dell'estensione di markup.  In altre parole, anche se un'estensione di markup restituisce una stringa di testo come output di `ProvideValue`, il comportamento di conversione dei tipi su quella stringa così come applicato a una proprietà specifica o a un tipo di valore della proprietà non viene richiamato. In genere, lo scopo di un'estensione di markup consiste nell'elaborare una stringa e restituire un oggetto senza coinvolgere alcun convertitore di tipi.  
  
 Una situazione comune che richiede un'estensione di markup piuttosto che un convertitore di tipi è la creazione di un riferimento a un oggetto già esistente.  Nella migliore delle ipotesi, un convertitore di tipi senza stato potrebbe solo generare una nuova istanza, che non necessariamente è appropriata.  Per ulteriori informazioni sulle estensioni di markup, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
### Convertitori di tipi nativi  
 Nell'implementazione WPF e .NET Framework del parser XAML esistono determinati tipi che dispongono di una gestione nativa della conversione del tipo, ma non di tipi considerabili, propriamente, primitivi.  Un esempio dei tipi in questione è <xref:System.DateTime>.  Il motivo consiste nel funzionamento dell'architettura di .NET Framework: il tipo <xref:System.DateTime> è definito in mscorlib, la libreria più elementare di .NET.  Poiché non è consentito assegnare a <xref:System.DateTime> un attributo fornito da un altro assembly che introduce una dipendenza \(<xref:System.ComponentModel.TypeConverterAttribute> è fornito da System\), il consueto meccanismo di individuazione del convertitore di tipi mediante assegnazione di attributi non può essere supportato.  Il parser XAML dispone invece di un elenco di tipi che necessitano di elaborazione nativa e li elabora secondo modalità analoghe all'elaborazione delle primitive effettive.  Nel caso di <xref:System.DateTime> ciò comporta una chiamata a <xref:System.DateTime.Parse%2A>.  
  
<a name="Implementing_a_Type_Converter"></a>   
## Implementazione di un convertitore di tipi  
  
### TypeConverter  
 Nel precedente esempio di <xref:System.Windows.Point> si è fatto cenno alla classe <xref:System.Windows.PointConverter>.  Per le implementazioni .NET di XAML, tutti i convertitori di tipi utilizzati per XAML sono classi derivanti dalla classe di base <xref:System.ComponentModel.TypeConverter>.  La classe <xref:System.ComponentModel.TypeConverter> era presente nelle versioni di .NET precedenti all'introduzione di XAML e in origine veniva tra l'altro utilizzata per fornire la conversione delle stringhe per le finestre di proprietà nelle finestre di progettazione visiva.  In XAML, il ruolo di <xref:System.ComponentModel.TypeConverter> risulta ampliato, andando a includere quello di classe di base per le conversioni da e a stringa che consentono l'analisi di un valore dell'attributo della stringa, nonché l'eventuale riconversione di un valore in fase di esecuzione di una particolare proprietà oggetto in una stringa per la serializzazione come attributo.  
  
 <xref:System.ComponentModel.TypeConverter> definisce quattro membri che sono rilevanti per la conversione da e in stringhe al fine di elaborare la sintassi XAML:  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 Tra questi, il metodo più importante è <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>.  Questo metodo converte la stringa di input nel tipo di oggetto richiesto.  In termini generali, sarebbe possibile implementare il metodo <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> per convertire una più vasta gamma di tipi nel tipo di destinazione previsto dal convertitore, assolvendo pertanto scopi che si estendono oltre quelli definiti per XAML, quale il supporto delle conversioni in fase di esecuzione. Tuttavia, per quanto riguarda XAML, l'unico elemento rilevante è il percorso del codice che consente di elaborare un input <xref:System.String>.  
  
 Il secondo metodo in ordine di importanza è <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>.  Se un'applicazione viene convertita in una rappresentazione del markup \(quando ad esempio viene salvata in XAML come file\), <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> sarà responsabile della creazione di una rappresentazione del markup.  In tal caso, il percorso del codice rilevante per XAML è costituito dal passaggio di `destinationType` di <xref:System.String>.  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> e <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> sono metodi di supporto utilizzati quando un servizio esegue una query sulle funzionalità dell'implementazione di <xref:System.ComponentModel.TypeConverter>.  È necessario implementare questi metodi per restituire `true` per i casi specifici del tipo supportati dai metodi di conversione equivalenti del convertitore.  Per XAML, si tratta in genere del tipo <xref:System.String>.  
  
### Informazioni relative alle impostazioni cultura e convertitori di tipi per XAML  
 Ogni implementazione di <xref:System.ComponentModel.TypeConverter> può avere un'interpretazione diversa della validità di una stringa per una conversione e può quindi utilizzare o ignorare la descrizione del tipo passata come parametri.  È opportuna una considerazione per quanto riguarda le impostazioni cultura e la conversione di tipi in XAML.  L'utilizzo di stringhe localizzabili come valori di attributo è supportato in XAML.  Tuttavia, l'utilizzo di una stringa localizzabile come input del convertitore di tipi con requisiti delle impostazioni cultura specifici non è supportato, perché i convertitori di tipi per i valori di attributo XAML implicano un comportamento di analisi basato su un'unica lingua e sulle impostazioni cultura `en-US`.  Per ulteriori informazioni sui motivi legati alla progettazione di tale limitazione, consultare la specifica del linguaggio XAML \([\[MS\-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525)\).  
  
 Un esempio delle problematiche che possono verificarsi con le impostazioni cultura è rappresentato dal separatore decimale per i numeri, che per alcune impostazioni cultura è la virgola.  Tale caratteristica è in conflitto con il comportamento di molti convertitori di tipi XAML di WPF, che prevede l'utilizzo della virgola come delimitatore \(basato su precedenti storici quali il formato X,Y comune o gli elenchi delimitati da virgole\).  Persino il passaggio di impostazioni cultura nel codice XAML adiacente \(impostando ad esempio `Language` o `xml:lang` sulle impostazioni cultura `sl-SI`, per le quali viene utilizzata la virgola come separatore decimale\) non consente di risolvere il problema.  
  
### Implementazione di ConvertFrom  
 Per essere utilizzabile come implementazione di <xref:System.ComponentModel.TypeConverter> che supporti XAML, il metodo <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> per tale convertitore deve accettare una stringa come parametro `value`.  Se la stringa ha un formato valido e può essere convertita dall'implementazione di <xref:System.ComponentModel.TypeConverter>, l'oggetto restituito deve supportare il casting nel tipo previsto dalla proprietà.  In caso contrario, l'implementazione <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> deve restituire `null`.  
  
 Ciascuna implementazione di <xref:System.ComponentModel.TypeConverter> può avere un'interpretazione diversa della validità di una stringa per una conversione e può quindi utilizzare o ignorare i contesti di descrizione del tipo o di impostazione cultura passati come parametri.  Tuttavia, l'elaborazione della sintassi XAML di WPF potrebbe non passare i valori al contesto della descrizione del tipo in tutti i casi e potrebbe perfino non passare le impostazioni cultura basate su `xml:lang`.  
  
> [!NOTE]
>  Non utilizzare i caratteri parentesi graffa, in particolare {, come elemento del formato stringa.  Questi caratteri vengono utilizzati esclusivamente come punti di ingresso e di uscita di una sequenza di estensione del markup.  
  
### Implementazione di ConvertTo  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> viene potenzialmente utilizzato per il supporto della serializzazione.  Il supporto della serializzazione tramite <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> per il tipo personalizzato e il relativo convertitore di tipi non è un requisito assoluto.  Tuttavia, se si implementa un controllo o si utilizza la serializzazione come parte delle funzionalità o della progettazione della classe, sarà necessario implementare <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>.  
  
 Per essere utilizzabile come implementazione di <xref:System.ComponentModel.TypeConverter> che supporti XAML, il metodo <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> per tale convertitore deve accettare il supporto di un'istanza del tipo \(o un valore\) come parametro `value`.  Quando il parametro `destinationType` è il tipo <xref:System.String>, deve essere possibile eseguire il casting dell'oggetto restituito come <xref:System.String>.  La stringa restituita deve rappresentare un valore serializzato di `value`.  In teoria, il formato di serializzazione scelto deve essere in grado di generare lo stesso valore se quella stringa fosse passata all'implementazione di <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> dello stesso convertitore, senza perdite significative di informazioni.  
  
 Se il valore non può essere serializzato o il convertitore non supporta la serializzazione, l'implementazione di <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> deve restituire `null` e in questo caso sarà possibile generare un'eccezione.  Tuttavia, se si generano eccezioni sarà necessario segnalare l'impossibilità di utilizzare tale conversione nell'implementazione di <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> in modo da supportare un controllo preventivo con <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>, che rappresenta la procedura consigliata per evitare eccezioni.  
  
 Se il parametro `destinationType` non è di tipo <xref:System.String>, è possibile scegliere la gestione del convertitore.  In genere, viene ripristinata la gestione dell'implementazione di base, che nella forma più elementare di <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> genera un'eccezione specifica.  
  
### Implementazione di CanConvertTo  
 L'implementazione di <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> deve restituire `true` per un oggetto `destinationType` di tipo <xref:System.String>; in caso contrario, deve rinviare all'implementazione di base.  
  
### Implementazione di CanConvertFrom  
 L'implementazione di <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> deve restituire `true` per un oggetto `sourceType` di tipo <xref:System.String>; in caso contrario, deve rinviare all'implementazione di base.  
  
<a name="Applying_the_TypeConverterAttribute"></a>   
## Applicazione di TypeConverterAttribute  
 Affinché il convertitore di tipi personalizzato sia utilizzato come convertitore di tipi operativo per una classe personalizzata da un processore XAML, è necessario applicare l'oggetto [!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)]<xref:System.ComponentModel.TypeConverterAttribute> alla definizione della classe.  L'oggetto <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> specificato tramite l'attributo deve corrispondere al nome di tipo del convertitore dei tipi personalizzato.  Avendo applicato questo attributo, quando un processore XAML gestisce valori per i quali il tipo di proprietà utilizza il tipo di classe personalizzato, può immettere le stringhe e restituire le istanze dell'oggetto.  
  
 È anche possibile fornire un convertitore dei tipi per le singole proprietà.  Anziché applicare un [!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute> alla definizione della classe, applicarlo a una definizione della proprietà \(la definizione principale, non le implementazioni di `get`\/`set` all'interno di essa\).  Il tipo della proprietà deve corrispondere al tipo elaborato dal convertitore dei tipi personalizzato.  Se questo attributo viene applicato, quando un processore XAML gestisce i valori di quella proprietà, può elaborare stringhe di input e restituire istanze di oggetti.  La tecnica del convertitore dei tipi per singole proprietà risulta particolarmente utile se si sceglie di utilizzare un tipo di proprietà dall'[!INCLUDE[TLA#tla_netframewk](../../../../includes/tlasharptla-netframewk-md.md)] o da qualche altra libreria in cui non è possibile controllare la definizione della classe né applicare un oggetto <xref:System.ComponentModel.TypeConverterAttribute>.  
  
## Vedere anche  
 <xref:System.ComponentModel.TypeConverter>   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)