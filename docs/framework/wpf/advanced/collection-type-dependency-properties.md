---
title: "Propriet&#224; di dipendenza di tipo raccolta | Microsoft Docs"
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
  - "proprietà del tipo di raccolta"
  - "proprietà di dipendenza"
  - "proprietà, tipo di raccolta"
  - "proprietà, dipendenza"
ms.assetid: 99f96a42-3ab7-4f64-a16b-2e10d654e97c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Propriet&#224; di dipendenza di tipo raccolta
In questo argomento vengono fornite linee guida e suggeriti modelli per l'implementazione di una [proprietà di dipendenza](GTMT) in cui la proprietà è di tipo raccolta.  
  
   
  
<a name="implementing"></a>   
## Implementazione di una proprietà di dipendenza di tipo raccolta  
 Per una proprietà di dipendenza generica, il modello di implementazione seguito consiste nel definire un wrapper della proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], nel quale quella proprietà è supportata da un identificatore <xref:System.Windows.DependencyProperty>, anziché da un campo o da un altro costrutto.  Questo stesso modello viene seguito quando si implementa una proprietà di tipo raccolta.  Tuttavia, una proprietà di tipo raccolta aggiunge alcuni aspetti più complessi al modello, se il tipo contenuto all'interno della raccolta è esso stesso un oggetto <xref:System.Windows.DependencyObject> o una classe derivata <xref:System.Windows.Freezable>.  
  
<a name="initializing"></a>   
## Inizializzazione della raccolta oltre il valore predefinito  
 Quando si crea una proprietà di dipendenza, non si specifica il valore predefinito della proprietà come valore iniziale del campo.  Al contrario, viene specificato il valore predefinito tramite i metadati della proprietà di dipendenza.  Se la proprietà è un tipo di riferimento, il valore predefinito specificato nei metadati della proprietà di dipendenza non è un valore predefinito per istanza, bensì un valore predefinito che viene applicato a tutte le istanze del tipo.  Pertanto, è necessario prestare attenzione a non utilizzare la singola raccolta statica definita dai metadati della proprietà della raccolta come valore di lavoro predefinito per le istanze del tipo appena create.  È necessario assicurarsi invece di impostare deliberatamente il valore della raccolta su un'unica raccolta \(istanza\), come parte della logica del costruttore di classi.  In caso contrario, sarà stata creata una classe Singleton non intenzionale.  
  
 Prendere in considerazione l'esempio riportato di seguito.  Nella sezione seguente dell'esempio viene descritta la definizione di una classe `Aquarium`.  La classe definisce la proprietà di dipendenza di tipo raccolta `AquariumObjects` che utilizza il tipo <xref:System.Collections.Generic.List%601> generico con un vincolo di tipo <xref:System.Windows.FrameworkElement>.  Nella chiamata <xref:System.Windows.DependencyProperty.Register%28System.String%2CSystem.Type%2CSystem.Type%2CSystem.Windows.PropertyMetadata%29> per la proprietà di dipendenza, i metadati stabiliscono che il valore predefinito sia un nuovo oggetto <xref:System.Collections.Generic.List%601> generico.  
  
 <!-- TODO: review snippet reference [!code-csharp[PropertiesOvwSupport#CollectionProblemDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemdefinition)]  -->
 [!code-vb[PropertiesOvwSupport#CollectionProblemDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemdefinition)]  
[!code-csharp[PropertiesOvwSupport#CollectionProblemEndB](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemendb)]
[!code-vb[PropertiesOvwSupport#CollectionProblemEndB](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemendb)]  
  
 Tuttavia, se si lascia inalterato il codice, quel singolo valore predefinito dell'elenco viene condiviso per tutte le istanze di `Aquarium`.  Se si esegue il codice di test riportato di seguito, destinato a mostrare la modalità di creazione di due istanze di `Aquarium` separate e si aggiunge un singolo oggetto `Fish` diverso a ciascuna di esse, il risultato è sorprendente.  
  
 [!code-csharp[PropertiesOvwSupport#CollectionProblemTestCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemtestcode)]
 [!code-vb[PropertiesOvwSupport#CollectionProblemTestCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemtestcode)]  
  
 Invece di contenere un solo elemento, ogni raccolta ne contiene due.  Questa situazione si verifica in quanto ciascun oggetto `Aquarium` ha aggiunto il proprio oggetto `Fish` alla raccolta dei valori predefiniti, generata da una singola chiamata al costruttore nei metadati e pertanto condivisa tra tutte le istanze.  Si tratta di una situazione non auspicata.  
  
 Per risolvere questo problema, è necessario reimpostare il valore della proprietà di dipendenza della raccolta su un'unica istanza, come parte della chiamata al costruttore di classi.  Dal momento che la proprietà è una proprietà di dipendenza di sola lettura, per impostarla viene utilizzato il metodo <xref:System.Windows.DependencyObject.SetValue%28System.Windows.DependencyPropertyKey%2CSystem.Object%29>, mediante l'oggetto <xref:System.Windows.DependencyPropertyKey>, al quale è possibile accedere solo all'interno della classe.  
  
 [!code-csharp[PropertiesOvwSupport#CollectionProblemCtor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#collectionproblemctor)]
 [!code-vb[PropertiesOvwSupport#CollectionProblemCtor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#collectionproblemctor)]  
  
 A questo punto, se si esegue nuovamente questo stesso codice di test, è possibile ottenere i risultati previsti, in cui ciascun oggetto `Aquarium` supporta la propria raccolta univoca.  
  
 Se si sceglie una proprietà della raccolta con possibilità di accesso in lettura\/scrittura, questo modello presenta una piccola variazione.  In tal caso, è possibile chiamare la funzione di accesso set pubblica del costruttore per eseguire l'inizializzazione, che esegue la chiamata della firma non chiave di <xref:System.Windows.DependencyObject.SetValue%28System.Windows.DependencyProperty%2CSystem.Object%29> all'interno del wrapper impostato, utilizzando un identificatore <xref:System.Windows.DependencyProperty> pubblico.  
  
## Creazione di report relativi alle modifiche dei valori di associazione nelle proprietà della raccolta  
 Una proprietà della raccolta che costituisce essa stessa una proprietà di dipendenza non crea automaticamente dei report delle modifiche per le relative sottoproprietà.  La creazione di associazioni all'interno di una raccolta può impedire all'associazione di creare report delle modifiche, invalidando in tal modo alcuni scenari di associazione dati.  Tuttavia, se si utilizza <xref:System.Windows.FreezableCollection%601> come tipo di raccolta, i report delle modifiche della sottoproprietà apportate agli elementi contenuti nella raccolta vengono creati correttamente e l'associazione funziona nel modo previsto.  
  
 Per abilitare l'associazione di sottoproprietà in una raccolta di oggetti di dipendenza, creare la proprietà della raccolta come tipo <xref:System.Windows.FreezableCollection%601>, con un vincolo di tipo per quella raccolta per qualsiasi classe derivata <xref:System.Windows.DependencyObject>.  
  
## Vedere anche  
 <xref:System.Windows.FreezableCollection%601>   
 [Classi XAML e personalizzate per WPF](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)