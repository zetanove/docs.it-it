---
title: "Defining Custom Types for Use with .NET Framework XAML Services | Microsoft Docs"
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
  - "defining custom types [XAML Services]"
ms.assetid: c2667cbd-2f46-4a7f-9dfc-53696e35e8e4
caps.latest.revision: 11
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 11
---
# Defining Custom Types for Use with .NET Framework XAML Services
Quando si definiscono tipi personalizzati che sono oggetti business o tipi privi di qualsiasi dipendenza da framework specifici, è possibile seguire alcune procedure consigliate per XAML.  Seguendo queste procedure, i servizi XAML di .NET Framework e i relativi reader e writer XAML possono individuare le caratteristiche XAML del tipo e rappresentarlo in maniera adeguata in un flusso del nodo XAML tramite il sistema di tipi XAML.  In questo argomento vengono descritte le procedure consigliate per le definizioni di tipi, le definizioni di membri e l'assegnazione di attributi CLR a tipi o membri.  
  
## Modelli di costruttore e definizioni di tipi per XAML  
 Affinché sia possibile crearne un'istanza come elemento oggetto in XAML, una classe personalizzata deve soddisfare i seguenti requisiti:  
  
-   La classe personalizzata deve essere pubblica e deve esporre un costruttore pubblico predefinito \(senza parametri\).  Per le note riguardanti le strutture, vedere la sezione seguente.  
  
-   La classe personalizzata non deve essere una classe annidata.  Il "punto" aggiuntivo nel percorso completo rende ambigua la divisione tra classe e spazio dei nomi e interferisce con altre funzionalità XAML, ad esempio le proprietà associate.  
  
 Se è possibile creare un'istanza di un oggetto come elemento oggetto, l'oggetto creato può inserire la forma di elemento proprietà di qualsiasi proprietà che accetta l'oggetto come tipo sottostante.  
  
 Se si abilita un convertitore di valori, è comunque possibile fornire valori di oggetti per i tipi che non soddisfano questi criteri.  Per ulteriori informazioni, vedere [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md).  
  
### Strutture  
 In base alla definizione CLR, le strutture possono sempre essere costruite in XAML.  Questo perché un compilatore CLR crea in modo implicito un costruttore predefinito per una struttura.  Il costruttore inizializza tutti i valori delle proprietà nei rispettivi valori predefiniti.  
  
 In alcuni casi, il comportamento di costruzione predefinito per una struttura non è appropriato.  Ciò può dipendere dal fatto che la struttura serve a inserire valori e concettualmente funziona come un'unione.  In quanto unione, i valori contenuti possono avere interpretazioni che si escludono a vicenda, pertanto nessuna delle proprietà è impostabile.  Un esempio di struttura di questo tipo nel vocabolario WPF è <xref:System.Windows.GridLength>.  Tali strutture devono implementare un convertitore di tipi, in modo che sia possibile esprimere i valori sotto forma di attributo utilizzando convenzioni di stringa che creano le diverse interpretazioni o modalità dei valori della struttura.  La struttura deve inoltre esporre un comportamento simile per la costruzione del codice tramite un costruttore non predefinito.  
  
### Interfacce  
 Le interfacce possono essere utilizzate come tipi sottostanti dei membri.  Il sistema di tipi XAML controlla l'elenco assegnabile e suppone che l'oggetto specificato come valore possa essere assegnato all'interfaccia.  Il concetto relativo alla modalità di presentazione dell'interfaccia come tipo XAML non è applicato, purché il tipo assegnabile pertinente supporti i requisiti di costruzione XAML.  
  
### Metodi factory  
 I metodi factory sono una funzionalità di XAML 2009.  Costituiscono una modifica del principio XAML secondo cui gli oggetti devono avere costruttori predefiniti.  I metodi factory non sono documentati in questo argomento.  Vedere [x:FactoryMethod Directive](../../../docs/framework/xaml-services/x-factorymethod-directive.md).  
  
## Enumerazioni  
 Le enumerazioni presentano il comportamento di conversione dei tipi nativi XAML.  I nomi delle costanti di enumerazione specificati in XAML vengono risolti a fronte del tipo di enumerazione sottostante e restituiscono il valore di enumerazione a un writer di oggetti XAML.  
  
 XAML supporta un utilizzo dello stile flag per le enumerazioni alle quali viene applicato <xref:System.FlagsAttribute>.  Per ulteriori informazioni, vedere [Descrizione dettagliata della sintassi XAML](../../../ocs/framework/wpf/advanced/xaml-syntax-in-detail.md).  L'argomento [Descrizione dettagliata della sintassi XAML](../../../ocs/framework/wpf/advanced/xaml-syntax-in-detail.md) è destinato agli utenti di WPF, tuttavia la maggior parte delle informazioni in esso contenute riguardano codice XAML non specifico di un particolare framework di implementazione.  
  
## Definizioni di membri  
 I tipi possono definire membri per l'utilizzo in XAML.  Grazie all'ereditarietà CLR, è possibile che un tipo definisca un membro utilizzabile in XAML anche se il tipo in questione  non è utilizzabile in XAML.  Se un tipo che eredita il membro supporta l'utilizzo in XAML come tipo e il membro supporta l'utilizzo in XAML per il tipo sottostante o dispone di una sintassi XAML nativa, tale membro è utilizzabile in XAML.  
  
### Proprietà  
 Se si definiscono proprietà come una proprietà CLR pubblica, utilizzando modelli delle funzioni di accesso `get` e `set` CLR tipiche e parole chiave appropriate per il linguaggio, il sistema di tipi XAML può segnalare la proprietà come membro con informazioni appropriate specificate per le proprietà di <xref:System.Xaml.XamlMember>, quali <xref:System.Xaml.XamlMember.IsReadPublic%2A> e <xref:System.Xaml.XamlMember.IsWritePublic%2A>.  
  
 Le proprietà specifiche possono abilitare una sintassi del testo applicando <xref:System.ComponentModel.TypeConverterAttribute>.  Per ulteriori informazioni, vedere [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md).  
  
 In assenza di una sintassi del testo o di una conversione XAML nativa e in assenza di un ulteriore riferimento indiretto, ad esempio un utilizzo dell'estensione di markup, il tipo di una proprietà \(<xref:System.Xaml.XamlMember.TargetType%2A> nel sistema di tipi XAML\) deve essere in grado di restituire un'istanza a un writer di oggetti XAML considerando il tipo di destinazione come un tipo CLR.  
  
 In caso di utilizzo di XAML 2009, è possibile utilizzare [x:Reference Markup Extension](../../../docs/framework/xaml-services/x-reference-markup-extension.md) per fornire valori qualora le considerazioni precedenti non vengano soddisfatte, ma è più una questione di utilizzo che non una questione di definizione di tipi.  
  
### Eventi  
 Se si definiscono eventi come evento CLR pubblico, il sistema di tipi XAML può segnalare l'evento come membro con la proprietà <xref:System.Xaml.XamlMember.IsEvent%2A> impostata su `true`.  Il collegamento dei gestori eventi non rientra nell'ambito delle funzionalità dei servizi XAML di .NET Framework, bensì viene lasciato a implementazioni e framework specifici.  
  
### Metodi  
 Il codice inline per i metodi non è una funzionalità di XAML predefinita.  Nella maggior parte dei casi non si fa riferimento ai membri del metodo direttamente da XAML e il ruolo dei metodi in XAML consiste unicamente nel fornire supporto per modelli XAML specifici.  [x:FactoryMethod Directive](../../../docs/framework/xaml-services/x-factorymethod-directive.md) è un'eccezione.  
  
### Campi  
 Le linee guida di progettazione di CLR sconsigliano i campi non statici.  Quanto ai campi statici, è possibile accedere ai valori di tali campi solo tramite [x:Static Markup Extension](../../../docs/framework/xaml-services/x-static-markup-extension.md); in questo caso non si fa nulla di particolare nella definizione CLR per esporre un campo per gli utilizzi di [x:Static](../../../docs/framework/xaml-services/x-static-markup-extension.md).  
  
## Membri associabili  
 I membri associabili vengono esposti in XAML tramite un modello di metodo della funzione di accesso in un tipo di definizione.  Non è necessario che il tipo di definizione in questione sia utilizzabile in XAML come oggetto.  Infatti, un modello comune è quello di dichiarare una classe di servizio il cui ruolo consiste nel possedere il membro associabile e implementarne i relativi comportamenti, ma non ha altre funzioni, ad esempio una rappresentazione dell'interfaccia utente.  Nelle sezioni che seguono, il segnaposto *PropertyName* rappresenta il nome del membro associabile.  Il nome deve essere valido nella [Grammatica XamlName](../../../docs/framework/xaml-services/xamlname-grammar.md).  
  
 Prestare attenzione ai conflitti di nome tra questi modelli e altri metodi di un tipo.  Se esiste un membro corrispondente a uno dei modelli, questo può essere interpretato da un processore XAML come percorso di utilizzo del membro associabile, sebbene in realtà non sia inteso come tale.  
  
#### Funzione di accesso GetPropertyName  
 La firma per la funzione di accesso `Get`*NomeProprietà* è la seguente:  
  
 `public static object Get` *PropertyName* `(object`  `target` `)`  
  
-   L'oggetto `target` può essere specificato nell'implementazione come tipo più specifico.  È possibile utilizzarlo per definire l'ambito di utilizzo del membro associabile; gli utilizzi che non rientrano nell'ambito desiderato generano eccezioni di cast non valido, successivamente segnalate da un errore di analisi XAML.  Il nome del parametro `target` non è un requisito, ma viene utilizzato per convenzione nella maggior parte delle implementazioni.  
  
-   Il valore restituito può essere specificato come tipo più specifico nell'implementazione.  
  
 Per supportare una sintassi del testo abilitata da <xref:System.ComponentModel.TypeConverter> per l'utilizzo degli attributi del membro associabile, applicare <xref:System.ComponentModel.TypeConverterAttribute> alla funzione di accesso `Get`*NomeProprietà*.  L'applicazione a `get` anziché a `set` può sembrare non intuitiva; tuttavia, questa convenzione può supportare il concetto di membri associabili di sola lettura serializzabili, utile negli scenari della finestra di progettazione.  
  
#### Funzione di accesso SetPropertyName  
 La firma richiesta per la funzione di accesso Set*NomeProprietà* è la seguente:  
  
 `public static void Set` *PropertyName* `(object`  `target` `, object`  `value` `)`  
  
-   L'oggetto `target` può essere specificato nell'implementazione come tipo più specifico, con la stessa logica e le stesse conseguenze descritte nella sezione precedente.  
  
-   L'oggetto `value` può essere specificato nell'implementazione come tipo più specifico.  
  
 Si tenga presente che il valore per questo metodo è l'input proveniente dall'utilizzo in XAML, in genere in forma di attributo.  La forma di attributo deve prevedere un supporto del convertitore di valori per una sintassi del testo; gli attributi si assegnano nella funzione di accesso `Get`*NomeProprietà*.  
  
### Archivi dei membri associabili  
 I metodi della funzione di accesso non sono in genere sufficienti a fornire un mezzo per inserire i valori dei membri associabili in un oggetto grafico o recuperare i valori dall'oggetto grafico e serializzarli nel modo appropriato.  Per fornire questa funzionalità, gli oggetti `target` nelle firme della funzione di accesso precedente devono essere in grado di archiviare valori.  Il meccanismo di archiviazione deve essere coerente con il principio del membro associabile secondo cui il membro è associabile a destinazioni in cui il membro associabile non è presente nell'elenco dei membri.  I servizi XAML di .NET Framework forniscono una tecnica di implementazione per gli archivi dei membri associabili tramite le API <xref:System.Xaml.IAttachedPropertyStore> e <xref:System.Xaml.AttachablePropertyServices>.  <xref:System.Xaml.IAttachedPropertyStore> è utilizzato dai writer XAML per scoprire l'implementazione dell'archivio e deve essere implementato sul tipo `target` delle funzioni di accesso.  Le API <xref:System.Xaml.AttachablePropertyServices> statiche sono utilizzate all'interno del corpo delle funzioni di accesso e fanno riferimento al membro associabile tramite il relativo <xref:System.Xaml.AttachableMemberIdentifier>.  
  
## Attributi CLR correlati a XAML  
 La corretta assegnazione di attributi a tipi, membri e assembly è importante ai fini della segnalazione delle informazioni sul sistema di tipi XAML ai servizi XAML di .NET Framework.  Questa funzionalità è pertinente se si intende utilizzare i tipi con sistemi XAML basati direttamente sui reader e i writer XAML dei servizi XAML di .NET Framework oppure se si definisce o si utilizza un framework che utilizza XAML basato su tali reader e writer XAML.  
  
 Per un elenco degli attributi correlati a XAML pertinenti al supporto XAML dei tipi personalizzati, vedere [XAML\-Related CLR Attributes for Custom Types and Libraries](../../../docs/framework/xaml-services/xaml-related-clr-attributes-for-custom-types-and-libraries.md).  
  
## Utilizzo  
 L'utilizzo dei tipi personalizzati richiede che l'autore del markup esegua il mapping di un prefisso per l'assembly e lo spazio dei nomi CLR contenenti il tipo personalizzato.  La procedura non è documentata in questo argomento.  
  
## Livello di accesso  
 XAML fornisce i mezzi per caricare e creare istanze dei tipi con un livello di accesso `internal`.  Questa funzionalità consente di definire tipi personalizzati dal codice utente, quindi creare istanze di tali classi dal markup che fa parte dell'ambito dello stesso codice utente.  
  
 Un esempio di WPF è ogni caso in cui il codice utente definisce un oggetto <xref:System.Windows.Controls.UserControl> inteso come modo per il refactoring di un comportamento dell'interfaccia utente, ma non come parti di qualsiasi possibile meccanismo di estensione che potrebbe essere implicito mediante la dichiarazione della classe di supporto con il livello di accesso `public`.  Tale oggetto <xref:System.Windows.Controls.UserControl> può essere dichiarato con accesso `internal` se il codice di supporto viene compilato nello stesso assembly che contiene un riferimento a esso come tipo XAML.  
  
 Per un'applicazione che carica XAML in attendibilità totale e utilizza <xref:System.Xaml.XamlObjectWriter>, il caricamento di classi con livello di accesso `internal` è sempre abilitato.  
  
 Per un'applicazione che carica XAML in attendibilità parziale, è possibile controllare le caratteristiche del livello di accesso utilizzando l'API <xref:System.Xaml.Permissions.XamlAccessLevel>.  Inoltre, i meccanismi di posticipazione \(ad esempio il sistema dei modelli WPF\) devono essere in grado di propagare qualsiasi autorizzazione di livello di accesso e conservarle per le valutazioni finali della fase di esecuzione; questo passaggio viene gestito internamente passando le informazioni di <xref:System.Xaml.Permissions.XamlAccessLevel>.  
  
### Implementazione di WPF  
 In XAML WPF viene utilizzato un modello di accesso ad attendibilità parziale secondo cui se BAML viene caricato in attendibilità parziale, l'accesso è limitato a <xref:System.Xaml.Permissions.XamlAccessLevel.AssemblyAccessTo%2A> per l'assembly che è l'origine di BAML.  Per la posticipazione, in WPF<xref:System.Xaml.IXamlObjectWriterFactory.GetParentSettings%2A?displayProperty=fullName> viene utilizzato come meccanismo per il passaggio delle informazioni del livello di accesso.  
  
 Nella terminologia di XAML WPF, per *tipo interno* si intende un tipo definito dallo stesso assembly che include anche il codice XAML di riferimento.  Tale tipo può essere mappato tramite uno spazio dei nomi XAML in cui viene deliberatamente omessa la parte assembly\= di un mapping, ad esempio `xmlns:local="clr-namespace:WPFApplication1"`.  Se BAML fa riferimento a un tipo interno e tale tipo ha livello di accesso `internal`, viene generata una classe `GeneratedInternalTypeHelper` per l'assembly.  Per evitare `GeneratedInternalTypeHelper`, è necessario utilizzare il livello di accesso `public` o eseguire il factoring della classe rilevante in un assembly separato e rendere tale assembly dipendente.  
  
## Vedere anche  
 [XAML\-Related CLR Attributes for Custom Types and Libraries](../../../docs/framework/xaml-services/xaml-related-clr-attributes-for-custom-types-and-libraries.md)   
 [XAML Services](../../../docs/framework/xaml-services/index.md)