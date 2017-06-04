---
title: "Type Converters and Markup Extensions for XAML | Microsoft Docs"
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
  - "XAML [XAML Services], type converter services"
  - "XAML [XAML Services], value converters"
  - "XAML [XAML Services], markup extension services"
  - "value converters for XAML [XAML Services]"
  - "XAML [XAML Services], service context"
ms.assetid: db07a952-05ce-4aa4-b6f9-aac7397d0326
caps.latest.revision: 13
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# Type Converters and Markup Extensions for XAML
I convertitori di tipi e le estensioni di markup sono due tecniche usate dai sistemi di tipi XAML e writer XAML per generare componenti dell'oggetto grafico. Anche se condividono alcune caratteristiche, i convertitori di tipi e le estensioni di markup sono rappresentati in modo diverso in un flusso del nodo XAML. In questo set di documentazione, i convertitori di tipi, le estensioni di markup e costrutti simili talvolta vengono detti collettivamente convertitori di valori.  
  
<a name="value_converters"></a>   
## Convertitori di valori  
 In XAML i convertitori di valori vengono usati per vari scenari. Nell'elenco seguente vengono indicati diversi tipi di convertitori di valori in XAML:  
  
-   Convertitore di tipi  
  
-   Estensione di markup  
  
-   Serializzatore di valori  
  
-   Classe correlata o classe di supporto che fornisce la logica per una sintassi del testo XAML  
  
<a name="type_converters"></a>   
## Convertitori di tipi  
 Nella definizione di servizi XAML di .NET Framework i convertitori di tipi sono classi che derivano dalla classe <xref:System.ComponentModel.TypeConverter> CLR.<xref:System.ComponentModel.TypeConverter> è una classe che era presente [!INCLUDE[TLA#tla_netframewk](../../../includes/tlasharptla-netframewk-md.md)] prima dell'introduzione di XAML. Lo scopo originale consisteva nel supporto di finestre delle proprietà e di analoghe metafore di modifica basate sul testo per le proprietà [!INCLUDE[TLA2#tla_ide](../../../includes/tla2sharptla-ide-md.md)]. L'introduzione di XAML a .NET Framework usa <xref:System.ComponentModel.TypeConverter> per convertire una sintassi del testo, come individuata in un valore di attributo o in un nodo di valori XAML, in un oggetto. <xref:System.ComponentModel.TypeConverter> può anche essere usato per serializzare un valore oggetto alla sintassi del testo.<xref:System.ComponentModel.TypeConverter> è stato usato anche in implementazioni XAML precedenti specifiche del framework in [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] e [!INCLUDE[vsindigo](../../../includes/vsindigo-md.md)]. Per altre informazioni su <xref:System.ComponentModel.TypeConverter> in XAML, vedere [Type Converters for XAML Overview](../../../docs/framework/xaml-services/type-converters-for-xaml-overview.md).  
  
<a name="markup_extensions"></a>   
## Estensioni di markup  
 Nell'implementazione di servizi XAML di .NET Framework, le estensioni di markup sono classi che derivano dalla classe <xref:System.Windows.Markup.MarkupExtension>. Le estensioni di markup sono un concetto che in questo formato è originato dal linguaggio XAML. È possibile considerare un'estensione di markup come una sequenza di escape estensibile che chiama una classe di servizio per fornirne la logica corrispondente. In termini di markup, i processori XAML riconoscono universalmente un'estensione di markup mediante una sequenza di testo che inizia con una parentesi graffa aperta \({\) in una stringa di testo.  
  
 Le estensioni di markup sono diverse dai convertitori di tipi. I convertitori di tipi sono in genere associati a tipi o membri. Vengono richiamati quando una creazione dell'oggetto grafico o una serializzazione rileva una sintassi del testo associato a tali entità.  
  
 Le estensioni di markup sono associate a una singola classe di servizio di supporto, ma possono essere applicate per qualsiasi valore del membro. È tuttavia possibile implementare l'estensione di markup per limitarne deliberatamente l'utilizzo a determinati membri o tipi di destinazione usando il contesto del servizio. Le estensioni di markup possono eseguire l'override di un'associazione del convertitore di tipi oppure è possibile specificare un valore di attributo per i membri che altrimenti non supporterebbero una sintassi del testo.  
  
 Per altre informazioni sul modello di implementazione dell'estensione di markup per XAML, vedere [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md).  
  
> [!NOTE]
>  I tipi <xref:System.Windows.Markup.MarkupExtension> e <xref:System.Windows.Markup.ValueSerializer> sono entrambi inclusi nello spazio dei nomi <xref:System.Windows.Markup> e non in quello <xref:System.Xaml>. Ciò non implica che questi tipi sono specifici di WPF o delle tecnologie [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)] che altrimenti popolano gli spazi dei nomi CLR che contengono la stringa `Windows`.<xref:System.Windows.Markup.MarkupExtension> e <xref:System.Windows.Markup.ValueSerializer> sono inclusi nell'assembly System.Xaml e non dispongono di alcuna dipendenza dal framework specifica. Questi tipi esistevano già nello spazio dei nomi CLR per [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] e restano nello spazio dei nomi CLR in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] per evitare di interrompere i riferimenti nei progetti WPF esistenti. Per altre informazioni, vedere [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md).  
  
<a name="value_serializers"></a>   
## Serializzatori di valori  
 Un oggetto <xref:System.Windows.Markup.ValueSerializer> è un convertitore di tipi specializzato ottimizzato per la conversione di un oggetto in una stringa. È possibile che un oggetto <xref:System.Windows.Markup.ValueSerializer> per XAML non implementi affatto il metodo `ConvertFrom`. Con un'implementazione di <xref:System.Windows.Markup.ValueSerializer> si ottengono servizi in un modo simile a quello di un'implementazione di <xref:System.ComponentModel.TypeConverter>. I metodi virtuali forniscono un parametro di input `context`. Il parametro `context` è di tipo <xref:System.Windows.Markup.IValueSerializerContext>, che eredita dall'interfaccia di <xref:System.IServiceProvider> e dispone di un metodo <xref:System.IServiceProvider.GetService%2A>.  
  
 Nel sistema di tipi XAML e per le implementazioni del writer XAML che usano l'elaborazione del ciclo del nodo XAML per la serializzazione, un convertitore di valori associato a un tipo o a un membro viene segnalato dalla relativa proprietà <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=fullName>. Il significato per i writer XAML che eseguono la serializzazione è che, in presenza di <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=fullName> e <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=fullName>, il convertitore di tipi deve essere usato per il percorso di caricamento e il serializzatore di valori deve essere usato per il percorso di salvataggio. Se <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=fullName> esiste ma <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=fullName> è `null`, il convertitore di tipi viene usato anche per il percorso di salvataggio.  
  
<a name="other_value_converters"></a>   
## Altri convertitori di valori  
 Un convertitore di valori è estensibile oltre i modelli specifici di un convertitore di tipi o un'estensione di markup. Questa personalizzazione tuttavia richiede anche la ridefinizione del sistema di tipi XAML fornito dai servizi XAML di .NET Framework. Il sistema di tipi XAML esistente dispone di rappresentazioni e sistemi di report per convertitori di tipi, estensioni di markup e serializzatori di valori, ma non per moduli personalizzati di conversione dei valori. Se si intendono creare convertitori di valori personalizzati, usare il tipo <xref:System.Xaml.Schema.XamlValueConverter%601>.  
  
<a name="type_converters_and_markup_extensions_in_combination"></a>   
## Convertitori di tipi ed estensioni di markup in combinazione  
 I convertitori di tipi e le estensioni di markup vengono usati per situazioni diverse in XAML. Anche se il contesto è disponibile per gli utilizzi di estensione di markup, il comportamento della conversione di tipi di proprietà in cui un'estensione di markup fornisce un valore in genere non è selezionato nelle implementazioni dell'estensione di markup. In altre parole, anche se un'estensione di markup restituisce una stringa di testo come output di `ProvideValue`, non viene richiamato il comportamento di conversione di tipi su quella stringa così come applicato a una proprietà specifica o a un tipo di valore della proprietà. Lo scopo di un'estensione di markup in genere è quello di elaborare una stringa e restituire un oggetto senza coinvolgere alcun convertitore di tipi.  
  
<a name="service_context_for_a_value_converter"></a>   
## Contesto del servizio per un convertitore di valori  
 Quando si implementa un convertitore di valori, è spesso necessario accedere a un contesto in cui viene applicato il convertitore di valori. Questo contesto è noto come contesto del servizio. Il contesto del servizio può includere informazioni quali il contesto dello schema XAML attivo, l'accesso al sistema di mapping dei tipi fornito dal contesto dello schema XAML e dal writer di oggetti XAML e così via. Per altre informazioni sui contesti del servizio disponibili per un convertitore di valori e sulle modalità di accesso ai servizi eventualmente forniti da un contesto del servizio, vedere [Service Contexts Available to Type Converters and Markup Extensions](../../../docs/framework/xaml-services/service-contexts-available-to-type-converters-and-markup-extensions.md).  
  
## Vedere anche  
 <xref:System.Windows.Markup.MarkupExtension>   
 <xref:System.Xaml.XamlObjectWriter>   
 [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md)   
 [Type Converters for XAML Overview](../../../docs/framework/xaml-services/type-converters-for-xaml-overview.md)   
 [Service Contexts Available to Type Converters and Markup Extensions](../../../docs/framework/xaml-services/service-contexts-available-to-type-converters-and-markup-extensions.md)