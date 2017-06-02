---
title: "Collections and Collection Types for XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
caps.latest.revision: 2
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 2
---
# Collections and Collection Types for XAML
In questo argomento viene descritto come definire le proprietà dei tipi da supportare una raccolta e supportare la sintassi XAML per creare istanze di elementi della raccolta come figlio dell'elemento di un elemento o di un elemento proprietà dell'oggetto padre.  
  
## Concetti della raccolta XAML  
 Concettualmente, qualsiasi relazione in XAML in cui sono presenti più elementi figlio in un elemento oggetto XAML o dell'elemento proprietà XAML deve essere implementata come raccolta.  Tale raccolta deve essere associata a una proprietà specifica XAML di tipo XAML che è il padre nella relazione.  La proprietà deve essere una raccolta in quanto un processore XAML prevede di assegnare ogni elemento nel markup sia un elemento appena aggiunta di proprietà della raccolta della sicurezza.  
  
 A livello di linguaggio XAML, i requisiti esatti di supporto della raccolta non sono completamente definiti.  Il concetto che una raccolta può essere o un elenco o un dizionario \(ma non entrambi\) sono definiti a livello di linguaggio XAML, ma che i tipi di supporto rappresentano elenchi o dizionari non è definito dal linguaggio XAML.  
  
 Nei servizi XAML di .NET Framework, il concetto di supporto della raccolta XAML è più chiaramente definita in termini di tipi di supporto.NET Framework.  In particolare, il supporto XAML alle raccolte è basato su numerosi concetti di .NET Framework e API utilizzate per la programmazione di .NET Framework di dizionari ed elenchi in generale.  
  
1.  <xref:System.Collections.IList> l'interfaccia indica una raccolta di elenchi.  
  
2.  <xref:System.Collections.IDictionary> l'interfaccia indica una raccolta dicionary.  
  
3.  <xref:System.Array> rappresenta una matrice e i supporti di una matrice  <xref:System.Collections.IList> metodi.  
  
 In ognuno di questi concetti di raccolta, un processore XAML dei servizi XAML di.NET Framework XAML prevede di chiamare `Add` metodo su un'istanza specifica del tipo della proprietà della raccolta.  Oppure, in uno scenario di serializzazione, un processore XAML produce le istanze specifiche del XAML\-tipo per ogni elemento trovato nell'elenco, nel dizionario o nella matrice in base al concetto specifico di ogni raccolta “degli elementi„.  questi sono: <xref:System.Collections.IList.Item%2A>;  <xref:System.Collections.IDictionary.Item%2A>; esplicito  <xref:System.Array.System%23Collections%23IList%23Item%2A> per  <xref:System.Array>.  
  
## Raccolte generiche  
 Le raccolte generiche possono essere utili per .NET Framework generali che programma e possono essere utilizzati per le proprietà della raccolta XAML.  tuttavia, le interfacce generiche <xref:System.Collections.Generic.IList%601> e  <xref:System.Collections.Generic.IDictionary%602> non sono identificati dai processori XAML dei servizi XAML di.NET Framework XAML come equivalente a non generico  <xref:System.Collections.IList> o  <xref:System.Collections.IDictionary>.  Anziché implementare le interfacce, un approccio consigliato per i tipi di proprietà di raccolta generici consiste nel derivare da classi <xref:System.Collections.Generic.List%601> o  <xref:System.Collections.Generic.Dictionary%602>.  Queste classi implementano le interfacce non generiche e pertanto sono inclusi il supporto previsto a raccolte di XAML nell'implementazione di base.  
  
## raccolta di sola lettura e logica di inizializzazione  
 Nella programmazione con.NET Framework, è un modello di progettazione comune per eseguire tutte le proprietà che contiene un valore di una raccolta come raccolta di sola lettura.  Questo modello consente all'istanza che possiede la proprietà della raccolta per controllare ciò che si verifica alla raccolta.  In particolare, il modello impedisce la sostituzione accidentale di un'intera raccolta preesistente impostando la proprietà.  In questo modello, qualsiasi accesso alla raccolta da parte deve invece essere eseguita dai metodi di chiamata o dalle proprietà come supportato dal tipo di libreria e\/o interfacce di raccolta rilevanti come <xref:System.Collections.IList>.  
  
 Utilizzando questo modello implica che qualsiasi classe che espone una proprietà di raccolta di sola lettura necessario innanzitutto inizializzare la proprietà per utilizzare una raccolta vuota.  In genere l'inizializzazione viene eseguito come parte del comportamento della costruzione per la classe.  Per essere utile per XAML, è importante che tale logica viene fatto riferimento sempre dal costruttore predefinito, perché XAML chiama in genere il costruttore predefinito prima di elaborare le proprietà \(proprietà della raccolta o altrimenti\).  
  
## Supporto e raccolte di sistema di tipi XAML  
 Oltre ai meccanismi di base di analisi XAML e di compilazione o di serializzare le proprietà della raccolta, il sistema di tipi XAML implementato nei servizi XAML di .NET Framework include diverse caratteristiche del progetto che riguardano le raccolte in XAML.  
  
1.  <xref:System.Xaml.XamlType.IsCollection%2A> restituisce true se il tipo XAML è momento da un tipo che fornisce XAML supporto della raccolta.  
  
2.  <xref:System.Xaml.XamlType.IsDictionary%2A> e  <xref:System.Xaml.XamlType.IsArray%2A> può inoltre identificare la modalità di raccolta il tipo XAML supporta.  Per i processori personalizzati XAML basati sui servizi XAML di.NET Framework e sul sistema di tipi XAML ma non sono basati sull'esistenza <xref:System.Xaml.XamlWriter> le implementazioni, conoscenti le modalità di raccolta viene utilizzata potrebbero essere necessarie per individuare il metodo per richiamare per l'elaborazione di raccolta.  
  
3.  Ognuno dei valori della proprietà precedenti potenzialmente viene influenzato da un override di <xref:System.Xaml.XamlType.LookupCollectionKind%2A> in un tipo XAML.