---
title: "Interfacce correlate all&#39;associazione dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "dati [Windows Form], interfacce di associazione dati"
  - "associazione dati, interfacce"
  - "IBindingList (interfaccia), associazione dati in Windows Form"
  - "IBindingListView (interfaccia)"
  - "IDataErrorInfo (interfaccia), associazione dati in Windows Form"
  - "IEditableObject (interfaccia), associazione dati in Windows Form"
  - "IList (interfaccia), associazione dati in Windows Form"
  - "INotifyPropertyChanged (interfaccia)"
  - "interfacce, associazione dati in Windows Form"
ms.assetid: 14e49a2e-3e46-47ca-b491-70d546333277
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Interfacce correlate all&#39;associazione dati
[!INCLUDE[vstecado](../../../includes/vstecado-md.md)] consente di creare numerose strutture di dati diverse per soddisfare le esigenze di associazione specifiche dell'applicazione e dei dati utilizzati.  Può essere opportuno creare proprie classi che forniscano o utilizzino i dati in Windows Form.  Questi oggetti sono in grado di offrire diversi livelli di funzionalità e complessità, dall'associazione semplice di dati alla fornitura di supporto in fase di progettazione, al controllo degli errori, alla notifica delle modifiche, fino al ripristino strutturato dello stato precedente le modifiche apportate ai dati.  
  
## Consumer delle interfacce di associazione dati  
 Nelle sezioni successive vengono descritti due gruppi di oggetti interfaccia.  Nel primo gruppo sono elencate le interfacce che vengono implementate sulle origini dati dagli autori di origini dati.  Queste interfacce sono progettate per l'utilizzo da parte dei consumer di origini dati, che nella maggior parte dei casi sono rappresentati da controlli o componenti Windows Form.  Nel secondo gruppo sono elencate le interfacce progettate per l'utilizzo da parte degli autori di componenti.  Gli autori di componenti utilizzano queste interfacce quando creano un componente che prevede l'utilizzo dell'associazione dati da parte del modulo di associazione dati Windows Form.  È possibile implementare queste interfacce all'interno di classi associate al form per abilitare l'associazione dati; ogni caso presenta una classe che implementa un'interfaccia che abilita l'interazione con i dati.  Gli strumenti di progettazione dati sviluppo rapido di applicazioni \(RAD\) di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] sfruttano già questa funzionalità.  
  
### Interfacce per l'implementazione da parte degli autori di origini dati  
 Le interfacce descritte di seguito sono progettate per l'utilizzo da parte di controlli Windows Form:  
  
-   Interfaccia <xref:System.Collections.IList>  
  
     Una classe che implementa l'interfaccia <xref:System.Collections.IList> potrebbe essere <xref:System.Array>, <xref:System.Collections.ArrayList> o <xref:System.Collections.CollectionBase>.  Si tratta di elenchi indicizzati di elementi di tipo <xref:System.Object>.  Questi elenchi devono contenere tipi omogenei, perché il primo elemento dell'indice determina il tipo.  <xref:System.Collections.IList> sarà disponibile per l'associazione solo in fase di esecuzione.  
  
    > [!NOTE]
    >  Se si desidera creare un elenco di oggetti business per l'associazione con Windows Form, è necessario prendere in considerazione l'utilizzo di <xref:System.ComponentModel.BindingList%601>.  <xref:System.ComponentModel.BindingList%601> è una classe estensibile che implementa le interfacce primarie richieste per l'associazione dati bidirezionale di Windows Form.  
  
-   Interfaccia <xref:System.ComponentModel.IBindingList>  
  
     Una classe che implementa l'interfaccia <xref:System.ComponentModel.IBindingList> fornisce funzionalità per l'associazione dati di livello decisamente superiore.  Questa implementazione fornisce funzionalità di ordinamento di base e la notifica delle modifiche, sia per modifiche delle voci contenute nell'elenco, ad esempio per una variazione nel campo Indirizzo della terza voce di un elenco di clienti, sia per cambiamenti dell'elenco stesso, ad esempio dovuti a un aumento o a una diminuzione delle voci presenti nell'elenco.  La notifica delle modifiche è importante quando si pianifica di associare più controlli agli stessi dati e si desidera che la modifica dei dati avvenga in uno dei controlli e venga propagata agli altri controlli associati.  
  
    > [!NOTE]
    >  La notifica delle modifiche viene attivata per l'interfaccia <xref:System.ComponentModel.IBindingList> mediante la proprietà <xref:System.ComponentModel.IBindingList.SupportsChangeNotification%2A> che, se impostata su `true`, genera un evento <xref:System.ComponentModel.IBindingList.ListChanged>, il quale indica che l'elenco o una voce nell'elenco è cambiata.  
  
     Il tipo di modifica è descritto dalla proprietà <xref:System.ComponentModel.ListChangedType> del parametro <xref:System.ComponentModel.ListChangedEventArgs>.  Ogni volta che il modello di dati viene aggiornato, dunque, verranno aggiornate anche tutte le visualizzazioni dipendenti, come ad esempio gli altri controlli associati alla stessa origine dati.  Gli oggetti contenuti nell'elenco dovranno tuttavia segnalare all'elenco quando subiscono modifiche, in modo che l'elenco possa generare l'evento <xref:System.ComponentModel.IBindingList.ListChanged>.  
  
    > [!NOTE]
    >  La classe <xref:System.ComponentModel.BindingList%601> fornisce un'implementazione generica dell'interfaccia <xref:System.ComponentModel.IBindingList>.  
  
-   Interfaccia <xref:System.ComponentModel.IBindingListView>  
  
     Una classe che implementa l'interfaccia <xref:System.ComponentModel.IBindingListView> fornisce tutte le funzionalità di un'implementazione di <xref:System.ComponentModel.IBindingList> e le funzionalità di filtro e ordinamento avanzato.  Questa implementazione fornisce funzionalità di filtro basate su stringhe e di ordinamento multicolonna con coppie descrittore\-direzione delle proprietà.  
  
-   Interfaccia <xref:System.ComponentModel.IEditableObject>  
  
     Una classe che implementa l'interfaccia <xref:System.ComponentModel.IEditableObject> consente a un oggetto di controllare quando le modifiche apportate a tale oggetto sono permanenti.  Questa implementazione mette a disposizione i metodi <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.EndEdit%2A> e <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> che consentono di ripristinare lo stato precedente e le modifiche apportate all'oggetto.  Di seguito viene fornita una breve descrizione del funzionamento dei metodi <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.EndEdit%2A> e <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> e della relativa interazione per attivare un possibile ripristino dello stato precedente le modifiche apportate ai dati:  
  
    -   Il metodo <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> segnala l'inizio della modifica di un oggetto.  È necessario che un oggetto che implementa questa interfaccia esegua l'archiviazione di qualsiasi aggiornamento dopo la chiamata al metodo <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> in modo da poter annullare gli aggiornamenti se viene chiamato il metodo <xref:System.ComponentModel.IEditableObject.CancelEdit%2A>.  Nell'associazione dati in Windows Form è possibile chiamare il metodo <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> più volte nell'ambito di una singola transazione di modifica, ad esempio <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.EndEdit%2A>\).  Le implementazioni di <xref:System.ComponentModel.IEditableObject> devono consentire di controllare se il metodo <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> è già stato chiamato e ignorare le chiamate successive al metodo <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>.  Poiché questo metodo può essere chiamato più volte, è importante che le chiamate successive non siano distruttive, ovvero che le successive chiamate a <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> non eliminino gli aggiornamenti o le modifiche apportate ai dati salvati con la prima chiamata a <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>.  
  
    -   Il metodo <xref:System.ComponentModel.IEditableObject.EndEdit%2A> inserisce nell'oggetto sottostante tutte le modifiche apportate dopo la chiamata a <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, se l'oggetto si trova in modalità di modifica.  
  
    -   Il metodo <xref:System.ComponentModel.IEditableObject.CancelEdit%2A> annulla tutte le modifiche apportate all'oggetto.  
  
     Per ulteriori informazioni sul funzionamento dei metodi <xref:System.ComponentModel.IEditableObject.BeginEdit%2A>, <xref:System.ComponentModel.IEditableObject.EndEdit%2A> e <xref:System.ComponentModel.IEditableObject.CancelEdit%2A>, vedere [Salvataggio dei dati nei dataset](../Topic/Save%20data%20back%20to%20the%20database.md).  
  
     Questa nozione transazionale delle funzionalità dei dati viene utilizzata dal controllo <xref:System.Windows.Forms.DataGridView>.  
  
-   Interfaccia <xref:System.ComponentModel.ICancelAddNew>  
  
     Di solito, una classe che implementa l'interfaccia <xref:System.ComponentModel.ICancelAddNew> implementa anche l'interfaccia <xref:System.ComponentModel.IBindingList> e consente di ripristinare un'aggiunta apportata all'origine dati con il metodo <xref:System.ComponentModel.IBindingList.AddNew%2A>.  Se l'origine dati implementa l'interfaccia <xref:System.ComponentModel.IBindingList>, è necessario che implementi anche l'interfaccia <xref:System.ComponentModel.ICancelAddNew>.  
  
-   Interfaccia <xref:System.ComponentModel.IDataErrorInfo>  
  
     Una classe che implementa l'interfaccia <xref:System.ComponentModel.IDataErrorInfo> consente agli oggetti di fornire informazioni personalizzate sugli errori ai controlli associati:  
  
    -   La proprietà <xref:System.ComponentModel.IDataErrorInfo.Error%2A> restituisce il testo di messaggi di errore generici, ad esempio "Si è verificato un errore".  
  
    -   La proprietà <xref:System.ComponentModel.IDataErrorInfo.Item%2A> restituisce una stringa con un messaggio di errore specifico dalla colonna, ad esempio "Il valore della colonna `State` non è valido".  
  
-   Interfaccia <xref:System.Collections.IEnumerable>  
  
     Una classe che implementa l'interfaccia <xref:System.Collections.IEnumerable> è generalmente utilizzata da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)].  Il supporto Windows Form per questa interfaccia è disponibile solo mediante il componente <xref:System.Windows.Forms.BindingSource>.  
  
    > [!NOTE]
    >  Il componente <xref:System.Windows.Forms.BindingSource> copia tutti gli elementi dell'interfaccia <xref:System.Collections.IEnumerable> in un elenco separato per motivi di associazione.  
  
-   Interfaccia <xref:System.ComponentModel.ITypedList>  
  
     Una classe di raccolte che implementa l'interfaccia <xref:System.ComponentModel.ITypedList> consente di gestire l'ordine e il set di proprietà esposte al controllo associato.  
  
    > [!NOTE]
    >  Quando si implementa il metodo <xref:System.ComponentModel.ITypedList.GetItemProperties%2A> e l'array <xref:System.ComponentModel.PropertyDescriptor> non è null, l'ultima voce della matrice sarà il descrittore della proprietà che descrive la proprietà elenco rappresentata da un altro elenco di elementi.  
  
-   Interfaccia <xref:System.ComponentModel.ICustomTypeDescriptor>  
  
     Una classe che implementa l'interfaccia <xref:System.ComponentModel.ICustomTypeDescriptor> fornisce informazioni dinamiche su se stessa.  Questa interfaccia è simile a <xref:System.ComponentModel.ITypedList> ma è utilizzata per oggetti diversi dagli elenchi.  L'interfaccia è utilizzata dalla classe <xref:System.Data.DataRowView> per proiettare lo schema delle righe sottostanti.  Una implementazione semplice di <xref:System.ComponentModel.ICustomTypeDescriptor> viene fornita dalla classe <xref:System.ComponentModel.CustomTypeDescriptor>.  
  
    > [!NOTE]
    >  Per supportare l'associazione in fase di progettazione a tipi che implementano l'interfaccia <xref:System.ComponentModel.ICustomTypeDescriptor>, il tipo deve implementare anche l'interfaccia <xref:System.ComponentModel.IComponent> e deve esistere in un'istanza nel form.  
  
-   Interfaccia <xref:System.ComponentModel.IListSource>  
  
     Una classe che implementa l'interfaccia <xref:System.ComponentModel.IListSource> consente l'associazione basata su elenchi in oggetti non di elenco.  Il metodo <xref:System.ComponentModel.IListSource.GetList%2A> di <xref:System.ComponentModel.IListSource> è utilizzato per restituire un elenco associabile da un oggetto che non eredita da <xref:System.Collections.IList>.  L'oggetto <xref:System.ComponentModel.IListSource> è utilizzato dalla classe <xref:System.Data.DataSet>.  
  
-   Interfaccia <xref:System.ComponentModel.IRaiseItemChangedEvents>  
  
     Una classe che implementa l'interfaccia <xref:System.ComponentModel.IRaiseItemChangedEvents> è un elenco associabile che implementa anche l'interfaccia <xref:System.ComponentModel.IBindingList>.  Questa interfaccia è utilizzata per indicare se il tipo genera eventi <xref:System.ComponentModel.IBindingList.ListChanged> di tipo <xref:System.ComponentModel.ListChangedType> mediante la proprietà <xref:System.ComponentModel.IRaiseItemChangedEvents.RaisesItemChangedEvents%2A>.  
  
    > [!NOTE]
    >  È necessario implementare l'interfaccia <xref:System.ComponentModel.IRaiseItemChangedEvents> se l'origine dati fornisce la proprietà per elencare la conversione degli eventi descritta precedentemente e interagisce con il componente <xref:System.Windows.Forms.BindingSource>.  In caso contrario, anche l'interfaccia <xref:System.Windows.Forms.BindingSource> eseguirà la proprietà per elencare la conversione degli eventi, con conseguente riduzione delle prestazioni.  
  
-   Interfaccia <xref:System.ComponentModel.ISupportInitialize>  
  
     Un componente che implementa l'interfaccia <xref:System.ComponentModel.ISupportInitialize> trae vantaggio dalle ottimizzazioni batch per l'impostazione delle proprietà e l'inizializzazione delle proprietà codipendenti.  L'interfaccia <xref:System.ComponentModel.ISupportInitialize> contiene due metodi:  
  
    -   Il metodo <xref:System.ComponentModel.ISupportInitialize.BeginInit%2A> segnala l'avvio dell'inizializzazione dell'oggetto.  
  
    -   Il metodo <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> segnala la fine dell'inizializzazione dell'oggetto.  
  
-   Interfaccia <xref:System.ComponentModel.ISupportInitializeNotification>  
  
     Un componente che implementa l'interfaccia <xref:System.ComponentModel.ISupportInitializeNotification> implementa anche l'interfaccia <xref:System.ComponentModel.ISupportInitialize>.  Questa interfaccia consente di notificare agli altri componenti dell'interfaccia <xref:System.ComponentModel.ISupportInitialize> il completamento dell'inizializzazione.  L'interfaccia <xref:System.ComponentModel.ISupportInitializeNotification> contiene due membri:  
  
    -   La proprietà <xref:System.ComponentModel.ISupportInitializeNotification.IsInitialized%2A> restituisce un valore `boolean` che indica se il componente è stato inizializzato.  
  
    -   L'evento <xref:System.ComponentModel.ISupportInitializeNotification.Initialized> si verifica quando viene chiamato il metodo <xref:System.ComponentModel.ISupportInitialize.EndInit%2A>.  
  
-   Interfaccia <xref:System.ComponentModel.INotifyPropertyChanged>  
  
     Una classe che implementa questa interfaccia è un tipo che genera un evento al variare di uno dei rispettivi valori di proprietà.  L'interfaccia è progettata per sostituire il criterio che prevede un evento di modifica per ciascuna proprietà di un controllo.  Quando è utilizzata in una classe <xref:System.ComponentModel.BindingList%601>, l'oggetto business deve implementare l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> e la classe BindingList\`1 convertirà gli eventi <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> in eventi <xref:System.ComponentModel.BindingList%601.ListChanged> di tipo <xref:System.ComponentModel.ListChangedType>.  
  
    > [!NOTE]
    >  Perché possano essere notificate le modifiche in un'associazione tra un client associato e un'origine dati, il tipo di origine dati associata deve implementare l'interfaccia <xref:System.ComponentModel.INotifyPropertyChanged> \(opzione preferita\); in alternativa, si possono fornire eventi *NomeProprietà*`Changed` per il tipo associato, ma non si possono svolgere entrambe le operazioni.  
  
### Interfacce per l'implementazione da parte degli autori di componenti  
 Le interfacce descritte di seguito sono progettate per l'utilizzo da parte del modulo di associazione dati di Windows Form:  
  
-   Interfaccia <xref:System.Windows.Forms.IBindableComponent>  
  
     Una classe che implementa questa interfaccia è un componente diverso da un controllo che supporta l'associazione dati.  Tale classe restituisce le associazioni dati e il contesto di associazione del componente mediante le proprietà <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> e <xref:System.Windows.Forms.IBindableComponent.BindingContext%2A> dell'interfaccia.  
  
    > [!NOTE]
    >  Se il componente eredita dalla classe <xref:System.Windows.Forms.Control>, non occorre implementare l'interfaccia <xref:System.Windows.Forms.IBindableComponent>.  
  
-   Interfaccia <xref:System.Windows.Forms.ICurrencyManagerProvider>  
  
     Una classe che implementa l'interfaccia <xref:System.Windows.Forms.ICurrencyManagerProvider> è un componente che fornisce la propria classe <xref:System.Windows.Forms.CurrencyManager> per gestire le associazioni abbinate a questo particolare componente.  L'accesso alla classe <xref:System.Windows.Forms.CurrencyManager> personalizzata è fornito dalla proprietà <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A>.  
  
    > [!NOTE]
    >  Poiché una classe che eredita da <xref:System.Windows.Forms.Control> gestisce automaticamente le associazioni mediante la proprietà <xref:System.Windows.Forms.Control.BindingContext%2A>, i casi in cui occorre implementare l'interfaccia <xref:System.Windows.Forms.ICurrencyManagerProvider> sono piuttosto rari.  
  
## Vedere anche  
 [Associazione dati e Windows Form](../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [Procedura: creare un controllo con associazione semplice in un Windows Form](../../../docs/framework/winforms/how-to-create-a-simple-bound-control-on-a-windows-form.md)   
 [Associazione ai dati di Windows Form](../../../docs/framework/winforms/windows-forms-data-binding.md)