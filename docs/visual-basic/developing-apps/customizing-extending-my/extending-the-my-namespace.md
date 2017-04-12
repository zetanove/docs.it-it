---
title: Estensione di My Namespace in Visual Basic | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.AddingMyExtensions
dev_langs:
- VB
helpviewer_keywords:
- My namespace, customizing
- My namespace
- My namespace, extending
ms.assetid: 808e8617-b01c-4135-8b21-babe87389e8e
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1d1e957536f35b81a9672994c9d4d261afb764ea
ms.lasthandoff: 03/13/2017

---
# <a name="extending-the-my-namespace-in-visual-basic"></a>Estensione dello spazio dei nomi My in Visual Basic
Il `My` spazio dei nomi in Visual Basic espone proprietà e metodi che consentono di sfruttare facilmente la potenza di .NET Framework. Il `My` dello spazio dei nomi semplifica problemi di programmazione comuni, spesso riducendo un'attività difficile a una singola riga di codice. Inoltre, il `My` spazio dei nomi è completamente estensibile in modo che sia possibile personalizzare il comportamento di `My` e aggiungere nuovi servizi alla gerarchia per adattarsi alle esigenze specifiche dell'applicazione. Questo argomento vengono illustrati entrambi come personalizzare i membri esistenti del `My` dello spazio dei nomi e come aggiungere le proprie classi personalizzate per il `My` dello spazio dei nomi.  
  
 **Sommario degli argomenti**  
  
-   [Personalizzazione esistenti membri personale Namespace](#customizing)  
  
-   [Aggiunta di membri a oggetti My](#addingtoobjects)  
  
-   [Aggiunta di oggetti personalizzati per il mio Namespace](#addingcustom)  
  
-   [Aggiunta di membri per il mio Namespace](#addingtonamespace)  
  
-   [Aggiunta di eventi agli oggetti My personalizzati](#addingevents)  
  
-   [Linee guida di progettazione](#design)  
  
-   [Progettazione di librerie di classi per My](#designing)  
  
-   [Assemblaggio e distribuzione delle estensioni](#packaging)  
  
##  <a name="customizing"></a>Personalizzazione esistenti membri personale Namespace  
 Il `My` dello spazio dei nomi in Visual Basic espone utilizzati informazioni sull'applicazione, il computer e così via. Per un elenco completo degli oggetti di `My` spazio dei nomi, vedere [My Reference](../../../visual-basic/language-reference/keywords/my-reference.md). Potrebbe essere necessario personalizzare i membri esistenti del `My` dello spazio dei nomi in modo da corrispondere meglio le esigenze dell'applicazione. Qualsiasi proprietà di un oggetto di `My` spazio dei nomi che non è di sola lettura può essere impostata su un valore personalizzato.  
  
 Ad esempio, si supponga che si utilizza spesso il `My.User` oggetto per accedere al contesto di sicurezza corrente per l'utente che esegue l'applicazione. Tuttavia, la società utilizza un oggetto utente personalizzato per esporre ulteriori informazioni e funzionalità per gli utenti all'interno della società. In questo scenario, è possibile sostituire il valore predefinito di `My.User.CurrentPrincipal` proprietà con un'istanza di un oggetto principale personalizzato, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbcnExtendingMy n.&1;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_1.vb)]  
  
 L'impostazione di `CurrentPrincipal` proprietà di `My.User` oggetto cambia l'identità con cui viene eseguito l'applicazione. Il `My.User` , a sua volta, restituisce informazioni sull'utente appena specificato.  
  
##  <a name="addingtoobjects"></a>Aggiunta di membri a oggetti My  
 I tipi restituiti da `My.Application` e `My.Computer` sono definite come `Partial` classi. Pertanto, è possibile estendere il `My.Application` e `My.Computer` oggetti mediante la creazione di un `Partial` classe denominata `MyApplication` o `MyComputer`. La classe non può essere un `Private` (classe). Se si specifica la classe come parte del `My` spazio dei nomi, è possibile aggiungere proprietà e metodi che verranno inclusi le `My.Application` o `My.Computer` oggetti.  
  
 Ad esempio, nell'esempio seguente aggiunge una proprietà denominata `DnsServerIPAddresses` per il `My.Computer` oggetto.  
  
 [!code-vb[VbVbcnExtendingMy n.&2;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_2.vb)]  
  
##  <a name="addingcustom"></a>Aggiunta di oggetti personalizzati per il mio Namespace  
 Sebbene il `My` dello spazio dei nomi fornisce soluzioni per molte attività di programmazione comuni, alcune attività potrebbero che il `My` dello spazio dei nomi non viene risolto. Ad esempio, l'applicazione potrebbe accedere ai servizi di directory personalizzata per i dati utente o l'applicazione può utilizzare gli assembly che non sono installati per impostazione predefinita con Visual Basic. È possibile estendere il `My` dello spazio dei nomi da includere soluzioni personalizzate per le attività comuni che sono specifiche per l'ambiente. Il `My` dello spazio dei nomi può essere facilmente esteso per aggiungere nuovi membri per soddisfare le crescenti esigenze dell'applicazione. Inoltre, è possibile distribuire il `My` dello spazio dei nomi estensioni ad altri sviluppatori come modello di Visual Basic.  
  
###  <a name="addingtonamespace"></a>Aggiunta di membri per il mio Namespace  
 Poiché `My` è uno spazio dei nomi come qualsiasi altro spazio dei nomi, è possibile aggiungere proprietà di primo livello a esso semplicemente aggiungendo un modulo e specificando un `Namespace` di `My`. Annotare il modulo con il `HideModuleName` attributo come illustrato nell'esempio seguente. Il `HideModuleName` attributo assicura che il nome del modulo non venga visualizzato in IntelliSense quando visualizza i membri del `My` dello spazio dei nomi.  
  
 [!code-vb[VbVbcnExtendingMy n.&3;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_3.vb)]  
  
 Per aggiungere i membri di `My` dello spazio dei nomi, aggiungere le proprietà necessarie per il modulo. Per ogni proprietà aggiunta per il `My` spazio dei nomi, aggiungere un campo privato di tipo `ThreadSafeObjectProvider(Of T)`, dove il tipo è il tipo restituito dalla proprietà personalizzata. Questo campo viene utilizzato per creare istanze di oggetti thread-safe che devono essere restituite dalla proprietà chiamando il `GetInstance` metodo. Di conseguenza, ogni thread che accede alla proprietà estesa riceve la propria istanza del tipo restituito. Nell'esempio seguente aggiunge una proprietà denominata `SampleExtension` che è di tipo `SampleExtension` per il `My` dello spazio dei nomi:  
  
 [!code-vb[VbVbcnExtendingMy n.&4;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_4.vb)]  
  
##  <a name="addingevents"></a>Aggiunta di eventi agli oggetti My personalizzati  
 È possibile utilizzare il `My.Application` oggetto per esporre gli eventi per personalizzato `My` oggetti estendendo il `MyApplication` classe parziale nel `My` dello spazio dei nomi. Per i progetti basati su Windows, è possibile fare doppio clic il **progetto** nodo per il progetto in **Esplora**. In Visual Basic **progettazione**, fare clic su di `Application` scheda e quindi fare clic sul `View Application Events` pulsante. Verrà creato un nuovo file denominato ApplicationEvents. vb. Contiene il codice seguente per estendere la `MyApplication` classe.  
  
 [!code-vb[VbVbcnExtendingMy n.&5;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_5.vb)]  
  
 È possibile aggiungere gestori eventi per personalizzato `My` oggetti mediante l'aggiunta di gestori di eventi personalizzati per la `MyApplication` classe. Eventi personalizzati consentono di aggiungere il codice che verrà eseguito un gestore eventi viene aggiunto, rimosso, oppure viene generato l'evento. Si noti che il `AddHandler` di codice per un evento personalizzato viene eseguito solo se il codice viene aggiunto da un utente di gestire l'evento. Ad esempio, si consideri che la `SampleExtension` oggetto nella sezione precedente ha un `Load` evento che si desidera aggiungere un gestore di eventi personalizzati per. Esempio di codice seguente viene illustrato un gestore eventi personalizzato denominato `SampleExtensionLoad` che sarà richiamato quando il `My.SampleExtension.Load` si verifica l'evento. Quando viene aggiunto codice per gestire il nuovo `My.SampleExtensionLoad` evento, il `AddHandler` viene eseguita parte del codice evento personalizzato. Il `MyApplication_SampleExtensionLoad` metodo è incluso nell'esempio di codice per visualizzare un esempio di un gestore eventi che gestisce il `My.SampleExtensionLoad` evento. Si noti che il `SampleExtensionLoad` eventi saranno disponibili quando si seleziona il **eventi applicazioni** opzione nell'elenco a discesa a sinistra sopra l'Editor del codice quando si modifica il file ApplicationEvents. vb.  
  
 [!code-vb[6 VbVbcnExtendingMy](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_6.vb)]  
  
##  <a name="design"></a>Linee guida di progettazione  
 Quando si sviluppano estensioni per il `My` dello spazio dei nomi, utilizzare le linee guida seguenti per ridurre al minimo i costi di manutenzione dei componenti di estensione.  
  
-   **Includere solo la logica di estensione.** La logica del `My` estensione dello spazio dei nomi deve includere solo il codice necessario per esporre la funzionalità richiesta nel `My` dello spazio dei nomi. Poiché l'estensione risiederà nei progetti utente come codice sorgente, l'aggiornamento del componente di estensione comporta un costo di manutenzione elevata e deve essere evitato se possibile.  
  
-   **Ridurre al minimo ipotesi di progetto.** Quando si creano le estensioni di `My` spazio dei nomi, non presupporre che un set di riferimenti, le importazioni a livello di progetto o le impostazioni del compilatore specifici (ad esempio, `Option Strict` off). Al contrario, ridurre al minimo le dipendenze e tutti i riferimenti di tipo completi utilizzando il `Global` (parola chiave). Inoltre, assicurarsi che l'estensione venga compilata con `Option Strict` per ridurre al minimo gli errori nell'estensione.  
  
-   **Isolare il codice di estensione.** Inserire il codice in un singolo file l'estensione rende facilmente distribuibile come modello di elemento Visual Studio. Per ulteriori informazioni, vedere "Creazione di pacchetti e distribuzione delle estensioni" più avanti in questo argomento. Inserimento di tutti i `My` codice di estensione dello spazio dei nomi in un singolo file o una cartella distinta in un progetto verrà inoltre consentire agli utenti di individuare il `My` estensione dello spazio dei nomi.  
  
##  <a name="designing"></a>Progettazione di librerie di classi per My  
 Come avviene con la maggior parte dei modelli a oggetti, alcuni modelli di progettazione funzionano in modo efficiente il `My` dello spazio dei nomi e gli altri non. Quando si progetta un'estensione per il `My` dello spazio dei nomi, considerare i principi seguenti:  
  
-   **Metodi senza stati.** Metodi di `My` dello spazio dei nomi deve fornire una soluzione completa per un'attività specifica. Assicurarsi che i valori dei parametri passati al metodo forniscano tutto l'input necessario per completare l'attività particolare. Evitare di creare metodi che si basano sullo stato precedente, ad esempio le connessioni aperte alle risorse.  
  
-   **Istanze globale.** L'unico stato che viene mantenuto il `My` spazio dei nomi è globale per il progetto. Ad esempio, `My.Application.Info` incapsula lo stato condiviso in tutta l'applicazione.  
  
-   **Tipi di parametro semplici.** Semplificare le operazioni, evitando di tipi di parametri complessi. Creare invece metodi che non utilizzino alcun parametro di input o che accettano tipi di input semplici, ad esempio stringhe, tipi primitivi e così via.  
  
-   **Metodi factory.** Alcuni tipi sono necessariamente difficile creare un'istanza. Fornendo i metodi factory come estensioni per il `My` dello spazio dei nomi consente di individuare più facilmente e utilizzare tipi che rientrano in questa categoria. Un esempio di un metodo factory che funziona bene è `My.Computer.FileSystem.OpenTextFileReader`. Sono disponibili molti tipi di flusso in .NET Framework. Specificando in particolare, i file di testo di `OpenTextFileReader` consente all'utente di capire quale flusso da utilizzare.  
  
 Queste linee guida non precludono i principi di progettazione generali per le librerie di classi. Piuttosto, sono raccomandazioni ottimizzate per gli sviluppatori che utilizzano Visual Basic e `My` dello spazio dei nomi. Per i principi di progettazione generali per la creazione di librerie di classi, vedere [Framework Design Guidelines](http://msdn.microsoft.com/library/5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b).  
  
##  <a name="packaging"></a>Assemblaggio e distribuzione delle estensioni  
 È possibile includere `My` estensioni dello spazio dei nomi in un modello di progetto di Visual Studio, oppure è possano comprimere le estensioni e distribuirli come modello di elemento Visual Studio. Quando crei il pacchetto di `My` estensioni dello spazio dei nomi come modello di elemento Visual Studio, è possibile sfruttare le funzionalità aggiuntive fornite da Visual Basic. Queste funzionalità consentono di includere un'estensione quando un progetto fa riferimento a un particolare assembly o consentire agli utenti di aggiungere in modo esplicito il `My` estensione dello spazio dei nomi utilizzando il **estensioni My** pagina della finestra di progettazione di progetto Visual Basic.  
  
 Per informazioni dettagliate su come distribuire `My` estensioni dello spazio dei nomi, vedere [pacchetti e distribuzione delle estensioni My personalizzate](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Assemblaggio e distribuzione delle estensioni My personalizzate](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)   
 [Estensione del modello di applicazione Visual Basic](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [Personalizzazione degli oggetti sono disponibili in My](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [Pagina Estensioni My, Progettazione progetti](https://docs.microsoft.com/visualstudio/ide/reference/my-extensions-page-project-designer-visual-basic)   
 [Application Page, Project Designer (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)  (Pagina Applicazione, Creazione progetti (Visual Basic))  
 [Partial](../../../visual-basic/language-reference/modifiers/partial.md)
