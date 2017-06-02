---
title: "Architettura del componente BindingSource | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BindingSource (componente) [Windows Form], informazioni sul componente BindingSource"
  - "BindingSource (componente), architettura"
  - "associazione dati, BindingSource (componente)"
  - "Windows Form, associazione dati"
ms.assetid: 7bc69c90-8a11-48b1-9336-3adab5b41591
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Architettura del componente BindingSource
Con il componente <xref:System.Windows.Forms.BindingSource>, è possibile associare tutti i controlli Windows Form alle origini dati a livello universale.  
  
 Il componente <xref:System.Windows.Forms.BindingSource> semplifica il processo di associazione dei controlli a un'origine dati e offre i seguenti vantaggi rispetto all'associazione dati tradizionale:  
  
-   Consente l'associazione agli oggetti business in fase di progettazione.  
  
-   Incapsula le funzionalità della classe <xref:System.Windows.Forms.CurrencyManager> ed espone gli eventi <xref:System.Windows.Forms.CurrencyManager> in fase di progettazione.  
  
-   Semplifica la creazione di un elenco che supporta l'interfaccia <xref:System.ComponentModel.IBindingList> fornendo la notifica delle eventuali modifiche nell'elenco per le origini dati che non supportano tale notifica a livello nativo.  
  
-   Fornisce un punto di estendibilità per il metodo <xref:System.ComponentModel.IBindingList.AddNew%2A?displayProperty=fullName>.  
  
-   Fornisce un livello di riferimento indiretto tra l'origine dati e il controllo.  Questa caratteristica è importante quando esiste la possibilità che l'origine dati cambi in fase di esecuzione.  
  
-   Consente di interoperare con altri controlli Windows Form correlati ai dati, in particolare il controllo <xref:System.Windows.Forms.BindingNavigator> e i controlli <xref:System.Windows.Forms.DataGridView>.  
  
 Per questi motivi il componente <xref:System.Windows.Forms.BindingSource> rappresenta il modo ottimale per associare i controlli Windows Form alle origini dati.  
  
## Funzionalità di BindingSource  
 Il componente <xref:System.Windows.Forms.BindingSource> fornisce diverse funzionalità per l'associazione dei controlli ai dati,  che consentono di implementare la maggior parte degli scenari di associazione dati con l'aggiunta di un semplice codice.  
  
 Ciò è possibile in quanto il componente <xref:System.Windows.Forms.BindingSource> fornisce un'interfaccia coerente per l'accesso a molti tipi di origini dati diversi.  Ciò significa che è possibile utilizzare la stessa procedura per l'associazione a qualsiasi tipo.  È ad esempio possibile collegare la proprietà <xref:System.Windows.Forms.BindingSource.DataSource%2A> a un <xref:System.Data.DataSet> o a un oggetto business e in entrambi i casi si utilizza lo stesso insieme di proprietà, metodi ed eventi per modificare l'origine dati.  
  
 L'interfaccia coerente fornita dal componente <xref:System.Windows.Forms.BindingSource> semplifica notevolmente il processo di associazione tra dati e controlli.  Per i tipi di origini dati che supportano la notifica delle modifiche, il componente <xref:System.Windows.Forms.BindingSource> comunica automaticamente le modifiche verificatesi tra il controllo e l'origine dati.  Per i tipi di origini dati che non supportano la notifica delle modifiche vengono forniti eventi che consentono di generare tali notifiche.  Nell'elenco seguente sono indicate le funzioni supportate dal componente <xref:System.Windows.Forms.BindingSource>:  
  
-   Riferimento indiretto  
  
-   Gestione della diffusione dei dati  
  
-   Origine dati sotto forma di elenco  
  
-   <xref:System.Windows.Forms.BindingSource> sotto forma di interfaccia <xref:System.ComponentModel.IBindingList>  
  
-   Creazione elementi personalizzata  
  
-   Creazione elementi transazionale  
  
-   Supporto dell'interfaccia <xref:System.Collections.IEnumerable>  
  
-   Supporto della fase di progettazione  
  
-   Metodi <xref:System.Windows.Forms.ListBindingHelper> static  
  
-   Ordinamento e filtro con l'interfaccia <xref:System.ComponentModel.IBindingListView>  
  
-   Integrazione con <xref:System.Windows.Forms.BindingNavigator>  
  
### Riferimento indiretto  
 Il componente <xref:System.Windows.Forms.BindingSource> fornisce un livello di riferimento indiretto tra un controllo e un'origine dati.  Anziché associare un controllo direttamente a un'origine dati, lo si associa a un componente <xref:System.Windows.Forms.BindingSource> e si collega l'origine dati alla proprietà <xref:System.Windows.Forms.BindingSource.DataSource%2A> del componente <xref:System.Windows.Forms.BindingSource>.  
  
 Tale livello di riferimento indiretto consente di cambiare l'origine dati senza reimpostare l'associazione del controllo.  Ciò rende possibili le operazioni seguenti:  
  
-   Collegamento del componente <xref:System.Windows.Forms.BindingSource> a origini dati diverse mantenendo nel contempo le associazioni correnti del controllo.  
  
-   Modifica degli elementi nell'origine dati e invio di una notifica ai controlli associati.  Per ulteriori informazioni, vedere [Procedura: riflettere gli aggiornamenti dell'origine dati in un controllo Windows Form con BindingSource](../../../../docs/framework/winforms/controls/reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md).  
  
-   Associazione a una classe <xref:System.Type> anziché a un oggetto in memoria.  Per ulteriori informazioni, vedere [Procedura: associare un controllo Windows Form a un tipo](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md).  L'associazione a un oggetto può essere eseguita in fase di esecuzione.  
  
### Gestione della diffusione dei dati  
 Il componente <xref:System.Windows.Forms.BindingSource> implementa l'interfaccia <xref:System.Windows.Forms.ICurrencyManagerProvider> per la gestione automatica della diffusione dei dati.  Utilizzando l'interfaccia <xref:System.Windows.Forms.ICurrencyManagerProvider> è inoltre possibile accedere all'oggetto CurrencyManager relativo a un oggetto <xref:System.Windows.Forms.BindingSource> e a un altro oggetto <xref:System.Windows.Forms.BindingSource> associato allo stesso <xref:System.Windows.Forms.BindingSource.DataMember%2A>.  
  
 Il componente <xref:System.Windows.Forms.BindingSource> incapsula funzionalità di <xref:System.Windows.Forms.CurrencyManager> ed espone proprietà ed eventi più comuni di <xref:System.Windows.Forms.CurrencyManager>.  Nella tabella seguente sono descritti alcuni membri correlati alla gestione della diffusione dei dati.  
  
 Proprietà <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A>  
 Ottiene l'oggetto CurrencyManager associato al <xref:System.Windows.Forms.BindingSource>.  
  
 Metodo <xref:System.Windows.Forms.ICurrencyManagerProvider.GetRelatedCurrencyManager%2A>  
 Se esiste un altro <xref:System.Windows.Forms.BindingSource> associato al membro dati specificato, ne ottiene l'oggetto CurrencyManager.  
  
 Proprietà <xref:System.Windows.Forms.BindingSource.Current%2A>  
 Ottiene l'elemento corrente dell'origine dati.  
  
 Proprietà <xref:System.Windows.Forms.BindingSource.Position%2A>  
 Ottiene o imposta la posizione corrente nell'elenco sottostante.  
  
 Metodo <xref:System.Windows.Forms.BindingSource.EndEdit%2A>  
 Applica modifiche in sospeso all'origine dati sottostante.  
  
 Metodo <xref:System.Windows.Forms.BindingSource.CancelEdit%2A>  
 Annulla l'operazione di modifica corrente.  
  
### Origine dati sotto forma di elenco  
 Il componente <xref:System.Windows.Forms.BindingSource> implementa le interfacce <xref:System.ComponentModel.IBindingListView> e <xref:System.ComponentModel.ITypedList>.  Ciò consente di utilizzare il componente <xref:System.Windows.Forms.BindingSource> stesso come origine dati, senza archivio esterno.  
  
 Quando il componente <xref:System.Windows.Forms.BindingSource> è collegato a un'origine dati, espone l'origine dati sotto forma di elenco.  
  
 La proprietà <xref:System.Windows.Forms.BindingSource.DataSource%2A> può essere impostata su diverse origini dati,  tra cui tipi, oggetti ed elenchi di tipi.  L'origine dati risultante verrà esposta sotto forma di elenco.  Nella tabella seguente sono indicate alcune origini dati comuni e l'elenco che risulta dalla valutazione.  
  
|Proprietà DataSource|Risultati dell'elenco|  
|--------------------------|---------------------------|  
|Riferimento null \(`Nothing` in Visual Basic\)|Un'interfaccia <xref:System.ComponentModel.IBindingList> vuota di oggetti.  Con l'aggiunta di un elemento l'elenco viene impostato sul tipo dell'elemento aggiunto.|  
|Riferimento null \(`Nothing` in Visual Basic\) con la proprietà <xref:System.Windows.Forms.BindingSource.DataMember%2A> impostata|Non supportato. Genera <xref:System.ArgumentException>.|  
|Tipo non di elenco o oggetto di tipo "T"|Un'interfaccia <xref:System.ComponentModel.IBindingList> vuota del tipo "T".|  
|Istanza di matrice|Un'interfaccia <xref:System.ComponentModel.IBindingList> contenente gli elementi della matrice.|  
|Istanza dell'interfaccia <xref:System.Collections.IEnumerable>|Un'interfaccia <xref:System.ComponentModel.IBindingList> contenente gli elementi di <xref:System.Collections.IEnumerable>.|  
|Istanza di elenco contenente il tipo "T"|Un'istanza di <xref:System.ComponentModel.IBindingList> contenente il tipo "T".|  
  
 Inoltre, la proprietà <xref:System.Windows.Forms.BindingSource.DataSource%2A> può essere impostata su altri tipi di elenco, ad esempio <xref:System.ComponentModel.IListSource> e <xref:System.ComponentModel.ITypedList>, e l'oggetto <xref:System.Windows.Forms.BindingSource> li gestirà in modo appropriato.  In questo caso, è necessario che il tipo contenuto nell'elenco disponga di un costruttore predefinito.  
  
### BindingSource sotto forma di un'interfaccia IBindingList  
 Il componente <xref:System.Windows.Forms.BindingSource> fornisce membri per l'accesso e la modifica dei dati sottostanti sotto forma di un'interfaccia <xref:System.ComponentModel.IBindingList>.  Nella tabella seguente sono descritti alcuni di tali membri.  
  
|Membro|Descrizione|  
|------------|-----------------|  
|Proprietà <xref:System.Windows.Forms.BindingSource.List%2A>|Ottiene l'elenco che risulta dalla valutazione della proprietà <xref:System.Windows.Forms.BindingSource.DataSource%2A> o <xref:System.Windows.Forms.BindingSource.DataMember%2A>.|  
|Metodo <xref:System.Windows.Forms.BindingSource.AddNew%2A>|Aggiunge un nuovo elemento all'elenco sottostante.  Viene applicato a origini dati che implementano l'interfaccia <xref:System.ComponentModel.IBindingList> e consentono l'aggiunta di elementi, vale a dire quando la proprietà <xref:System.Windows.Forms.BindingSource.AllowNew%2A> è impostata su `true`.|  
  
### Creazione elementi personalizzata  
 È possibile gestire l'evento <xref:System.Windows.Forms.BindingSource.AddingNew> per fornire una logica di creazione elementi personalizzata.  L'evento <xref:System.Windows.Forms.BindingSource.AddingNew> si verifica prima che un nuovo oggetto venga aggiunto al <xref:System.Windows.Forms.BindingSource>.  Viene generato dopo la chiamata del metodo <xref:System.Windows.Forms.BindingSource.AddNew%2A> ma prima che il nuovo elemento venga aggiunto all'elenco sottostante.  La gestione dell'evento consente di fornire un comportamento di creazione elementi personalizzato senza derivazione dalla classe <xref:System.Windows.Forms.BindingSource>.  Per ulteriori informazioni, vedere [Procedura: personalizzare l'aggiunta di elementi con BindingSource Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-item-addition-with-the-windows-forms-bindingsource.md).  
  
### Creazione elementi transazionale  
 Il componente <xref:System.Windows.Forms.BindingSource> implementa l'interfaccia <xref:System.ComponentModel.ICancelAddNew>, che consente la creazione di elementi transazionale.  Dopo la creazione temporanea di un nuovo elemento mediante una chiamata al metodo <xref:System.Windows.Forms.BindingSource.AddNew%2A>, è possibile eseguire il commit o il rollback dell'aggiunta nei modi seguenti:  
  
-   Con il metodo <xref:System.ComponentModel.ICancelAddNew.EndNew%2A> il commit dell'aggiunta in sospeso viene eseguito in modo esplicito.  
  
-   Con l'esecuzione di un'altra operazione sulle raccolte, ad esempio un inserimento, una rimozione o uno spostamento, il commit dell'aggiunta in sospeso viene eseguito in modo implicito.  
  
-   Con il metodo <xref:System.ComponentModel.ICancelAddNew.CancelNew%2A> viene eseguito il rollback dell'aggiunta in sospeso se il commit non è stato ancora eseguito.  
  
### Supporto di IEnumerable  
 Il componente <xref:System.Windows.Forms.BindingSource> consente l'associazione di controlli a origini dati <xref:System.Collections.IEnumerable>.  Con tale componente è possibile eseguire un'associazione a un'origine dati come una classe <xref:System.Data.SqlClient.SqlDataReader?displayProperty=fullName>.  
  
 Quando un'origine dati <xref:System.Collections.IEnumerable> è assegnata al componente <xref:System.Windows.Forms.BindingSource>, il <xref:System.Windows.Forms.BindingSource> crea un'interfaccia <xref:System.ComponentModel.IBindingList> e aggiunge il contenuto dell'origine dati <xref:System.Collections.IEnumerable> all'elenco.  
  
### Supporto della fase di progettazione  
 Alcuni tipi di oggetto non possono essere creati in fase di progettazione, ad esempio gli oggetti creati da una class factory o quelli restituiti da un servizio Web.  Talvolta può essere necessario associare controlli a questi tipi in fase di progettazione, anche se non esiste alcun oggetto in memoria a cui associare i controlli.  Potrebbe, ad esempio, essere necessario etichettare le intestazioni di colonna di un controllo <xref:System.Windows.Forms.DataGridView> con i nomi delle proprietà pubbliche del tipo personalizzato.  
  
 Per tale scenario il componente <xref:System.Windows.Forms.BindingSource> supporta l'associazione a una classe <xref:System.Type>.  Quando si assegna una classe <xref:System.Type> alla proprietà <xref:System.Windows.Forms.BindingSource.DataSource%2A>, il componente <xref:System.Windows.Forms.BindingSource> crea una classe <xref:System.ComponentModel.BindingList%601> vuota di elementi <xref:System.Type>.  Agli eventuali controlli associati successivamente al componente <xref:System.Windows.Forms.BindingSource> verrà comunicata la presenza delle proprietà o dello schema del tipo in fase di progettazione o di esecuzione.  Per ulteriori informazioni, vedere [Procedura: associare un controllo Windows Form a un tipo](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md).  
  
### Metodi ListBindingHelper static  
 I tipi <xref:System.Windows.Forms.BindingContext?displayProperty=fullName>, <xref:System.Windows.Forms.CurrencyManager?displayProperty=fullName> e <xref:System.Windows.Forms.BindingSource> condividono tutti una logica comune per generare un elenco da una coppia `DataSource`\/`DataMember`.  Questa logica comune, inoltre, viene esposta pubblicamente per essere utilizzata dagli autori di controlli e da altri utenti nei seguenti metodi `static`:  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListItemProperties%2A>  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetList%2A>.  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListName%2A>  
  
-   <xref:System.Windows.Forms.ListBindingHelper.GetListItemType%2A>  
  
### Ordinamento e filtro con l'interfaccia IBindingListView  
 Il componente <xref:System.Windows.Forms.BindingSource> implementa l'interfaccia <xref:System.ComponentModel.IBindingListView>, che estende l'interfaccia <xref:System.ComponentModel.IBindingList>.  L'interfaccia <xref:System.ComponentModel.IBindingList> consente l'ordinamento di singole colonne mentre <xref:System.ComponentModel.IBindingListView> offre funzioni di filtro e ordinamento avanzato.  Con <xref:System.ComponentModel.IBindingListView> è possibile ordinare e filtrare gli elementi nell'origine dati, a condizione che anche in quest'ultima sia implementata una di queste interfacce.  Il componente <xref:System.Windows.Forms.BindingSource> non fornisce un'implementazione di riferimento di tali membri.  Le chiamate, al contrario, vengono inoltrate all'elenco sottostante.  
  
 Nella tabella seguente vengono descritte le proprietà utilizzate per l'ordinamento e il filtro.  
  
|Membro|Descrizione|  
|------------|-----------------|  
|Proprietà <xref:System.Windows.Forms.BindingSource.Filter%2A>|Se l'origine dati è un'interfaccia <xref:System.ComponentModel.IBindingListView>, ottiene o imposta l'espressione utilizzata per filtrare le righe visualizzate.|  
|Proprietà <xref:System.Windows.Forms.BindingSource.Sort%2A>|Se l'origine dati è un'interfaccia <xref:System.ComponentModel.IBindingList>, ottiene o imposta un nome di colonna utilizzato per l'ordinamento e il criterio di ordinamento.<br /><br /> In alternativa<br /><br /> Se l'origine dati è un'interfaccia <xref:System.ComponentModel.IBindingListView> e supporta l'ordinamento avanzato, ottiene più nomi di colonna utilizzati per l'ordinamento e il criterio di ordinamento.|  
  
### Integrazione con BindingNavigator  
 È possibile utilizzare il componente <xref:System.Windows.Forms.BindingSource> per associare qualsiasi controllo Windows Form a un'origine dati ma il controllo <xref:System.Windows.Forms.BindingNavigator> è progettato in modo specifico per l'utilizzo con il componente <xref:System.Windows.Forms.BindingSource>.  Il controllo <xref:System.Windows.Forms.BindingNavigator> fornisce un'interfaccia utente per il controllo dell'elemento corrente del componente <xref:System.Windows.Forms.BindingSource>.  Per impostazione predefinita il controllo <xref:System.Windows.Forms.BindingNavigator> fornisce pulsanti che corrispondono ai metodi di navigazione esistenti nel componente <xref:System.Windows.Forms.BindingSource>.  Per ulteriori informazioni, vedere [Procedura: esplorare i dati con il controllo BindingNavigator Windows Form](../../../../docs/framework/winforms/controls/how-to-navigate-data-with-the-windows-forms-bindingnavigator-control.md).  
  
## Vedere anche  
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.BindingNavigator>   
 [Cenni preliminari sul componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component-overview.md)   
 [Controllo BindingNavigator](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)   
 [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Controlli da utilizzare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [Procedura: associare un controllo Windows Form a un tipo](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)   
 [Procedura: riflettere gli aggiornamenti dell'origine dati in un controllo Windows Form con BindingSource](../../../../docs/framework/winforms/controls/reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)