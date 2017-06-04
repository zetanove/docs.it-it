---
title: "Automatic Scaling in Windows Forms | Microsoft Docs"
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
  - "scalability, automatic in Windows Forms"
  - "Windows Forms, automatic scaling"
ms.assetid: 68fad25b-afbc-44bd-8e1b-966fc43507a4
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Automatic Scaling in Windows Forms
Con il ridimensionamento automatico, un form e i relativi controlli, progettati su un computer con una determinata risoluzione dello schermo o tipo di carattere del sistema, possono essere visualizzati correttamente su un altro computer con una risoluzione dello schermo o tipo di carattere del sistema diverso.  Questa funzionalità assicura che il form e i controlli vengano ridimensionati in modo coerente con le finestre native e le altre applicazioni presenti sia sui computer degli utenti che su quelli di altri sviluppatori.  Il supporto di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] per il ridimensionamento automatico e gli stili di visualizzazione consente alle applicazioni [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] di avere sempre un aspetto coerente, se confrontate con le applicazioni Windows native sul computer di ogni utente.  
  
## Necessità del ridimensionamento automatico  
 Senza ridimensionamento automatico, un'applicazione progettata per un'unica risoluzione dello schermo o tipo di carattere apparirà troppo piccola o troppo grande quando si modifica tale risoluzione o tipo di carattere.  Ad esempio, se l'applicazione viene progettata con Tahoma a 9 punti come base, senza regolazione apparirà troppo piccola se eseguita su un computer in cui il tipo di carattere del sistema è Tahoma a 12 punti.  Gli elementi di testo, ad esempio titoli, menu, contenuti delle caselle di testo e così via, verranno visualizzati più in piccolo che nelle altre applicazioni.  Inoltre, le dimensioni degli elementi dell'interfaccia utente contenenti testo, ad esempio la barra del titolo, i menu e molti controlli, dipendono dal tipo di carattere usato.  In questo esempio, tali elementi appariranno anche relativamente più piccoli.  
  
 Una situazione analoga si verifica quando un'applicazione è progettata per una determinata risoluzione dello schermo.  La risoluzione dello schermo più comune è di 96 punti per pollice \(dpi\), ma sono sempre più diffuse risoluzioni dello schermo più elevate che supportano 120, 133, 170 dpi e oltre.  Senza regolazione, un'applicazione, soprattutto una con molti elementi grafici, progettata per un'unica risoluzione apparirà troppo grande o troppo piccola se eseguita con un'altra risoluzione.  
  
 Il ridimensionamento automatico cerca di risolvere questi problemi ridimensionando automaticamente il form e i controlli figlio in base alle dimensioni del carattere o risoluzione dello schermo relativa.  Per supportare il ridimensionamento automatico delle finestre di dialogo, il sistema operativo Windows usa un'unità di misura relativa, chiamata DLU.  Una DLU si basa sul tipo di carattere del sistema e la relazione con i pixel può essere determinata attraverso la funzione `GetDialogBaseUnits` di Win32 SDK.  Quando un utente cambia il tema usato da Windows, tutte le finestre di dialogo vengono automaticamente adattate di conseguenza.  Inoltre,  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] supporta il ridimensionamento automatico basato sia sulla risoluzione dello schermo che sul tipo di carattere del sistema predefinito.  Facoltativamente, il ridimensionamento automatico può essere disabilitato in un'applicazione.  
  
## Supporto originale per il ridimensionamento automatico  
 Le versioni 1.0 e 1.1 di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] supportavano un tipo di ridimensionamento automatico semplice, che dipendeva dal tipo di carattere predefinito di Windows usato per l'interfaccia utente, rappresentato dal valore **DEFAULT\_GUI\_FONT** di Win32 SDK.  Questo tipo di carattere in genere viene modificato solo quando cambia la risoluzione dello schermo.  Per implementare il ridimensionamento automatico, veniva usato il meccanismo seguente:  
  
1.  In fase di progettazione, la proprietà <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> \(ora deprecata\) veniva impostata sull'altezza e sulla larghezza del tipo di carattere del sistema predefinito sul computer dello sviluppatore.  
  
2.  In fase di esecuzione, il tipo di carattere del sistema predefinito del computer dell'utente veniva usato per inizializzare la proprietà <xref:System.Windows.Forms.Control.Font%2A> della classe <xref:System.Windows.Forms.Form>.  
  
3.  Prima di visualizzare il form, veniva chiamato il metodo <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A> per ridimensionarlo.  Questo metodo calcolava le dimensioni per la scalabilità relative in base a <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> e <xref:System.Windows.Forms.Control.Font%2A>, quindi chiamava il metodo <xref:System.Windows.Forms.Control.Scale%2A> per ridimensionare effettivamente il form e gli elementi figlio.  
  
4.  Il valore di <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> veniva aggiornato in modo che le chiamate successive a <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A> non ridimensionassero progressivamente il form.  
  
 Anche se questo meccanismo era sufficiente per la maggior parte degli scopi, tuttavia aveva i seguenti limiti:  
  
-   Poiché la proprietà <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> rappresenta le dimensioni del carattere di base come valori integrali, si verificano errori di arrotondamento che diventano evidenti quando un form viene visualizzato in sequenza in più risoluzioni.  
  
-   Il ridimensionamento automatico era implementato solo nella classe <xref:System.Windows.Forms.Form> e non nella classe <xref:System.Windows.Forms.ContainerControl>.  Di conseguenza, i controlli utente venivano ridimensionati in modo corretto solo quando il controllo utente era progettato con la stessa risoluzione del form e veniva inserito nel form in fase di progettazione.  
  
-   I form e i controlli figlio potevano essere progettati simultaneamente da più sviluppatori solo se le risoluzioni dei computer erano le stesse.  Allo stesso modo, l'ereditarietà di un form dipendeva dalla risoluzione associata al form padre.  
  
-   Non è compatibile con i nuovi gestori di layout introdotti con [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versione 2.0, ad esempio <xref:System.Windows.Forms.FlowLayoutPanel> e <xref:System.Windows.Forms.TableLayoutPanel>.  
  
-   Non supportava il ridimensionamento basato direttamente sulla risoluzione dello schermo, necessario per la compatibilità con [!INCLUDE[compact](../../../includes/compact-md.md)].  
  
 Anche se questo meccanismo è ancora presente in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versione 2.0 per mantenere la compatibilità con le versioni precedenti, è stato sostituito da un meccanismo di ridimensionamento più affidabile, descritto di seguito.  Di conseguenza, <xref:System.Windows.Forms.Form.AutoScale%2A>, <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A>, <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> e alcuni overload di <xref:System.Windows.Forms.Control.Scale%2A> sono contrassegnati come obsoleti.  
  
> [!NOTE]
>  È possibile eliminare senza problemi i riferimenti a questi membri quando si aggiorna il codice legacy per [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versione 2.0.  
  
## Supporto corrente per il ridimensionamento automatico  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] versione 2.0 supera i precedenti limiti introducendo le seguenti modifiche al ridimensionamento automatico di Windows Form:  
  
-   Il supporto di base per il ridimensionamento è stato spostato nella classe <xref:System.Windows.Forms.ContainerControl> in modo che i form, i controlli compositi nativi e i controlli utente ricevano tutti lo stesso supporto.  Sono stati aggiunti i nuovi membri <xref:System.Windows.Forms.ContainerControl.AutoScaleFactor%2A>, <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>, <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> e <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>.  
  
-   La classe <xref:System.Windows.Forms.Control> dispone anche di alcuni nuovi membri che le consentono di partecipare al ridimensionamento e di supportare il ridimensionamento misto nello stesso form.  In particolare i membri <xref:System.Windows.Forms.Control.Scale%2A>, <xref:System.Windows.Forms.Control.ScaleChildren%2A> e <xref:System.Windows.Forms.Control.GetScaledBounds%2A> supportano il ridimensionamento.  
  
-   È stato aggiunto il supporto per il ridimensionamento basato sulla risoluzione dello schermo, come complemento del supporto per il tipo di carattere del sistema, definito dall'enumerazione <xref:System.Windows.Forms.AutoScaleMode>.  Questa modalità è compatibile con il ridimensionamento automatico supportato dal [!INCLUDE[compact](../../../includes/compact-md.md)] e semplifica la migrazione delle applicazioni.  
  
-   È stata aggiunta all'implementazione del ridimensionamento automatico la compatibilità con i gestori di layout, ad esempio <xref:System.Windows.Forms.FlowLayoutPanel> e <xref:System.Windows.Forms.TableLayoutPanel>.  
  
-   I fattori di ridimensionamento sono ora rappresentati come valori a virgola mobile, in genere con la struttura <xref:System.Drawing.SizeF>, praticamente eliminando gli errori di arrotondamento.  
  
> [!CAUTION]
>  Non sono supportate combinazioni arbitrarie di DPI e modalità di ridimensionamento dei tipi di carattere.  Anche se è possibile ridimensionare un controllo utente con una sola modalità \(ad esempio, DPI\) e inserirlo in un form con un'altra modalità \(Font\) senza problemi, tuttavia, se si combinano un form di base in una modalità e un form derivato in un'altra, è possibile che si verifichino risultati imprevisti.  
  
### Uso del ridimensionamento automatico  
 Windows Form usa ora la seguente logica per ridimensionare automaticamente i form e i relativi contenuti:  
  
1.  In fase di progettazione, ogni <xref:System.Windows.Forms.ContainerControl> registra la modalità di ridimensionamento e la risoluzione corrente rispettivamente in <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> e <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>.  
  
2.  In fase di esecuzione, la risoluzione effettiva viene archiviata nella proprietà <xref:System.Windows.Forms.ContainerControl.CurrentAutoScaleDimensions%2A>.  La proprietà <xref:System.Windows.Forms.ContainerControl.AutoScaleFactor%2A> calcola in modo dinamico il rapporto tra la risoluzione di ridimensionamento in fase di esecuzione e in fase di progettazione.  
  
3.  Quando il form viene caricato, se i valori di <xref:System.Windows.Forms.ContainerControl.CurrentAutoScaleDimensions%2A> e <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> sono diversi, viene chiamato il metodo <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A> per ridimensionare il controllo e gli elementi figlio.  Questo metodo sospende il layout e chiama il metodo <xref:System.Windows.Forms.Control.Scale%2A> per eseguire il ridimensionamento effettivo.  Successivamente, il valore di <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> viene aggiornato per evitare il ridimensionamento progressivo.  
  
4.  <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A> viene richiamato automaticamente anche nelle situazioni seguenti:  
  
    -   In risposta all'evento <xref:System.Windows.Forms.Control.OnFontChanged%2A> se la modalità di ridimensionamento è <xref:System.Windows.Forms.AutoScaleMode>.  
  
    -   Quando il layout del controllo contenitore viene ripristinato e viene rilevata una modifica nelle proprietà <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> o <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>.  
  
    -   Come accennato in precedenza, quando è in corso il ridimensionamento di un <xref:System.Windows.Forms.ContainerControl> padre.  Ogni controllo contenitore è responsabile del ridimensionamento degli elementi figlio con i propri fattori di scala e non con quello del contenitore padre.  
  
5.  I controlli figlio possono modificare il comportamento di ridimensionamento in più modi:  
  
    -   È possibile eseguire l'override della proprietà <xref:System.Windows.Forms.Control.ScaleChildren%2A> per determinare se i controlli figlio devono essere ridimensionati.  
  
    -   È possibile eseguire l'override del metodo <xref:System.Windows.Forms.Control.GetScaledBounds%2A> per regolare i limiti in base a cui il controllo viene ridimensionato, ma non la logica di ridimensionamento.  
  
    -   È possibile eseguire l'override del metodo <xref:System.Windows.Forms.Control.ScaleControl%2A> per cambiare la logica di ridimensionamento per il controllo corrente.  
  
## Vedere anche  
 <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>   
 <xref:System.Windows.Forms.Control.Scale%2A>   
 <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>   
 <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>   
 [Rendering dei controlli con stili visivi](../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)   
 [Procedura: migliorare le prestazioni evitando l'adattamento automatico](../../../docs/framework/winforms/advanced/how-to-improve-performance-by-avoiding-automatic-scaling.md)