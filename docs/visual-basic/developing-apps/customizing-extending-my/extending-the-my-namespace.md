---
title: "Extending the My Namespace in Visual Basic | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AddingMyExtensions"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My namespace, customizing"
  - "My namespace"
  - "My namespace, extending"
ms.assetid: 808e8617-b01c-4135-8b21-babe87389e8e
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Extending the My Namespace in Visual Basic
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Lo spazio dei nomi `My` in Visual Basic espone proprietà e metodi che consentono di sfruttare facilmente la potenza di .NET Framework.  Lo spazio dei nomi `My` semplifica problemi di programmazione comuni, spesso riducendo un'attività difficile a una sola riga di codice.  Inoltre, lo spazio dei nomi `My` è completamente estensibile così da rendere possibile la personalizzazione del comportamento di `My` e l'aggiunta di servizi nuovi alla gerarchia per adattarsi alle necessità specifiche dell'applicazione.  In questo argomento viene indicato come personalizzare i membri esistenti dello spazio dei nomi `My` e come aggiungere le proprie classi personalizzate allo spazio dei nomi `My`.  
  
 **Sommario degli argomenti**  
  
-   [Personalizzazione dei membri esistenti dello spazio dei nomi My](#customizing)  
  
-   [Aggiunta di membri agli oggetti My](#addingtoobjects)  
  
-   [Aggiunta di oggetti personalizzati allo spazio dei nomi My](#addingcustom)  
  
-   [Aggiunta dei membri allo spazio dei nomi My](#addingtonamespace)  
  
-   [Aggiunta di eventi agli oggetti My personalizzati](#addingevents)  
  
-   [Indicazioni per la progettazione](#design)  
  
-   [Progettazione delle librerie di classi per My](#designing)  
  
-   [Assemblaggio e distribuzione delle estensioni](#packaging)  
  
##  <a name="customizing"></a> Personalizzazione dei membri esistenti dello spazio dei nomi My  
 Lo spazio dei nomi `My` in Visual Basic espone di frequente le informazioni utilizzate sull'applicazione, sul computer e così via.  Per l'elenco completo degli oggetti nello spazio dei nomi `My`, vedere [My Reference](../../../visual-basic/language-reference/keywords/my-reference.md).  Potrebbe essere necessario personalizzare i membri esistenti dello spazio dei nomi `My` in modo da corrispondere meglio alle necessità dell'applicazione.  Qualsiasi proprietà di un oggetto nello spazio dei nomi `My` che non sia di sola lettura può essere impostata su un valore personalizzato.  
  
 Si supponga, ad esempio, che l'oggetto `My.User` venga utilizzato di frequente per accedere al contesto di sicurezza corrente per l'utente che esegue l'applicazione.  L'azienda invece usa un oggetto utente personalizzato per esporre le informazioni aggiuntive e le funzionalità per gli utenti all'interno dell'azienda.  In questo scenario, è possibile sostituire il valore predefinito della proprietà `My.User.CurrentPrincipal` con un'istanza del proprio oggetto principale personalizzato, come indicato nell'esempio seguente.  
  
 [!code-vb[VbVbcnExtendingMy#1](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_1.vb)]  
  
 L'impostazione della proprietà `CurrentPrincipal` sull'oggetto `My.User` modifica l'identità sotto la quale viene eseguita l'applicazione.  L'oggetto `My.User`, a sua volta, restituisce le informazioni sull'utente appena specificato.  
  
##  <a name="addingtoobjects"></a> Aggiunta di membri agli oggetti My  
 I tipi restituiti da `My.Application` e `My.Computer` sono definiti come classi `Partial`.  Pertanto, è possibile estendere gli oggetti `My.Application` e `My.Computer` creando una classe `Partial` denominata `MyApplication` o `MyComputer`.  La classe non può essere `Private`.  Se si specifica la classe come parte dello spazio dei nomi `My`, è possibile aggiungere le proprietà e i metodi che saranno inclusi con gli oggetti `My.Application` o `My.Computer`.  
  
 Nell'esempio riportato di seguito viene aggiunta una proprietà denominata `DnsServerIPAddresses` all'oggetto `My.Computer`:  
  
 [!code-vb[VbVbcnExtendingMy#2](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_2.vb)]  
  
##  <a name="addingcustom"></a> Aggiunta di oggetti personalizzati allo spazio dei nomi My  
 Sebbene lo spazio dei nomi `My` fornisca soluzioni per molte attività di programmazione comuni, alcune attività potrebbero non essere incluse nello spazio dei nomi `My`.  Ad esempio, quando l'applicazione accede a servizi directory personalizzati per i dati dell'utente o utilizza assembly che non sono installati per impostazione predefinita con Visual Basic.  È possibile estendere lo spazio dei nomi `My` in modo da includere soluzioni personalizzate alle attività comuni specifiche all'ambiente.  Lo spazio dei nomi `My` può essere facilmente esteso in modo da aggiungere membri nuovi per soddisfare le necessità crescenti dell'applicazione.  Inoltre, è possibile distribuire le estensioni dello spazio dei nomi `My` agli altri sviluppatori come modello di Visual Basic.  
  
###  <a name="addingtonamespace"></a> Aggiunta dei membri allo spazio dei nomi My  
 Dal momento che `My` è come qualsiasi altro spazio dei nomi, è possibile aggiungervi le proprietà di livello superiore semplicemente aggiungendo un modulo e specificando uno `Namespace` di `My`.  Annotare il modulo con l'attributo `HideModuleName` come indicato nell'esempio seguente.  L'attributo `HideModuleName` assicura che il nome del modulo non venga visualizzato in IntelliSense quando visualizza i membri dello spazio dei nomi `My`.  
  
 [!code-vb[VbVbcnExtendingMy#3](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_3.vb)]  
  
 Per aggiungere membri allo spazio dei nomi `My`, aggiungere le proprietà al modulo secondo le necessità.  Per ogni proprietà aggiunta allo spazio dei nomi `My`, aggiungere un campo privato di tipo `ThreadSafeObjectProvider(Of T)`, dove il tipo è il tipo restituito dalla proprietà personalizzata.  Questo campo è utilizzato per creare istanze di oggetti thread\-safe che devono essere restituite dalla proprietà chiamando il metodo `GetInstance`.  Di conseguenza, ogni thread che accede alla proprietà estesa riceve la propria istanza del tipo restituito.  Nell'esempio seguente viene aggiunta la proprietà `SampleExtension` di tipo `SampleExtension` allo spazio dei nomi `My`.  
  
 [!code-vb[VbVbcnExtendingMy#4](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_4.vb)]  
  
##  <a name="addingevents"></a> Aggiunta di eventi agli oggetti My personalizzati  
 È possibile utilizzare l'oggetto `My.Application` per esporre eventi per gli oggetti `My` personalizzati estendendo la classe parziale `MyApplication` nello spazio dei nomi `My`.  Per i progetti basati su Windows, è possibile fare doppio clic sul nodo **Progetto** in **Esplora soluzioni**.  In **Progettazione progetti** di Visual Basic, fare clic sulla scheda `Application` e quindi sul pulsante `View Application Events`.  Verrà creato un nuovo file denominato ApplicationEvents.vb  contenente il codice seguente per l'estensione della classe `MyApplication`.  
  
 [!code-vb[VbVbcnExtendingMy#5](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_5.vb)]  
  
 È possibile aggiungere i gestori eventi per gli oggetti `My` personalizzati aggiungendo i gestori eventi personalizzati alla classe `MyApplication`.  Gli eventi personalizzati consentono di aggiungere il codice che verrà eseguito quando un gestore eventi viene aggiunto, rimosso o generato.  Si noti che il codice `AddHandler` per un evento personalizzato viene eseguito solo se il codice viene aggiunto da un utente per gestire l'evento.  Ad esempio, si consideri che l'oggetto `SampleExtension` della sezione precedente abbia un evento `Load` per il quale si desidera aggiungere un gestore eventi personalizzato.  L'esempio di codice seguente mostra un gestore eventi personalizzato denominato `SampleExtensionLoad` che verrà richiamato quando si verifica l'evento `My.SampleExtension.Load`.  Quando il codice viene aggiunto per gestire il nuovo evento `My.SampleExtensionLoad`, viene eseguita la parte `AddHandler` di questo codice dell'evento personalizzato.  Il metodo `MyApplication_SampleExtensionLoad` è incluso nell'esempio di codice per mostrare come un gestore eventi gestisca l'evento `My.SampleExtensionLoad`.  Si noti che l'evento `SampleExtensionLoad` sarà disponibile quando si seleziona l'opzione **Eventi applicazioni** nell'elenco a discesa di sinistra sopra l'editor del codice quando si modifica il file ApplicationEvents.vb.  
  
 [!code-vb[VbVbcnExtendingMy#6](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_6.vb)]  
  
##  <a name="design"></a> Indicazioni per la progettazione  
 Quando si sviluppano estensioni allo spazio dei nomi `My`, utilizzare le linee guida seguenti per consentire di minimizzare i costi di manutenzione dei componenti di estensione.  
  
-   **Includere solo la logica dell'estensione.** Nella logica compresa nell'estensione dello spazio dei nomi `My` deve essere incluso solo il codice necessario per esporre la funzionalità richiesta nello spazio dei nomi `My`.  Poiché l'estensione risiederà nei progetti utente come codice sorgente, aggiornando il componente di estensione si incorre in costi di manutenzione elevati che dovrebbero essere evitati, se possibile.  
  
-   **Minimizzare le ipotesi di progetto.** Quando si creano le estensioni dello spazio dei nomi `My`, è opportuno non presupporre un insieme di riferimenti, importazioni a livello di progetto o impostazioni specifiche del compilatore \(ad esempio, l'oggetto `Option Strict` disattivato\).  Minimizzare, invece, le dipendenze e qualificare in modo completo ogni tipo di riferimento utilizzando la parola chiave `Global`.  Assicurarsi inoltre che l'estensione venga compilata con `Option Strict` attivato per ridurre gli errori nell'estensione.  
  
-   **Isolare il codice dell'estensione.** Inserendo il codice in un singolo file è possibile distribuire facilmente l'estensione come un modello di elemento di Visual Studio.  Per ulteriori informazioni, vedere "Assemblaggio e distribuzione delle estensioni" più avanti in questo argomento.  Anche inserendo tutto il codice di estensione dello spazio dei nomi `My` in un singolo file o in una cartella separata si semplifica il reperimento dell'estensione dello spazio dei nomi `My` da parte degli utenti.  
  
##  <a name="designing"></a> Progettazione delle librerie di classi per My  
 Come per la maggior parte dei modelli a oggetti, solo alcuni modelli di progettazione funzionano nello spazio dei nomi `My`.  Quando si progetta un'estensione allo spazio dei nomi `My`, considerare i principi seguenti:  
  
-   **Metodi senza stato.** I metodi nello spazio dei nomi `My` devono fornire una soluzione completa a un'attività specifica.  Assicurarsi che i valori di parametro passati al metodo forniscano tutto l'input richiesto per completare la particolare attività.  Evitare di creare metodi che si basano sullo stato precedente, ad esempio l'apertura di connessioni alle risorse.  
  
-   **Istanze globali.** L'unico stato gestito nello spazio dei nomi `My` è globale per il progetto.  Ad esempio, `My.Application.Info` incapsula lo stato condiviso in tutta l'applicazione.  
  
-   **Semplici tipi di parametro.** Semplificare le operazioni, evitando tipi di parametro complessi.  Creare invece metodi che non utilizzino input di parametri o che utilizzino tipi di input semplici, ad esempio stringhe, tipi primitivi e così via.  
  
-   **Metodi factory.** Creare l'istanza di alcuni tipi è un'operazione effettivamente difficile.  Fornendo i metodi factory come estensioni allo spazio dei nomi `My` è possibile individuare più facilmente e utilizzare tipi che rientrano in questa categoria.  Un esempio di un metodo factory che funziona bene è `My.Computer.FileSystem.OpenTextFileReader`.  Ci sono molti tipi di flusso disponibili in .NET Framework.  Specificando file di testo in modo esplicito, `OpenTextFileReader` consente all'utente di capire quale flusso utilizzare.  
  
 Queste linee guida non precludono i principi di progettazione generali per le librerie di classi.  Piuttosto, sono raccomandazioni ottimizzate per gli sviluppatori che utilizzano Visual Basic e lo spazio dei nomi `My`.  Per i principi di progettazione generali per la creazione di librerie di classi, vedere [Linee guida](../Topic/Framework%20Design%20Guidelines.md).  
  
##  <a name="packaging"></a> Assemblaggio e distribuzione delle estensioni  
 È possibile includere le estensioni dello spazio dei nomi `My` in un modello di progetto di Visual Studio o comprimere le estensioni e distribuirle come modello di elemento di Visual Studio.  Quando si comprimono le estensioni dello spazio dei nomi `My` come modello di elemento di Visual Studio, è possibile sfruttare le funzionalità aggiuntive fornite da Visual Basic.  Queste funzionalità consentono di includere un'estensione quando un progetto fa riferimento a un particolare assembly o consente agli utenti di aggiungere in modo esplicito l'estensione dello spazio dei nomi `My` utilizzando la pagina **Estensioni My** di Progettazione progetti di Visual Basic.  
  
 Per le informazioni dettagliate sulla distribuzione delle estensioni dello spazio dei nomi `My`, vedere [Packaging and Deploying Custom My Extensions](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md).  
  
## Vedere anche  
 [Packaging and Deploying Custom My Extensions](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)   
 [Extending the Visual Basic Application Model](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [Customizing Which Objects are Available in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [Pagina Estensioni My, Progettazione progetti](/visual-studio/ide/reference/my-extensions-page-project-designer-visual-basic)   
 [Pagina Applicazione, Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)   
 [Partial](../../../visual-basic/language-reference/modifiers/partial.md)