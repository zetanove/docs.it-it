---
title: "Procedura dettagliata: hosting di contenuto WPF in Win32 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "hosting di contenuto WPF nella finestra Win32"
ms.assetid: 38ce284a-4303-46dd-b699-c9365b22a7dc
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Procedura dettagliata: hosting di contenuto WPF in Win32
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce un ambiente completo per la creazione di applicazioni.  Tuttavia, se si dispone di una grande quantità di codice [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)], può essere più efficace aggiungere funzionalità [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] all'applicazione anziché riscrivere il codice originale.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce un meccanismo semplice per l'hosting di contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
 Questa esercitazione descrive come scrivere un'applicazione di esempio, [Esempio di hosting di un contenuto Windows Presentation Foundation in una finestra Win32](http://go.microsoft.com/fwlink/?LinkID=160004), che ospita contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  L'esempio può essere esteso a qualsiasi finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Dal momento che implica l'uso combinato di codice gestito e non gestito, l'applicazione viene scritta in [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)].  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="requirements"></a>   
## Requisiti  
 Questa esercitazione presuppone una conoscenza di base della programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Per un'introduzione alla programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Guida introduttiva](../../../../docs/framework/wpf/getting-started/index.md).  Per un'introduzione alla programmazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], fare riferimento a uno dei numerosi manuali sull'argomento, in particolare *Programmare Windows* di Charles Petzold.  
  
 Poiché l'esempio che accompagna questa esercitazione è implementato in [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)], questa esercitazione presuppone una buona conoscenza dell'uso di [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] per la programmazione dell'[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] oltre alla conoscenza della programmazione in codice gestito.  La conoscenza di [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] è utile, ma non essenziale.  
  
> [!NOTE]
>  Questa esercitazione include numerosi esempi di codice relativi all'esempio associato.  Tuttavia, per una questione di leggibilità, il codice di esempio completo non è compreso.  Per il codice di esempio completo, vedere [Esempio di hosting di un contenuto Windows Presentation Foundation in una finestra Win32](http://go.microsoft.com/fwlink/?LinkID=160004).  
  
<a name="basic_procedure"></a>   
## Procedura di base  
 Questa sezione illustra la procedura di base da usare per ospitare contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Le sezioni rimanenti illustrano in dettaglio i vari passaggi.  
  
 La chiave per ospitare contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] è la classe <xref:System.Windows.Interop.HwndSource>.  Questa classe esegue il wrapping del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], consentendo di incorporarlo nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] come finestra figlio.  Nell'approccio che segue, [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono combinati in un'unica applicazione.  
  
1.  Implementare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] come classe gestita.  
  
2.  Implementare un'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] con [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)].  Se si parte da un'applicazione esistente e da codice [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] non gestito, in genere è possibile abilitarla a chiamare codice gestito modificando le impostazioni del progetto e includendo il flag del compilatore `/clr`.  
  
3.  Impostare il modello di threading su apartment a thread singolo \(STA\).  
  
4.  Gestire la notifica [WM\_CREATE](http://msdn.microsoft.com/library/ms632619.aspx) nella procedura di finestra ed eseguire le operazioni seguenti:  
  
    1.  Creare un nuovo oggetto <xref:System.Windows.Interop.HwndSource> con la finestra padre come parametro `parent`.  
  
    2.  Creare un'istanza della classe di contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
    3.  Assegnare all'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] un riferimento alla proprietà <xref:System.Windows.Interop.HwndSource.RootVisual%2A> di <xref:System.Windows.Interop.HwndSource>.  
  
    4.  Ottenere HWND per il contenuto.  La proprietà <xref:System.Windows.Interop.HwndSource.Handle%2A> dell'oggetto <xref:System.Windows.Interop.HwndSource> contiene l'handle di finestra \(HWND\).  Per ottenere un HWND utilizzabile nella parte non gestita dell'applicazione, eseguire il cast di `Handle.ToPointer()` a un HWND.  
  
5.  Implementare una classe gestita contenente un campo statico con un riferimento al contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Questa classe consente di ottenere un riferimento al contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dal codice [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
6.  Assegnare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] al campo statico.  
  
7.  Ricevere notifiche dal contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] associando un gestore a uno o più eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
8.  Comunicare con il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usando il riferimento archiviato nel campo statico per impostare le proprietà ed eseguire altre operazioni.  
  
> [!NOTE]
>  È anche possibile usare [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] per implementare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Tuttavia, sarà necessario compilarlo separatamente come [!INCLUDE[TLA#tla_dll](../../../../includes/tlasharptla-dll-md.md)] e fare riferimento a tale [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] dall'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  La parte restante della procedura è simile a quella appena descritta.  
  
<a name="implementing_the_application"></a>   
## Implementazione dell'applicazione host  
 Questa sezione descrive come ospitare contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in un'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] di base.  Il contenuto viene implementato in [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] come classe gestita.  In gran parte si tratta di semplice programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Gli aspetti principali dell'implementazione del contenuto vengono illustrati in [Implementazione del contenuto WPF](#implementing_the_wpf_page).  
  
<a name="autoNestedSectionsOUTLINE1"></a>   
-   [Applicazione di base](#the_basic_application)  
  
-   [Hosting del contenuto WPF](#hosting_the_wpf_page)  
  
-   [Riferimento al contenuto WPF](#holding_a_reference)  
  
-   [Comunicazione con il contenuto WPF](#communicating_with_the_page)  
  
<a name="the_basic_application"></a>   
### Applicazione di base  
 Il punto di partenza per l'applicazione host consisteva nella creazione di un modello in [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)].  
  
1.  Aprire [!INCLUDE[TLA2#tla_visualstu2005](../../../../includes/tla2sharptla-visualstu2005-md.md)] e scegliere **Nuovo progetto** dal menu **File**.  
  
2.  Selezionare **Win32** dall'elenco dei tipi di progetto [!INCLUDE[TLA2#tla_visualcpp](../../../../includes/tla2sharptla-visualcpp-md.md)].  Se il linguaggio predefinito non è [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)], questi tipi di progetto sono disponibili in **Altri linguaggi**.  
  
3.  Selezionare un modello **Progetto Win32**, assegnare un nome al progetto e fare clic su **OK** per avviare la **Creazione guidata applicazione Win32**.  
  
4.  Accettare impostazioni predefinite della procedura guidata e fare clic su **Fine** per avviare il progetto.  
  
 Il modello crea un'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] di base, che include:  
  
-   Un punto di ingresso per l'applicazione.  
  
-   Una finestra, con una procedura di finestra associata \(WndProc\).  
  
-   Un menu dotato di intestazioni **File** e **?**.  Il menu **File** contiene un elemento **Esci** che consente di chiudere l'applicazione.  Il menu **?** contiene un elemento **Informazioni su** che consente di avviare una finestra di dialogo semplice.  
  
 Prima di iniziare a scrivere il codice per ospitare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario apportare due modifiche al modello di base.  
  
 La prima consiste nel compilare il progetto come codice gestito.  Per impostazione predefinita, il progetto viene compilato come codice non gestito.  Tuttavia, dal momento che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è implementato in codice gestito, il progetto deve essere compilato di conseguenza.  
  
1.  Fare clic con il pulsante destro del mouse sul nome del progetto in **Esplora soluzioni** e scegliere**Proprietà** dal menu contestuale per avviare la finestra di dialogo **Pagine delle proprietà**.  
  
2.  Nella visualizzazione albero nel riquadro di sinistra selezionare **Proprietà di configurazione**.  
  
3.  Selezionare il supporto **Common Language Runtime** nell'elenco **Impostazioni predefinite progetto** nel riquadro di destra.  
  
4.  Selezionare **Supporto Common Language Runtime Support \(\/clr\)** dall'elenco a discesa.  
  
> [!NOTE]
>  Questo flag del compilatore consente di usare codice gestito nell'applicazione, ma il codice non gestito verrà comunque compilato come in precedenza.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa il modello di threading STA \(apartment a thread singolo\).  Per il funzionamento corretto con il codice del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario impostare il modello di threading dell'applicazione su STA applicando un attributo al punto di ingresso.  
  
 [!code-cpp[Win32HostingWPFPage#WinMain](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#winmain)]  
  
<a name="hosting_the_wpf_page"></a>   
### Hosting del contenuto WPF  
 Il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è una semplice applicazione di immissione dell'indirizzo.  È costituito da diversi controlli <xref:System.Windows.Controls.TextBox> nei quali immettere nome utente, indirizzo e così via.  Sono presenti anche due controlli <xref:System.Windows.Controls.Button>, **OK** e **Cancel**.  Facendo clic su **OK**, il gestore eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click> del pulsante raccoglie i dati dai controlli <xref:System.Windows.Controls.TextBox>, li assegna alle proprietà corrispondenti e genera un evento personalizzato, `OnButtonClicked`.  Facendo clic su **Cancel**, il gestore genera semplicemente `OnButtonClicked`.  L'oggetto argomento dell'evento per `OnButtonClicked` contiene un campo booleano che indica il pulsante scelto.  
  
 Il codice per ospitare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene implementato in un gestore per la notifica [WM\_CREATE](http://msdn.microsoft.com/library/ms632619.aspx) nella finestra host.  
  
 [!code-cpp[Win32HostingWPFPage#WMCreate](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcreate)]  
  
 Il metodo `GetHwnd` acquisisce informazioni sulla dimensione e posizione oltre all'handle della finestra padre e restituisce l'handle della finestra del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitato.  
  
> [!NOTE]
>  Non è possibile usare una direttiva `#using` per lo spazio dei nomi `System::Windows::Interop`,  in quanto si creerebbe un conflitto di nomi tra la struttura <xref:System.Windows.Interop.MSG> nello spazio dei nomi e la struttura MSG dichiarata in winuser.h.  Al contrario, occorre usare nomi completi per accedere al contenuto dello spazio dei nomi.  
  
 [!code-cpp[Win32HostingWPFPage#GetHwnd](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#gethwnd)]  
  
 Non è possibile ospitare contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] direttamente nella finestra dell'applicazione.  Al contrario, occorre prima creare un oggetto <xref:System.Windows.Interop.HwndSource> per eseguire il wrapping del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Questo oggetto è fondamentalmente una finestra progettata per ospitare un contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per ospitare l'oggetto <xref:System.Windows.Interop.HwndSource> nella finestra padre, occorre crearlo come figlio di una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]appartenente all'applicazione.  I parametri del costruttore <xref:System.Windows.Interop.HwndSource> contengono pressappoco le stesse informazioni che verrebbero passate a CreateWindow durante la creazione di una finestra figlio [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
 La fase successiva prevede la creazione di un'istanza dell'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  In questo caso, il contenuto[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene implementato come classe separata, `WPFPage`, usando [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)].  È anche possibile implementare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] mediante [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  A tale scopo, tuttavia, è necessario configurare un progetto separato e compilare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] come [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)].  È possibile aggiungere un riferimento alla [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] nel progetto e usarlo per creare un'istanza del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Per visualizzare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nella finestra figlio, assegnare un riferimento al contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] alla proprietà <xref:System.Windows.Interop.HwndSource.RootVisual%2A> di <xref:System.Windows.Interop.HwndSource>.  
  
 La riga di codice successiva associa un gestore eventi, `WPFButtonClicked`, all'evento `OnButtonClicked` del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Questo gestore viene chiamato quando l'utente fa clic sul pulsante **OK** o **Cancel**.  Vedere [Comunicazione con il contenuto WPF](#communicating_with_the_page) per maggiori informazioni su questo gestore eventi.  
  
 La riga finale del codice illustrata restituisce l'handle della finestra \(HWND\) associato all'oggetto <xref:System.Windows.Interop.HwndSource>.  È possibile usare questo handle dal codice [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] per inviare messaggi alla finestra ospitata, benché questo non avvenga nell'esempio.  L'oggetto <xref:System.Windows.Interop.HwndSource> genera un evento ogni volta che riceve un messaggio.   Per elaborare i messaggi, chiamare il metodo <xref:System.Windows.Interop.HwndSource.AddHook%2A> per associare un gestore di messaggi, quindi elaborare i messaggi in tale gestore.  
  
<a name="holding_a_reference"></a>   
### Riferimento al contenuto WPF  
 Per molte applicazioni si vorrà comunicare con il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in un secondo momento.  Ad esempio, sarà possibile modificare le proprietà del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] o fare in modo che l'oggetto <xref:System.Windows.Interop.HwndSource> ospiti un contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] diverso.  A tale scopo, è necessario un riferimento all'oggetto <xref:System.Windows.Interop.HwndSource> o al contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  L'oggetto <xref:System.Windows.Interop.HwndSource> e il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] associato restano in memoria fino all'eliminazione dell'handle della finestra.  Tuttavia, la variabile assegnata all'oggetto <xref:System.Windows.Interop.HwndSource> uscirà dall'ambito non appena si esce dalla procedura di finestra.  Per gestire questo problema con le applicazioni [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] si usa in genere una variabile statica o globale.  Sfortunatamente, non è possibile assegnare un oggetto gestito ai suddetti tipi di variabili.  È possibile assegnare l'handle della finestra associato all'oggetto <xref:System.Windows.Interop.HwndSource> a una variabile globale o statica, ma ciò non consentirà di accedere all'oggetto in questione.  
  
 La soluzione più semplice a questo problema consiste nell'implementare una classe gestita contenente un insieme di campi statici che a loro volta contengono i riferimenti agli oggetti gestiti ai quali si vuole accedere.  Nell'esempio viene usata la classe `WPFPageHost`, che contiene un riferimento al contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] oltre ai valori iniziali di diverse proprietà, modificabili in un secondo momento dall'utente.  La classe viene definita nell'intestazione.  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageHost](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.h#wpfpagehost)]  
  
 La seconda parte della funzione `GetHwnd` assegna valori ai suddetti campi che verranno usati in un secondo momento, con `myPage` ancora nell'ambito.  
  
<a name="communicating_with_the_page"></a>   
### Comunicazione con il contenuto WPF  
 Esistono due tipi di comunicazione con il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  L'applicazione riceve informazioni dal contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] quando l'utente fa clic sui pulsanti **OK** o **Cancel**.  L'applicazione dispone anche di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] che consente di modificare diverse proprietà del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], ad esempio il colore di sfondo o le dimensioni predefinite del carattere.  
  
 Come indicato in precedenza, quando l'utente fa clic su uno dei pulsanti il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] genera un evento `OnButtonClicked`.  L'applicazione associa un gestore a questo evento per ricevere le notifiche.  Nel caso sia stato scelto il pulsante **OK**, il gestore ottiene le informazioni utente dal contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e le visualizza in un insieme di controlli statici.  
  
 [!code-cpp[Win32HostingWPFPage#WPFButtonClicked](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wpfbuttonclicked)]  
  
 Il gestore riceve un oggetto argomento dell'evento personalizzato dal contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], `MyPageEventArgs`.  La proprietà `IsOK` dell'oggetto è impostata su `true` se il pulsante scelto è **OK**, altrimenti su `false` se il pulsante scelto è **Cancel**.  
  
 Se il pulsante scelto è **OK**, il gestore ottiene un riferimento al contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dalla classe dei contenitori.  Raccoglie quindi le informazioni utente contenute nelle proprietà del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] associate e sa i controlli statici per visualizzare le informazioni nella finestra padre.  Essendo i dati del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sotto forma di stringa gestita, devono essere sottoposti a marshalling per l'uso da parte di un controllo [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Se il pulsante scelto è **Cancel**, il gestore cancella i dati dai controlli statici.  
  
 L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dell'applicazione fornisce un set di pulsanti di opzione che consentono di modificare il colore di sfondo del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e diverse proprietà correlate al tipo di carattere.  Nell'esempio seguente viene illustrato un estratto della procedura di finestra \(WndProc\) dell'applicazione, nonché la gestione dei messaggi tramite la quale è possibile impostare varie proprietà in messaggi diversi, incluso il colore di sfondo.  La parte restante è simile, pertanto non viene illustrata.  Vedere l'esempio completo per i dettagli e il contesto.  
  
 [!code-cpp[Win32HostingWPFPage#WMCommandToBG](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcommandtobg)]  
  
 Per impostare il colore di sfondo, ottenere un riferimento al contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] \(`hostedPage`\) da `WPFPageHost` e impostare la proprietà del colore di sfondo sul colore appropriato.  Nell'esempio vengono usate tre opzioni di colore: il colore originale, verde chiaro o salmone chiaro.  Il colore di sfondo originale viene archiviato come campo statico nella classe `WPFPageHost`.  Per impostare gli altri due colori, creare un nuovo oggetto <xref:System.Windows.Media.SolidColorBrush> e passare al costruttore un valore di colore statico dall'oggetto <xref:System.Windows.Media.Colors>.  
  
<a name="implementing_the_wpf_page"></a>   
## Implementazione della pagina WPF  
 È possibile ospitare e usare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] senza alcuna conoscenza dell'implementazione effettiva.  Se il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fosse stato assemblato in una [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] separata, la compilazione sarebbe potuta avvenire in qualsiasi linguaggio [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)].  Di seguito viene riportata una breve procedura dettagliata relativa all'implementazione [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] usata nell'esempio.  Questa sezione contiene le sottosezioni seguenti.  
  
<a name="autoNestedSectionsOUTLINE2"></a>   
-   [Layout](#page_layout)  
  
-   [Restituzione dei dati alla finestra host](#returning_data_to_window)  
  
-   [Impostazione delle proprietà WPF](#set_page_properties)  
  
<a name="page_layout"></a>   
### Layout  
 Gli elementi [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] nel contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono costituiti da cinque controlli <xref:System.Windows.Controls.TextBox>, dotati di controlli <xref:System.Windows.Controls.Label> associati: Name, Address, City, State e Zip.  Sono presenti anche due controlli <xref:System.Windows.Controls.Button>, **OK** e **Cancel**  
  
 Il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è implementato nella classe `WPFPage`.  Il layout viene gestito mediante un apposito elemento <xref:System.Windows.Controls.Grid>.  La classe eredita da <xref:System.Windows.Controls.Grid>, il che la rende effettivamente l'elemento radice del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Il costruttore del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] misura la larghezza e l'altezza richieste e sulla base di queste adatta le dimensioni di <xref:System.Windows.Controls.Grid>.  Definisce quindi il layout di base creando un set di oggetti <xref:System.Windows.Controls.ColumnDefinition> e <xref:System.Windows.Controls.RowDefinition> e aggiungendoli rispettivamente alle raccolte <xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> e <xref:System.Windows.Controls.Grid.RowDefinitions%2A> di base dell'oggetto <xref:System.Windows.Controls.Grid>.  Viene così definita una griglia di cinque righe e sette colonne, le cui dimensioni sono determinate dal contenuto delle celle.  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorToGridDef](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortogriddef)]  
  
 Successivamente il costruttore aggiunge gli elementi dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] a <xref:System.Windows.Controls.Grid>.  Il primo elemento è il testo del titolo, ovvero un controllo <xref:System.Windows.Controls.Label> centrato nella prima riga della griglia.  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorTitle](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortitle)]  
  
 La riga successiva contiene il controllo <xref:System.Windows.Controls.Label> Name e il controllo <xref:System.Windows.Controls.TextBox> associato.  Dal momento che per ogni coppia etichetta\/casella di testo viene usato lo stesso codice, questo viene collocato in una coppia di metodi privati e usato per tutte e cinque le coppie etichetta\/casella di testo.  I metodi creano il controllo appropriato e chiamano i metodi <xref:System.Windows.Controls.Grid.SetColumn%2A> e <xref:System.Windows.Controls.Grid.SetRow%2A> statici della classe <xref:System.Windows.Controls.Grid> per posizionare i controlli nella cella appropriata.  Una volta creato il controllo, nell'esempio viene chiamato il metodo <xref:System.Windows.Controls.UIElementCollection.Add%2A> sulla proprietà <xref:System.Windows.Controls.Panel.Children%2A> di <xref:System.Windows.Controls.Grid> per aggiungere il controllo alla griglia.  Il codice usato per aggiungere le coppie etichetta\/casella di testo restanti è simile.  Vedere il codice di esempio per i dettagli.  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorName](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorname)]  
  
 D seguito viene riportata l'implementazione dei due metodi:  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCreateHelpers](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagecreatehelpers)]  
  
 Infine, nell'esempio vengono aggiunti i pulsanti **OK** e **Cancel** e viene associato un gestore eventi agli eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click> correlati.  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorButtonsEvents](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorbuttonsevents)]  
  
<a name="returning_data_to_window"></a>   
### Restituzione dei dati alla finestra host  
 Facendo clic su un pulsante, viene generato il rispettivo evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click>.  La finestra host potrebbe semplicemente associare i gestori a questi eventi e ottenere i dati direttamente dai controlli <xref:System.Windows.Controls.TextBox>.  Nell'esempio viene usato un approccio meno diretto.  <xref:System.Windows.Controls.Primitives.ButtonBase.Click> viene gestito all'interno del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e un evento personalizzato `OnButtonClicked` viene generato per notificare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  In questo modo il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] può eseguire la convalida dei parametri prima di notificare l'host.  Il gestore ottiene il testo dai controlli <xref:System.Windows.Controls.TextBox> e lo assegna a proprietà pubbliche, dalle quali l'host può recuperare le informazioni.  
  
 Dichiarazione di evento in WPFPage.h:  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageEventDecl](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpageeventdecl)]  
  
 Gestore eventi <xref:System.Windows.Controls.Primitives.ButtonBase.Click> in WPFPage.cpp:  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageButtonClicked](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagebuttonclicked)]  
  
<a name="set_page_properties"></a>   
### Impostazione delle proprietà WPF  
 L'host [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] consente all'utente di modificare diverse proprietà del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Dal lato di [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], si tratta semplicemente di modificare le proprietà.  L'implementazione nella classe del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è leggermente più complessa, poiché non esiste un'unica proprietà globale che controlla i tipi di carattere per tutti i controlli.  La proprietà adatta per ogni controllo viene modificata nelle funzioni di accesso dell'insieme di proprietà.  L'esempio seguente illustra il codice completo per la proprietà `DefaultFontFamily`.  Impostando la proprietà, viene chiamato un metodo privato che a sua volta imposta le proprietà <xref:System.Windows.Controls.Control.FontFamily%2A> per i vari controlli.  
  
 Da WPFPage.h:  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageFontFamilyProperty](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpagefontfamilyproperty)]  
  
 Da WPFPage.cpp:  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageSetFontFamily](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagesetfontfamily)]  
  
## Vedere anche  
 <xref:System.Windows.Interop.HwndSource>   
 [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)