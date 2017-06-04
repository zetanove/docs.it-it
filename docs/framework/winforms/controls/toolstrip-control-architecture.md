---
title: "Architettura del controllo ToolStrip | Microsoft Docs"
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
  - "ToolStrip (controllo) [Windows Form], architettura"
ms.assetid: 71df2d18-862e-4701-9ff9-c1fe606f94f2
caps.latest.revision: 32
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 32
---
# Architettura del controllo ToolStrip
Le classi <xref:System.Windows.Forms.ToolStrip> e <xref:System.Windows.Forms.ToolStripItem> forniscono un sistema flessibile e estendibile per la visualizzazione di elementi di barre degli strumenti, barre di stato e menu.  Tutte le classi sono contenute nello spazio dei nomi <xref:System.Windows.Forms> e nel nome contengono il prefisso "ToolStrip" \(ad esempio <xref:System.Windows.Forms.ToolStripOverflow>\) oppure il suffisso "Strip" \(ad esempio <xref:System.Windows.Forms.MenuStrip>\).  
  
## ToolStrip  
 Negli argomenti seguenti vengono descritti la classe <xref:System.Windows.Forms.ToolStrip> e i relativi controlli derivati.  
  
 <xref:System.Windows.Forms.ToolStrip> è la classe base astratta per <xref:System.Windows.Forms.MenuStrip>, <xref:System.Windows.Forms.StatusStrip> e <xref:System.Windows.Forms.ContextMenuStrip>.  Nel modello a oggetti seguente viene illustrata la gerarchia di ereditarietà di <xref:System.Windows.Forms.ToolStrip>.  
  
 ![Modello a oggetti ToolStrip](../../../../docs/framework/winforms/controls/media/toolstripobjectmodel.png "ToolStripObjectModel")  
Modello a oggetti ToolStrip  
  
 È possibile accedere a tutti gli elementi in <xref:System.Windows.Forms.ToolStrip> attraverso la raccolta <xref:System.Windows.Forms.ToolStrip.Items%2A>.  È possibile accedere a tutti gli elementi in <xref:System.Windows.Forms.ToolStripDropDownItem> attraverso la raccolta <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItems%2A>.  In una classe derivata da <xref:System.Windows.Forms.ToolStrip>, è anche possibile utilizzare la proprietà <xref:System.Windows.Forms.ToolStrip.DisplayedItems%2A> per accedere solo agli elementi attualmente visualizzati.  Si tratta degli elementi non presenti attualmente in un menu di overflow.  
  
 Gli elementi riportati di seguito sono progettati specificamente per essere utilizzati senza problemi con <xref:System.Windows.Forms.ToolStripSystemRenderer> e <xref:System.Windows.Forms.ToolStripProfessionalRenderer> in tutti gli orientamenti.  Per impostazione predefinita, sono disponibili in fase di progettazione per il controllo <xref:System.Windows.Forms.ToolStrip>:  
  
-   <xref:System.Windows.Forms.ToolStripButton>  
  
-   <xref:System.Windows.Forms.ToolStripSeparator>  
  
-   <xref:System.Windows.Forms.ToolStripLabel>  
  
-   <xref:System.Windows.Forms.ToolStripDropDownButton>  
  
-   <xref:System.Windows.Forms.ToolStripSplitButton>  
  
-   <xref:System.Windows.Forms.ToolStripTextBox>  
  
-   <xref:System.Windows.Forms.ToolStripComboBox>  
  
### MenuStrip  
 <xref:System.Windows.Forms.MenuStrip> è il contenitore di livello superiore che sostituisce <xref:System.Windows.Forms.MainMenu>.  Fornisce inoltre la gestione dei tasti e funzionalità di interfaccia a documenti multipli.  Dal punto di vista funzionale, <xref:System.Windows.Forms.ToolStripDropDownItem> e <xref:System.Windows.Forms.ToolStripMenuItem> vengono utilizzate insieme a <xref:System.Windows.Forms.MenuStrip>, sebbene derivino da <xref:System.Windows.Forms.ToolStripItem>.  
  
 Gli elementi riportati di seguito sono progettati specificamente per essere utilizzati senza problemi con <xref:System.Windows.Forms.ToolStripSystemRenderer> e <xref:System.Windows.Forms.ToolStripProfessionalRenderer> in tutti gli orientamenti.  Per impostazione predefinita, sono disponibili in fase di progettazione per il controllo <xref:System.Windows.Forms.MenuStrip>:  
  
-   <xref:System.Windows.Forms.ToolStripMenuItem>  
  
-   <xref:System.Windows.Forms.ToolStripTextBox>  
  
-   <xref:System.Windows.Forms.ToolStripComboBox>  
  
### StatusStrip  
 <xref:System.Windows.Forms.StatusStrip> sostituisce il controllo <xref:System.Windows.Forms.StatusBar>.  Le funzionalità speciali di <xref:System.Windows.Forms.StatusStrip> includono un layout di tabella personalizzato, il supporto per i riquadri di ridimensionamento e di spostamento e la proprietà `Spring`, che consente a <xref:System.Windows.Forms.ToolStripStatusLabel> di occupare automaticamente lo spazio disponibile.  
  
 Gli elementi riportati di seguito sono progettati specificamente per essere utilizzati senza problemi con <xref:System.Windows.Forms.ToolStripSystemRenderer> e <xref:System.Windows.Forms.ToolStripProfessionalRenderer> in tutti gli orientamenti.  Per impostazione predefinita, sono disponibili in fase di progettazione per il controllo <xref:System.Windows.Forms.StatusStrip>:  
  
-   <xref:System.Windows.Forms.ToolStripStatusLabel>  
  
-   <xref:System.Windows.Forms.ToolStripDropDownButton>  
  
-   <xref:System.Windows.Forms.ToolStripSplitButton>  
  
-   <xref:System.Windows.Forms.ToolStripProgressBar>  
  
### ContextMenuStrip  
 <xref:System.Windows.Forms.ContextMenuStrip> sostituisce <xref:System.Windows.Forms.ContextMenu>.  È possibile associare un controllo <xref:System.Windows.Forms.ContextMenuStrip> a qualsiasi controllo. Con un'azione di clic con il pulsante destro del mouse verrà automaticamente visualizzato un menu di scelta rapida.  È possibile mostrare un oggetto <xref:System.Windows.Forms.ContextMenuStrip> a livello di programmazione utilizzando il metodo <xref:System.Windows.Forms.ToolStripDropDown.Show%2A>.  L'oggetto <xref:System.Windows.Forms.ContextMenuStrip> supporta gli eventi cancellabili <xref:System.Windows.Forms.ToolStripDropDown.Opening> e <xref:System.Windows.Forms.ToolStripDropDown.Closing> per gestire il popolamento dinamico e scenari a selezione multipla.  L'oggetto <xref:System.Windows.Forms.ContextMenuStrip> supporta le immagini, lo stato di selezione delle voci di menu, il testo, i tasti di scelta, i tasti di scelta rapida e i menu a cascata.  
  
 Gli elementi riportati di seguito sono progettati specificamente per essere utilizzati senza problemi con <xref:System.Windows.Forms.ToolStripSystemRenderer> e <xref:System.Windows.Forms.ToolStripProfessionalRenderer> in tutti gli orientamenti.  Per impostazione predefinita, sono disponibili in fase di progettazione per il controllo <xref:System.Windows.Forms.ContextMenuStrip>:  
  
-   <xref:System.Windows.Forms.ToolStripMenuItem>  
  
-   <xref:System.Windows.Forms.ToolStripSeparator>  
  
-   <xref:System.Windows.Forms.ToolStripTextBox>  
  
-   <xref:System.Windows.Forms.ToolStripComboBox>  
  
### Funzionalità generiche di ToolStrip  
 Negli argomenti seguenti vengono descritti le funzionalità e il comportamento generici per il controllo <xref:System.Windows.Forms.ToolStrip> e i controlli derivati.  
  
#### Disegno  
 È possibile eseguire disegni personalizzati nei controlli <xref:System.Windows.Forms.ToolStrip> in molti modi.  Come altri controlli Windows Form, i controlli <xref:System.Windows.Forms.ToolStrip> e <xref:System.Windows.Forms.ToolStripItem> dispongono di metodi `OnPaint` ed eventi `Paint` sottoponibili a override.  Analogamente ai disegni normali, il sistema di coordinate è relativo all'area client del controllo, ovvero l'angolo superiore sinistro del controllo corrisponde a 0, 0.  L'evento `Paint` e il metodo `OnPaint` per un oggetto <xref:System.Windows.Forms.ToolStripItem> si comportano come gli altri eventi del controllo Paint.  
  
 I controlli <xref:System.Windows.Forms.ToolStrip> forniscono inoltre l'accesso ottimizzato al rendering degli elementi e del contenitore tramite la classe <xref:System.Windows.Forms.ToolStripRenderer>, che dispone di metodi sottoponibili a override per il disegno dello sfondo, dello sfondo dell'elemento, dell'immagine dell'elemento, della freccia dell'elemento e del testo dell'elemento, nonché del bordo di <xref:System.Windows.Forms.ToolStrip>.  Gli argomenti dell'evento per questi metodi espongono diverse proprietà ad esempio rettangoli, colori e formati testo che è possibile regolare secondo necessità.  
  
 Per regolare solo alcuni aspetti di come viene disegnato un elemento, eseguire generalmente l'override della classe <xref:System.Windows.Forms.ToolStripRenderer>.  
  
 Se si scrive un nuovo elemento e si desidera controllare tutti gli aspetti del disegno, eseguire l'override del metodo `OnPaint`.  Dal metodo `OnPaint` è possibile utilizzare i metodi della classe <xref:System.Windows.Forms.ToolStripRenderer>.  
  
 Per impostazione predefinita, il controllo <xref:System.Windows.Forms.ToolStrip> è a doppio buffering, traendo vantaggio dall'impostazione <xref:System.Windows.Forms.ControlStyles>.  
  
#### Elemento padre  
 Il concetto di proprietà e elemento padre del contenitore è più complesso nei controlli <xref:System.Windows.Forms.ToolStrip> che in altri controlli contenitori Windows Form.  È necessario per supportare scenari dinamici come overflow e condivisione di elementi a discesa tra più elementi <xref:System.Windows.Forms.ToolStrip> e per supportare la generazione di una classe <xref:System.Windows.Forms.ContextMenuStrip> da un controllo.  
  
 Nell'elenco seguente vengono descritti i membri relativi all'assegnazione di un elemento padre e il relativo utilizzo.  
  
-   La proprietà <xref:System.Windows.Forms.ToolStripDropDown.OwnerItem%2A> accede all'elemento che corrisponde all'origine dell'elemento a discesa.  È simile alla proprietà <xref:System.Windows.Forms.ContextMenuStrip.SourceControl%2A>, ma anziché restituire un controllo, restituisce una classe <xref:System.Windows.Forms.ToolStripItem>.  
  
-   La proprietà <xref:System.Windows.Forms.ContextMenuStrip.SourceControl%2A> determina quale controllo è l'origine della classe <xref:System.Windows.Forms.ContextMenuStrip> quando più controlli condividono la stessa classe <xref:System.Windows.Forms.ContextMenuStrip>.  
  
-   Il metodo <xref:System.Windows.Forms.ToolStripItem.GetCurrentParent%2A> è una funzione di accesso di sola lettura alla proprietà <xref:System.Windows.Forms.ToolStripItem.Parent%2A>.  Un elemento padre differisce da un proprietario in quanto indica il controllo <xref:System.Windows.Forms.ToolStrip> corrente restituito in cui l'elemento è visualizzato, che potrebbe essere nell'area di overflow.  
  
-   La proprietà <xref:System.Windows.Forms.ToolStripItem.Owner%2A> restituisce il controllo <xref:System.Windows.Forms.ToolStrip> la cui raccolta Items contiene il controllo <xref:System.Windows.Forms.ToolStripItem> corrente.  Questo è il modo migliore per fare riferimento alla proprietà <xref:System.Windows.Forms.ToolStrip.ImageList%2A> o ad altre proprietà nel controllo <xref:System.Windows.Forms.ToolStrip> di livello superiore senza scrivere codice speciale per gestire l'overflow.  
  
#### Comportamento dei controlli ereditati  
 I controlli seguenti vengono bloccati ogni volta che vengono utilizzati nell'erediterietà:  
  
-   <xref:System.Windows.Forms.ToolStrip>  
  
-   <xref:System.Windows.Forms.MenuStrip>  
  
-   <xref:System.Windows.Forms.ContextMenuStrip>  
  
-   <xref:System.Windows.Forms.StatusStrip>  
  
-   <xref:System.Windows.Forms.ToolStripPanel> che include i pannelli in un controllo <xref:System.Windows.Forms.ToolStripContainer> e anche i singoli controlli <xref:System.Windows.Forms.ToolStripPanel>.  
  
 Ad esempio, creare una nuova applicazione Windows Form utilizzando uno o più controlli dell'elenco precedente.  Impostare il modificatore di accesso di uno o più controlli su `public` o `protected`e quindi compilare il progetto.  Aggiungere un form che eredita dal primo form, quindi selezionare un controllo ereditato.  Il controllo appare bloccato e si comporta come se il proprio modificatore di accesso fosse `private`.  
  
#### Supporto di ToolStripContainer dell'ereditarietà  
 Il controllo <xref:System.Windows.Forms.ToolStripContainer> supporta scenari di ereditarietà limitati, in modo simile all'esempio seguente:  
  
1.  Creare una nuova applicazione Windows Form.  
  
2.  Aggiungere una classe <xref:System.Windows.Forms.ToolStripContainer> al form.  
  
3.  Impostare il modificatore di accesso del controllo <xref:System.Windows.Forms.ToolStripContainer> su `public` o `protected`.  
  
4.  Aggiungere qualsiasi combinazione di controlli <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip> e <xref:System.Windows.Forms.ContextMenuStrip> alle aree <xref:System.Windows.Forms.ToolStripPanel> del controllo <xref:System.Windows.Forms.ToolStripContainer>.  
  
5.  Compilare il progetto.  
  
6.  Aggiungere un form che eredita dal primo form.  
  
7.  Selezionare il controllo <xref:System.Windows.Forms.ToolStripContainer> ereditato sul form.  
  
#### Comportamento ereditato dei controlli figlio  
 Dopo aver completato i passaggi precedenti, si verifica il comportamento ereditato seguente:  
  
-   Nella finestra di progettazione il controllo viene visualizzato con un'icona ereditata.  
  
-   I controlli <xref:System.Windows.Forms.ToolStripPanel> sono bloccati. Non è possibile selezionare né ridisporre il relativo contenuto.  
  
-   È possibile aggiungere controlli al controllo <xref:System.Windows.Forms.ToolStripContentPanel>, spostare i controlli e renderli controlli figlio del controllo <xref:System.Windows.Forms.ToolStripContentPanel>.  
  
-   Le modifiche persistono dopo la compilazione del form.  
  
    > [!NOTE]
    >  Rimuovere i modificatori di accesso da tutti i controlli <xref:System.Windows.Forms.ToolStripPanel> che fanno parte di un controllo <xref:System.Windows.Forms.ToolStripContainer>.  Il modificatore di accesso del controllo <xref:System.Windows.Forms.ToolStripContainer> regola l'intero controllo.  
  
#### Attendibilità parziale  
 Le limitazioni dei controlli `ToolStrip` con attendibilità parziale sono progettate per impedire l'immissione accidentale di informazioni personali che potrebbero essere utilizzate da utenti o servizi non autorizzati.  Di seguito sono riportate le misure protettive:  
  
-   I controlli `ToolStripDropDown` richiedono che l'enumerazione <xref:System.Security.Permissions.UIPermissionWindow> visualizzi gli elementi in una classe <xref:System.Windows.Forms.ToolStripControlHost>.  Ciò vale sia per i controlli intrinseci, ad esempio <xref:System.Windows.Forms.ToolStripTextBox>, <xref:System.Windows.Forms.ToolStripComboBox> e <xref:System.Windows.Forms.ToolStripProgressBar> che per i controlli creati dall'utente.  Se questo requisito non viene soddisfatto, gli elementi non vengono visualizzati.  Non viene generata alcuna eccezione.  
  
-   Non è consentito impostare la proprietà <xref:System.Windows.Forms.ToolStripDropDown.AutoClose%2A> su `false` e il parametro dell'evento <xref:System.Windows.Forms.ToolStripDropDown.Closing> annullabile viene ignorato.  In questo modo è impossibile immettere più di una sequenza di tasti senza chiudere l'elenco a discesa.  Se questo requisito non viene soddisfatto, gli elementi non vengono visualizzati.  Non viene generata alcuna eccezione.  
  
-   Molti eventi di gestione delle sequenze di tasti non verranno generati se si verificano in contesti con attendibilità parziale diversi da <xref:System.Security.Permissions.UIPermissionWindow>.  
  
-   I tasti di scelta non vengono elaborati se non viene concessa l'enumerazione <xref:System.Security.Permissions.UIPermissionWindow>.  
  
#### Utilizzo  
 I modelli di utilizzo seguenti influiscono sul layout del controllo <xref:System.Windows.Forms.ToolStrip>, sull'interazione da tastiera e sul comportamento degli utenti finali:  
  
-   Unito in un controllo <xref:System.Windows.Forms.ToolStripPanel>  
  
     <xref:System.Windows.Forms.ToolStrip> può essere riposizionato all'interno del controllo <xref:System.Windows.Forms.ToolStripPanel> e tra i controlli <xref:System.Windows.Forms.ToolStripPanel>.  La proprietà `Dock` viene ignorata e, se viene ignorata e, se <xref:System.Windows.Forms.ToolStrip.Stretch%2A> la proprietà è `false`, le dimensioni di <xref:System.Windows.Forms.ToolStrip> aumentano quando vengono aggiunti elementi a <xref:System.Windows.Forms.ToolStripPanel>.  In genere, <xref:System.Windows.Forms.ToolStrip> non partecipa nell'ordine di tabulazione.  
  
-   Ancorato  
  
     <xref:System.Windows.Forms.ToolStrip> viene inserito su un lato di un contenitore in una posizione fissa e le relative dimensioni si espandono in tutto il bordo cui è ancorato.  In genere, <xref:System.Windows.Forms.ToolStrip> non partecipa nell'ordine di tabulazione.  
  
-   Posizionato in modo assoluto  
  
     <xref:System.Windows.Forms.ToolStrip> è simile ad altri controlli, in quanto viene inserito dalla proprietà <xref:System.Windows.Forms.Control.Location%2A>, ha dimensioni fisse e in genere partecipa nell'ordine di tabulazione.  
  
#### Interazione da tastiera  
  
##### Tasti di scelta  
 Premuti in combinazione o dopo il tasto ALT, i tasti di scelta rappresentano una delle modalità disponibili per attivare un controllo tramite tastiera.  <xref:System.Windows.Forms.ToolStrip> supporta i tasti di scelta espliciti e impliciti.  Con la definizione esplicita si utilizza un carattere e commerciale \(&\) anteposto alla lettera.  Con la definizione implicita si utilizza un algoritmo che tenta di trovare un elemento corrispondente in base all'ordine dei caratteri in una proprietà `Text` specificata.  
  
##### Tasti di scelta rapida  
 Per la definizione dei tasti di scelta rapida utilizzati da un controllo <xref:System.Windows.Forms.MenuStrip> si utilizza una combinazione dell'enumerazione <xref:System.Windows.Forms.Keys> \(che non è specifica dell'ordine\).  È anche possibile utilizzare la proprietà <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A> per visualizzare un tasto di scelta rapida con solo testo, ad esempio che visualizza "Canc" anziché "Elimina".  
  
##### Navigazione  
 Il tasto ALT attiva il controllo <xref:System.Windows.Forms.MenuStrip> a cui fa riferimento la proprietà <xref:System.Windows.Forms.Form.MainMenuStrip%2A>.  Da questo punto, la combinazione CTRL\+TAB consente di spostarsi tra i controlli <xref:System.Windows.Forms.ToolStrip> all'interno dei controlli `ToolStripPanel`.  Il tasto TAB e i tasti di direzione del tastierino numerico consentono di spostarsi tra gli elementi di un controllo <xref:System.Windows.Forms.ToolStrip>.  Un algoritmo speciale gestisce la navigazione nell'area di overflow.  Con la BARRA SPAZIATRICE si seleziona un controllo <xref:System.Windows.Forms.ToolStripButton>, <xref:System.Windows.Forms.ToolStripDropDownButton> o <xref:System.Windows.Forms.ToolStripSplitButton>.  
  
##### Stato attivo e convalida  
 Se attivato dal tasto ALT, il controllo <xref:System.Windows.Forms.MenuStrip> o <xref:System.Windows.Forms.ToolStrip> in genere non assume né rimuove lo stato attivo dal controllo cui è al momento assegnato.  Se è disponibile un controllo contenuto all'interno della classe <xref:System.Windows.Forms.MenuStrip> o un controllo a discesa della classe <xref:System.Windows.Forms.MenuStrip>, il controllo riceve lo stato attivo quando l'utente preme il tasto TAB.  In generale, è possibile che gli eventi <xref:System.Windows.Forms.Control.GotFocus>, <xref:System.Windows.Forms.Control.LostFocus>, <xref:System.Windows.Forms.Control.Enter> e <xref:System.Windows.Forms.Control.Leave> di <xref:System.Windows.Forms.MenuStrip> non vengano generati quando vengono attivati tramite tastiera.  In tali casi, utilizzare invece gli eventi <xref:System.Windows.Forms.MenuStrip.MenuActivate> e <xref:System.Windows.Forms.MenuStrip.MenuDeactivate>.  
  
 Per impostazione predefinita, il valore di <xref:System.Windows.Forms.ToolStrip.CausesValidation%2A> è `false`.  Eseguire una chiamata al metodo <xref:System.Windows.Forms.ContainerControl.Validate%2A> in modo esplicito sul form per eseguire la convalida.  
  
#### Layout  
 Per controllare il layout di <xref:System.Windows.Forms.ToolStrip>, scegliere uno dei membri della classe <xref:System.Windows.Forms.ToolStripLayoutStyle> con la proprietà <xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A>.  
  
##### Layout di stack  
 Lo stacking è la disposizione degli elementi adiacenti alle due estremità della classe <xref:System.Windows.Forms.ToolStrip>.  Nell'elenco riportato di seguito vengono descritti i layout di stack.  
  
-   <xref:System.Windows.Forms.ToolStripLayoutStyle> è il valore predefinito.  Con questa impostazione il layout di <xref:System.Windows.Forms.ToolStrip> viene modificato automaticamente in base alla proprietà <xref:System.Windows.Forms.ToolStrip.Orientation%2A> per gestire gli scenari di trascinamento e ancoraggio.  
  
-   <xref:System.Windows.Forms.ToolStripLayoutStyle> esegue il rendering degli elementi <xref:System.Windows.Forms.ToolStrip> adiacenti in orientamento verticale.  
  
-   <xref:System.Windows.Forms.ToolStripLayoutStyle> esegue il rendering degli elementi <xref:System.Windows.Forms.ToolStrip> adiacenti in orientamento orizzontale.  
  
##### Altre funzionalità dei layout di stack  
 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> determina la fine del <xref:System.Windows.Forms.ToolStrip> a cui l'elemento viene allineato.  
  
 Quando gli elementi non corrispondono all'interno del <xref:System.Windows.Forms.ToolStrip>, viene visualizzato automaticamente un pulsante di overflow.  L'impostazione della proprietà <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> determina se un elemento deve essere visualizzato o meno nell'area di overflow, in base alle necessità.  
  
 Nell'evento <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> è possibile controllare la proprietà <xref:System.Windows.Forms.ToolStripItem.Placement%2A> per determinare se un elemento è stato collocato nella classe <xref:System.Windows.Forms.ToolStrip> principale, nella classe <xref:System.Windows.Forms.ToolStrip> di overflow o se non viene visualizzato affatto.  Un elemento non viene in genere visualizzato perché non è contenuto nell'oggetto <xref:System.Windows.Forms.ToolStrip> principale e la relativa proprietà <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> è impostata su <xref:System.Windows.Forms.ToolStripItemOverflow>.  
  
 Rendere un <xref:System.Windows.Forms.ToolStrip> mobile inserendolo in un <xref:System.Windows.Forms.ToolStripPanel> e impostandone la proprietà <xref:System.Windows.Forms.ToolStrip.GripStyle%2A> su <xref:System.Windows.Forms.ToolStripGripStyle>.  
  
##### Altre opzioni di layout  
 Le altre opzioni di layout sono <xref:System.Windows.Forms.ToolStripLayoutStyle> e <xref:System.Windows.Forms.ToolStripLayoutStyle>.  
  
##### Layout di flusso  
 Il layout <xref:System.Windows.Forms.ToolStripLayoutStyle> è l'impostazione predefinita per <xref:System.Windows.Forms.ContextMenuStrip>, <xref:System.Windows.Forms.ToolStripDropDownMenu> e <xref:System.Windows.Forms.ToolStripOverflow>.  È simile alla classe <xref:System.Windows.Forms.FlowLayoutPanel>.  Le funzionalità del layout <xref:System.Windows.Forms.ToolStripLayoutStyle> sono:  
  
-   Tutte le funzionalità di <xref:System.Windows.Forms.FlowLayoutPanel> sono esposte dalla proprietà <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A>.  È necessario eseguire il cast della classe <xref:System.Windows.Forms.LayoutSettings> a una classe <xref:System.Windows.Forms.FlowLayoutSettings>.  
  
-   È possibile utilizzare le proprietà <xref:System.Windows.Forms.ToolStripItem.Dock%2A> e <xref:System.Windows.Forms.ToolStripItem.Anchor%2A> nel codice per allineare gli elementi all'interno della riga.  
  
-   La proprietà <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> viene ignorata.  
  
-   Nell'evento <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> è possibile controllare la proprietà <xref:System.Windows.Forms.ToolStripItem.Placement%2A> per determinare se un elemento è stato collocato nella classe <xref:System.Windows.Forms.ToolStrip> principale.  
  
-   Poiché non viene eseguito il rendering del riquadro di ridimensionamento, non è possibile spostare un <xref:System.Windows.Forms.ToolStrip> nello stile di layout <xref:System.Windows.Forms.ToolStripLayoutStyle> di un <xref:System.Windows.Forms.ToolStripPanel> .  
  
-   Il pulsante di overflow <xref:System.Windows.Forms.ToolStrip> non viene sottoposto a rendering e la proprietà <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> viene ignorata.  
  
##### Layout Table  
 Il layout <xref:System.Windows.Forms.ToolStripLayoutStyle> è l'impostazione predefinita per <xref:System.Windows.Forms.StatusStrip>.  È simile a <xref:System.Windows.Forms.TableLayoutPanel>.  Le funzionalità del layout <xref:System.Windows.Forms.ToolStripLayoutStyle> sono:  
  
-   Tutte le funzionalità di <xref:System.Windows.Forms.TableLayoutPanel> sono esposte dalla proprietà <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A>.  È necessario eseguire il cast della classe <xref:System.Windows.Forms.LayoutSettings> a una classe <xref:System.Windows.Forms.TableLayoutSettings>.  
  
-   È possibile utilizzare le proprietà <xref:System.Windows.Forms.ToolStripItem.Dock%2A> e <xref:System.Windows.Forms.ToolStripItem.Anchor%2A> nel codice per allineare gli elementi all'interno della cella di tabella.  
  
-   La proprietà <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> viene ignorata.  
  
-   Nell'evento <xref:System.Windows.Forms.ToolStrip.LayoutCompleted> è possibile controllare la proprietà <xref:System.Windows.Forms.ToolStripItem.Placement%2A> per determinare se un elemento è stato collocato nella classe <xref:System.Windows.Forms.ToolStrip> principale.  
  
-   Il riquadro di ridimensionamento non viene sottoposto a rendering, pertanto non è possibile spostare il controllo <xref:System.Windows.Forms.ToolStrip> nello stile di layout <xref:System.Windows.Forms.ToolStripLayoutStyle> di un controllo <xref:System.Windows.Forms.ToolStripPanel>.  
  
-   Il pulsante di overflow <xref:System.Windows.Forms.ToolStrip> non viene sottoposto a rendering e la proprietà <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> viene ignorata.  
  
## ToolStripItem  
 Negli argomenti seguenti vengono descritti la classe <xref:System.Windows.Forms.ToolStripItem> e i relativi controlli derivati.  
  
 <xref:System.Windows.Forms.ToolStripItem> è la classe base astratta per tutti gli elementi da inserire in un controllo <xref:System.Windows.Forms.ToolStrip>.  Nel modello a oggetti seguente viene illustrata la gerarchia di ereditarietà di <xref:System.Windows.Forms.ToolStripItem>.  
  
 ![Modello a oggetti ToolStripItem](../../../../docs/framework/winforms/controls/media/toolstripitemobjectmodel.png "ToolStripItemObjectModel")  
Modello a oggetti ToolStripItem  
  
 Le classi <xref:System.Windows.Forms.ToolStripItem> ereditano direttamente da <xref:System.Windows.Forms.ToolStripItem> o indirettamente da <xref:System.Windows.Forms.ToolStripItem> tramite <xref:System.Windows.Forms.ToolStripControlHost> o <xref:System.Windows.Forms.ToolStripDropDownItem>.  
  
 I controlli <xref:System.Windows.Forms.ToolStripItem> devono essere contenuti in un controllo <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip>, <xref:System.Windows.Forms.StatusStrip> o <xref:System.Windows.Forms.ContextMenuStrip> e non possono essere aggiunti direttamente a un form.  Le varie classi di contenitori sono progettate per contenere un sottoinsieme appropriato di controlli <xref:System.Windows.Forms.ToolStripItem>.  
  
 Nella tabella seguente sono elencati i controlli <xref:System.Windows.Forms.ToolStripItem> predefiniti e i contenitori a essi più appropriati.  Pur potendo essere incluso in qualsiasi contenitore derivato da <xref:System.Windows.Forms.ToolStrip>, ogni elemento <xref:System.Windows.Forms.ToolStrip> è progettato espressamente per essere inserito nei contenitori seguenti:  
  
> [!NOTE]
>  <xref:System.Windows.Forms.ToolStripDropDown> non è presente nella casella degli strumenti della finestra di progettazione.  
  
|Elemento contenuto|ToolStrip|MenuStrip|ContextMenuStrip|StatusStrip|ToolStripDropDown|  
|------------------------|---------------|---------------|----------------------|-----------------|-----------------------|  
|<xref:System.Windows.Forms.ToolStripButton>|Sì|No|No|No|Sì|  
|<xref:System.Windows.Forms.ToolStripComboBox>|Sì|Sì|Sì|No|Sì|  
|<xref:System.Windows.Forms.ToolStripSplitButton>|Sì|No|No|Sì|Sì|  
|<xref:System.Windows.Forms.ToolStripLabel>|Sì|No|No|Sì|Sì|  
|<xref:System.Windows.Forms.ToolStripSeparator>|Sì|Sì|Sì|No|Sì|  
|<xref:System.Windows.Forms.ToolStripDropDownButton>|Sì|No|No|Sì|Sì|  
|<xref:System.Windows.Forms.ToolStripTextBox>|Sì|Sì|Sì|No|Sì|  
|<xref:System.Windows.Forms.ToolStripMenuItem>|No|Sì|Sì|No|No|  
|<xref:System.Windows.Forms.ToolStripStatusLabel>|No|No|No|Sì|No|  
|<xref:System.Windows.Forms.ToolStripProgressBar>|Sì|No|No|Sì|No|  
|<xref:System.Windows.Forms.ToolStripControlHost>|Sì|Sì|No|Sì|Sì|  
  
### ToolStripButton  
 <xref:System.Windows.Forms.ToolStripButton> è l'elemento pulsante per <xref:System.Windows.Forms.ToolStrip>.  È possibile visualizzarlo con vari stili di bordo, nonché utilizzarlo per rappresentare e attivare gli stati operativi.  È inoltre possibile definire che abbia lo stato attivo per impostazione predefinita.  
  
### ToolStripLabel  
 <xref:System.Windows.Forms.ToolStripLabel> fornisce la funzionalità di etichetta nei controlli <xref:System.Windows.Forms.ToolStrip>.  <xref:System.Windows.Forms.ToolStripLabel> è simile a <xref:System.Windows.Forms.ToolStripButton>, che non riceve lo stato attivo per impostazione predefinita e non viene sottoposto a rendering come premuto o evidenziato.  
  
 <xref:System.Windows.Forms.ToolStripLabel>, in quanto elemento ospitato, supporta i tasti di scelta.  
  
 Utilizzare le proprietà <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>, <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> e <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A> in una classe <xref:System.Windows.Forms.ToolStripLabel> per supportare il controllo di collegamento in un controllo <xref:System.Windows.Forms.ToolStrip>.  
  
### ToolStripStatusLabel  
 <xref:System.Windows.Forms.ToolStripStatusLabel> è una versione di <xref:System.Windows.Forms.ToolStripLabel> specificamente progettata per l'utilizzo in <xref:System.Windows.Forms.StatusStrip>.  Le funzionalità speciali includono <xref:System.Windows.Forms.ToolStripStatusLabel.BorderStyle%2A>, <xref:System.Windows.Forms.ToolStripStatusLabel.BorderSides%2A> e <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>.  
  
### ToolStripSeparator  
 La classe <xref:System.Windows.Forms.ToolStripSeparator> aggiunge una linea verticale o orizzontale a una barra degli strumenti o un menu, a seconda dell'orientamento.  Fornisce il raggruppamento o la distinzione tra elementi, ad esempio quelli di un menu.  
  
 È possibile aggiungere un controllo <xref:System.Windows.Forms.ToolStripSeparator> in fase di progettazione scegliendolo da un elenco a discesa.  È tuttavia anche possibile creare automaticamente un controllo <xref:System.Windows.Forms.ToolStripSeparator> digitando un trattino \(\-\) nel nodo del modello della finestra di progettazione o nel metodo <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A>.  
  
### ToolStripControlHost  
 <xref:System.Windows.Forms.ToolStripControlHost> è la classe base astratta per <xref:System.Windows.Forms.ToolStripComboBox>, <xref:System.Windows.Forms.ToolStripTextBox> e <xref:System.Windows.Forms.ToolStripProgressBar>.  <xref:System.Windows.Forms.ToolStripControlHost> può ospitare altri controlli, tra cui i controlli personalizzati, in due modi:  
  
-   Creare una classe <xref:System.Windows.Forms.ToolStripControlHost> con una classe derivata da <xref:System.Windows.Forms.Control>.  Per un accesso completo al controllo contenuto e alle proprietà, è necessario eseguire nuovamente il cast della proprietà <xref:System.Windows.Forms.ToolStripControlHost.Control%2A> sulla classe effettiva che rappresenta.  
  
-   Estendere <xref:System.Windows.Forms.ToolStripControlHost> e chiamare il costruttore della classe base nel costruttore predefinito della classe ereditata, passando una classe derivata da <xref:System.Windows.Forms.Control>.  L'opzione consente di eseguire il wrapping di proprietà e metodi di controllo comuni per l'accesso semplificato a una classe <xref:System.Windows.Forms.ToolStrip>.  
  
### ToolStripComboBox  
 <xref:System.Windows.Forms.ToolStripComboBox> è il controllo <xref:System.Windows.Forms.ComboBox> ottimizzato per l'hosting in un controllo <xref:System.Windows.Forms.ToolStrip>.  Un sottoinsieme delle proprietà e degli eventi del controllo ospitato viene esposto al livello <xref:System.Windows.Forms.ToolStripComboBox>, ma il controllo <xref:System.Windows.Forms.ComboBox> sottostante è completamente accessibile tramite la proprietà <xref:System.Windows.Forms.ToolStripComboBox.ComboBox%2A>.  
  
### ToolStripTextBox  
 <xref:System.Windows.Forms.ToolStripTextBox> è il controllo <xref:System.Windows.Forms.TextBox> ottimizzato per l'hosting in un controllo <xref:System.Windows.Forms.ToolStrip>.  Un sottoinsieme delle proprietà e degli eventi del controllo ospitato viene esposto al livello <xref:System.Windows.Forms.ToolStripTextBox>, ma il controllo <xref:System.Windows.Forms.TextBox> sottostante è completamente accessibile tramite la proprietà <xref:System.Windows.Forms.ToolStripTextBox.TextBox%2A>.  
  
### ToolStripProgressBar  
 <xref:System.Windows.Forms.ToolStripProgressBar> è il controllo <xref:System.Windows.Forms.ProgressBar> ottimizzato per l'hosting in un controllo <xref:System.Windows.Forms.ToolStrip>.  Un sottoinsieme delle proprietà e degli eventi del controllo ospitato viene esposto al livello <xref:System.Windows.Forms.ToolStripProgressBar>, ma il controllo <xref:System.Windows.Forms.ProgressBar> sottostante è completamente accessibile tramite la proprietà <xref:System.Windows.Forms.ToolStripProgressBar.ProgressBar%2A>.  
  
### ToolStripDropDownItem  
 <xref:System.Windows.Forms.ToolStripDropDownItem> è la classe base astratta per <xref:System.Windows.Forms.ToolStripMenuItem>, <xref:System.Windows.Forms.ToolStripDropDownButton> e <xref:System.Windows.Forms.ToolStripSplitButton>, che possono ospitare direttamente gli elementi o ospitare elementi aggiuntivi in un contenitore a discesa.  A tale scopo, impostare la proprietà <xref:System.Windows.Forms.ToolStripDropDownItem.DropDown%2A> su una classe <xref:System.Windows.Forms.ToolStripDropDown> e impostare la proprietà <xref:System.Windows.Forms.ToolStrip.Items%2A> della classe <xref:System.Windows.Forms.ToolStripDropDown>.  Accedere direttamente a questi elementi a discesa tramite la proprietà <xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItems%2A>.  
  
### ToolStripMenuItem  
 <xref:System.Windows.Forms.ToolStripMenuItem> è una classe <xref:System.Windows.Forms.ToolStripDropDownItem> che, insieme a <xref:System.Windows.Forms.ToolStripDropDownMenu> e <xref:System.Windows.Forms.ContextMenuStrip>, gestisce le funzionalità speciali di evidenziazione, layout e disposizione in colonna per i menu.  
  
### ToolStripDropDownButton  
 <xref:System.Windows.Forms.ToolStripDropDownButton> è simile a <xref:System.Windows.Forms.ToolStripButton>, ma visualizza un'area a discesa quando l'utente fa clic.  Nascondere o mostrare la freccia a discesa impostando la proprietà <xref:System.Windows.Forms.ToolStripDropDownButton.ShowDropDownArrow%2A>.  <xref:System.Windows.Forms.ToolStripDropDownButton> contiene un oggetto <xref:System.Windows.Forms.ToolStripOverflowButton> che visualizza gli elementi di overflow dell'oggetto <xref:System.Windows.Forms.ToolStrip>.  
  
### ToolStripSplitButton  
 <xref:System.Windows.Forms.ToolStripSplitButton> combina funzionalità di pulsante e pulsante a discesa.  
  
 Utilizzare la proprietà <xref:System.Windows.Forms.ToolStripSplitButton.DefaultItem%2A> per sincronizzare l'evento <xref:System.Windows.Forms.Control.Click> dell'elemento a discesa prescelto con l'elemento visualizzato sul pulsante.  
  
### Funzionalità generiche di ToolStripItem  
 <xref:System.Windows.Forms.ToolStripItem> fornisce le seguenti funzionalità e opzioni generiche ai controlli che ereditano:  
  
-   Eventi principali  
  
-   Gestione delle immagini  
  
-   Allineamento  
  
-   Relazione tra testo e immagine  
  
-   Stile di visualizzazione  
  
#### Eventi principali  
 I controlli <xref:System.Windows.Forms.ToolStripItem> ricevono gli eventi Click, Mouse e Paint e sono in grado di eseguire anche alcune operazioni di pre\-elaborazione da tastiera.  
  
#### Gestione delle immagini  
 Le proprietà <xref:System.Windows.Forms.ToolStripItem.Image%2A>, <xref:System.Windows.Forms.ToolStripItem.ImageAlign%2A>, <xref:System.Windows.Forms.ToolStripItem.ImageIndex%2A>, <xref:System.Windows.Forms.ToolStripItem.ImageKey%2A> e <xref:System.Windows.Forms.ToolStripItem.ImageScaling%2A> sono relative a vari aspetti della gestione di immagini.  Utilizzare le immagini nei controlli <xref:System.Windows.Forms.ToolStrip> impostando direttamente queste proprietà o impostando la proprietà <xref:System.Windows.Forms.ToolStrip.ImageList%2A> solo in fase di esecuzione.  
  
 Il ridimensionamento dell'immagine è determinato dall'interazione delle proprietà in <xref:System.Windows.Forms.ToolStrip> e <xref:System.Windows.Forms.ToolStripItem>, come segue:  
  
-   <xref:System.Windows.Forms.ToolStrip.ImageScalingSize%2A> è la scala dell'immagine finale come determinato dalla combinazione dell'impostazione <xref:System.Windows.Forms.ToolStripItem.ImageScaling%2A> dell'immagine e l'impostazione <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> del contenitore.  
  
    -   Se la proprietà <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> è `true` \(impostazione predefinita\) e la classe <xref:System.Windows.Forms.ToolStripItemImageScaling> è <xref:System.Windows.Forms.ToolStripItemImageScaling>, non si verifica alcun ridimensionamento dell'immagine e le dimensioni di <xref:System.Windows.Forms.ToolStrip> corrispondono a quelle dell'elemento più grande oppure a una dimensione minima prestabilita.  
  
    -   Se la proprietà <xref:System.Windows.Forms.ToolStrip.AutoSize%2A> è `false` e la classe <xref:System.Windows.Forms.ToolStripItemImageScaling> è <xref:System.Windows.Forms.ToolStripItemImageScaling>, non si verifica il ridimensionamento dell'immagine né di <xref:System.Windows.Forms.ToolStrip>.  
  
#### Allineamento  
 Il valore della proprietà <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> determina l'estremità del controllo <xref:System.Windows.Forms.ToolStrip> in corrispondenza della quale è visualizzato un elemento.  La proprietà <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> funziona solo quando lo stile di layout del controllo <xref:System.Windows.Forms.ToolStrip> è impostato su uno dei valori di overflow dello stack.  
  
 Gli elementi vengono inseriti sul controllo <xref:System.Windows.Forms.ToolStrip> nell'ordine in cui appaiono nella raccolta Items.  Per modificare a livello di codice la posizione in cui viene inserito un elemento, utilizzare il metodo <xref:System.Windows.Forms.ToolStripItemCollection.Insert%2A> per spostare l'elemento nella raccolta.  Questo metodo sposta l'elemento ma non lo duplica.  
  
#### Relazione tra testo e immagine  
 La proprietà <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A> definisce la posizione relativa dell'immagine rispetto al testo in un controllo <xref:System.Windows.Forms.ToolStripItem>.  Gli elementi senza immagine, testo o entrambi vengono considerati come casi speciali, in modo che il controllo <xref:System.Windows.Forms.ToolStripItem> non visualizzi uno spazio vuoto al posto dell'elemento o degli elementi mancanti.  
  
#### Stile di visualizzazione  
 La proprietà <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> consente di impostare i valori delle proprietà Text e Image di un elemento visualizzando solo gli elementi desiderati.  Questa opzione viene in genere utilizzata per modificare solo lo stile di visualizzazione quando lo stesso elemento viene mostrato in un contesto diverso.  
  
## Classi accessorie  
 Le classi che forniscono varie altre funzionalità includono:  
  
-   <xref:System.Windows.Forms.ToolStripManager> supporta attività correlate a <xref:System.Windows.Forms.ToolStrip> per intere applicazioni, ad esempio unione, impostazioni e opzioni di rendering.  
  
-   <xref:System.Windows.Forms.ToolStripRenderer> consente di applicare facilmente uno stile o un tema specifico a <xref:System.Windows.Forms.ToolStrip>.  
  
-   <xref:System.Windows.Forms.ToolStripProfessionalRenderer> crea penne e pennelli in base a una tabella di colori sostituibili \(<xref:System.Windows.Forms.ProfessionalColorTable>\).  
  
-   <xref:System.Windows.Forms.ToolStripSystemRenderer> applica i colori di sistema e uno stile di visualizzazione uniforme alle applicazioni <xref:System.Windows.Forms.ToolStrip>.  
  
-   <xref:System.Windows.Forms.ToolStripContainer> è simile a <xref:System.Windows.Forms.SplitContainer>.  Utilizza quattro pannelli laterali ancorati \(istanze di <xref:System.Windows.Forms.ToolStripPanel>\) e un pannello centrale \(istanza di <xref:System.Windows.Forms.ToolStripContentPanel>\) per creare una disposizione tipica.  Non è possibile rimuovere i pannelli laterali, ma è possibile nasconderli.  Non è possibile rimuovere né nascondere il pannello centrale.  È possibile disporre uno o più controlli <xref:System.Windows.Forms.ToolStrip>, <xref:System.Windows.Forms.MenuStrip> o <xref:System.Windows.Forms.StatusStrip> nei pannelli laterali e utilizzare il pannello centrale per altri controlli.  La classe <xref:System.Windows.Forms.ToolStripContentPanel> consente inoltre il supporto del renderer nel corpo del form per un aspetto uniforme.  <xref:System.Windows.Forms.ToolStripContainer> non supporta l'interfaccia a più documenti.  
  
-   <xref:System.Windows.Forms.ToolStripPanel> fornisce lo spazio per spostare e disporre i controlli <xref:System.Windows.Forms.ToolStrip>.  È possibile utilizzare solo un pannello se si preferisce e <xref:System.Windows.Forms.ToolStripPanel> è efficace negli scenari di interfaccia a documenti multipli.  
  
## Vedere anche  
 [Cenni preliminari sul controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [Riepilogo della tecnologia ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)   
 [Controllo ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)   
 [Controllo MenuStrip](../../../../docs/framework/winforms/controls/menustrip-control-windows-forms.md)   
 [Controllo StatusStrip](../../../../docs/framework/winforms/controls/statusstrip-control.md)   
 [Controllo ContextMenuStrip](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)   
 [Controllo BindingNavigator](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)