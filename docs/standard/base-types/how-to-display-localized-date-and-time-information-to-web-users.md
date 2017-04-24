---
title: "Procedura: visualizzare le informazioni su data e ora localizzate agli utenti del Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "visualizzazione di dati relativi a data e ora"
  - "formattazione [.NET Framework], date"
  - "formattazione [.NET Framework], dati localizzati"
  - "localizzazione [.NET Framework], visualizzazioni di data e ora"
  - "data localizzata (visualizzazioni) [.NET Framework]"
  - "analisi delle stringhe [.NET Framework], stringhe di data e ora"
ms.assetid: 377fe93c-32be-421a-a30a-be639a46ede8
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: visualizzare le informazioni su data e ora localizzate agli utenti del Web
Poiché una pagina Web può essere visualizzata in qualsiasi parte del mondo, le operazioni che analizzano e formattano valori di data e ora non devono basarsi su un formato predefinito \(quasi sempre corrispondente al formato delle impostazioni cultura locali del server Web\) in caso di interazione con l'utente.  I Web Form che gestiscono le stringhe di data e ora immesse dall'utente devono invece analizzare tali stringhe utilizzando le impostazioni cultura preferite dell'utente.  Analogamente, i valori di data e ora devono essere visualizzati in un formato conforme alle impostazioni cultura dell'utente.  In questo argomento viene illustrato come eseguire queste operazioni.  
  
### Per analizzare le stringhe di data e ora immesse dall'utente  
  
1.  Determinare se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> è compilata.  In caso contrario, andare al passaggio 6.  
  
2.  Se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A> è compilata, recuperarne il primo elemento.  Il primo elemento indica la lingua e l'area predefinite o preferite dell'utente.  
  
3.  Creare un'istanza di un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura preferite dell'utente chiamando il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName>.  
  
4.  Chiamare il metodo `TryParse` o il metodo `Parse` del tipo <xref:System.DateTime> o <xref:System.DateTimeOffset> per provare la conversione.  Utilizzare un overload del metodo `TryParse` o del metodo `Parse` con un parametro `provider` e passare uno degli elementi seguenti:  
  
    -   L'oggetto <xref:System.Globalization.CultureInfo> creato al passaggio 3.  
  
    -   L'oggetto <xref:System.Globalization.DateTimeFormatInfo> restituito dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> dell'oggetto <xref:System.Globalization.CultureInfo> creato al passaggio 3.  
  
5.  Se la conversione non riesce, ripetere i passaggi da 2 a 4 per ogni elemento rimanente nella matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A>.  
  
6.  Se la conversione ancora non riesce o se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A> è vuota, analizzare la stringa utilizzando le impostazioni cultura inglese, restituita dalla proprietà <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  
  
### Per analizzare la data e l'ora locale della richiesta dell'utente  
  
1.  Aggiungere un controllo <xref:System.Web.UI.WebControls.HiddenField> a un Web Form.  
  
2.  Creare una funzione JavaScript che gestisce l'evento `onClick` di un pulsante `Submit` scrivendo la data e l'ora corrente e l'offset del fuso orario locale rispetto all'ora UTC \(Coordinated Universal Time\) nella proprietà <xref:System.Web.UI.WebControls.HiddenField.Value%2A>.  Utilizzare un delimitatore, ad esempio un punto e virgola, per separare i due componenti della stringa.  
  
3.  Utilizzare l'evento <xref:System.Web.UI.Control.PreRender> del Web Form per inserire la funzione nel flusso di output HTML passando il testo dello script al metodo <xref:System.Web.UI.ClientScriptManager.RegisterClientScriptBlock%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=fullName>.  
  
4.  Connettere il gestore eventi all'evento `onClick` del pulsante `Submit` specificando il nome della funzione JavaScript per l'attributo `OnClientClick` del pulsante `Submit`.  
  
5.  Creare un gestore per l'evento <xref:System.Web.UI.WebControls.Button.Click> del pulsante `Submit`.  
  
6.  Nel gestore eventi determinare se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> è compilata.  In caso contrario, andare al passaggio 14.  
  
7.  Se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A> è compilata, recuperarne il primo elemento.  Il primo elemento indica la lingua e l'area predefinite o preferite dell'utente.  
  
8.  Creare un'istanza di un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura preferite dell'utente chiamando il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName>.  
  
9. Passare la stringa assegnata alla proprietà <xref:System.Web.UI.WebControls.HiddenField.Value%2A> al metodo <xref:System.String.Split%2A> per memorizzare la rappresentazione di stringa della data e ora locale dell'utente e la rappresentazione di stringa dell'offset del fuso orario locale dell'utente in elementi di matrice separati.  
  
10. Chiamare il metodo <xref:System.DateTime.Parse%2A?displayProperty=fullName> o <xref:System.DateTime.TryParse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%2CSystem.DateTime%40%29?displayProperty=fullName> per convertire la data e l'ora della richiesta dell'utente in un valore <xref:System.DateTime>.  Utilizzare un overload del metodo con un parametro `provider` e passare uno degli elementi seguenti:  
  
    -   L'oggetto <xref:System.Globalization.CultureInfo> creato al passaggio 8.  
  
    -   L'oggetto <xref:System.Globalization.DateTimeFormatInfo> restituito dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> dell'oggetto <xref:System.Globalization.CultureInfo> creato al passaggio 8.  
  
11. Se l'operazione di analisi al passaggio 10 non riesce, procedere con il passaggio 13.  In caso contrario, chiamare il metodo <xref:System.UInt32.Parse%28System.String%29?displayProperty=fullName> per convertire la rappresentazione di stringa dell'offset del fuso orario dell'utente in un valore intero.  
  
12. Creare un'istanza di un oggetto <xref:System.DateTimeOffset> che rappresenta l'ora locale dell'utente chiamando il costruttore <xref:System.DateTimeOffset.%23ctor%28System.DateTime%2CSystem.TimeSpan%29?displayProperty=fullName>.  
  
13. Se la conversione al passaggio 10 non riesce, ripetere i passaggi da 7 a 12 per ogni elemento rimanente nella matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A>.  
  
14. Se la conversione ancora non riesce o se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A> è vuota, analizzare la stringa utilizzando le impostazioni cultura inglese, restituita dalla proprietà <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  Ripetere quindi i passaggi da 7 a 12.  
  
 Il risultato è un oggetto <xref:System.DateTimeOffset> che rappresenta l'ora locale dell'utente della pagina Web.  È quindi possibile determinare l'ora UTC equivalente chiamando il metodo <xref:System.DateTimeOffset.ToUniversalTime%2A>.  È anche possibile determinare la data e l'ora equivalente sul server Web chiamando il metodo <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=fullName> e passando il valore <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> come fuso orario in cui convertire l'ora.  
  
## Esempio  
 Nell'esempio riportato di seguito sono contenuti sia l'origine che il codice HTML per un Web Form ASP.NET che richiede all'utente l'immissione di un valore di data e ora.  Uno script sul lato client scrive anche informazioni sulla data e l'ora locale della richiesta dell'utente e sull'offset del fuso orario dell'utente rispetto all'ora UTC in un campo nascosto.  Queste informazioni vengono quindi analizzate dal server che restituisce una pagina Web con l'input dell'utente.  Nella pagina vengono visualizzate anche la data e l'ora della richiesta dell'utente utilizzando l'ora locale dell'utente, l'ora del server e l'ora UTC.  
  
 <!-- TODO: review snippet reference [!code-csharp[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/cs/GetDateInfo.aspx#1)]  -->
 <!-- TODO: review snippet reference [!code-vb[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/vb/GetDateInfo.aspx#1)]  -->  
  
 Lo script sul lato client chiama il metodo JavaScript `toLocaleString`.  e produce una stringa che rispetta le convenzioni di formattazione delle impostazioni locali dell'utente, la cui analisi viene in genere eseguita correttamente sul server.  
  
 La proprietà <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> viene compilata con i nomi delle impostazioni cultura contenuti nelle intestazioni `Accept-Language` incluse in una richiesta HTTP.  Non tutti i browser, tuttavia, includono intestazioni `Accept-Language` nelle rispettive richieste e inoltre le intestazioni possono essere del tutto rimosse dall'utente.  Per questo motivo è importante disporre di impostazioni cultura di fallback durante l'analisi dell'input dell'utente.  In genere le impostazioni cultura di fallback corrispondono alla lingua inglese restituita da <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  Gli utenti possono anche specificare i nomi delle impostazioni cultura in una casella di testo di Internet Explorer, rischiando tuttavia di inserire nomi non validi.  È pertanto indispensabile utilizzare la gestione delle eccezioni durante la creazione di un'istanza di un oggetto <xref:System.Globalization.CultureInfo>.  
  
 Quando viene recuperata da una richiesta HTTP inviata da Internet Explorer, la matrice <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> viene compilata in base alla preferenza dell'utente.  Il primo elemento della matrice contiene il nome delle impostazioni cultura\/area primarie dell'utente.  Se la matrice contiene elementi aggiuntivi, Internet Explorer assegna loro arbitrariamente un identificatore di qualità, separato dal nome delle impostazioni cultura con un punto e virgola.  Una voce per le impostazioni cultura fr\-FR può ad esempio avere il formato `fr-FR;q=0.7`.  
  
 Nell'esempio viene chiamato il costruttore <xref:System.Globalization.CultureInfo.%23ctor%2A> il cui parametro `useUserOverride` è impostato su `false` per creare un nuovo oggetto <xref:System.Globalization.CultureInfo>.  In questo modo, se il nome delle impostazioni cultura è il nome predefinito sul server, il nuovo oggetto <xref:System.Globalization.CultureInfo> creato dal costruttore della classe contiene le impostazioni cultura predefinite e non riflette le impostazioni sottoposte a override mediante l'applicazione **Opzioni internazionali e della lingua** del server.  È improbabile che i valori delle impostazioni sottoposte a override sul server si trovino sul sistema dell'utente o vengano riflessi nell'input dell'utente.  
  
 Poiché in questo esempio vengono analizzate due rappresentazioni di stringa di una data e di un'ora \(una immessa dall'utente, l'altra memorizzata nel campo nascosto\), vengono definiti in anticipo gli oggetti <xref:System.Globalization.CultureInfo> che potrebbero essere richiesti.  Viene creata una matrice di oggetti <xref:System.Globalization.CultureInfo> ovvero una matrice maggiore del numero di elementi restituiti dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName>.  Viene quindi creata un'istanza di un oggetto <xref:System.Globalization.CultureInfo> per ogni stringa di lingua\/area, nonché un'istanza di un oggetto <xref:System.Globalization.CultureInfo> che rappresenta <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  
  
 Il codice può chiamare il metodo <xref:System.DateTime.Parse%2A> o <xref:System.DateTime.TryParse%2A> per convertire la rappresentazione di stringa dell'utente di una data e ora in un valore <xref:System.DateTime>.  Chiamate ripetute a un metodo di analisi potrebbero richiedere una singola operazione di analisi.  Di conseguenza, il metodo <xref:System.DateTime.TryParse%2A> è preferibile in quanto restituisce `false` se un'operazione di analisi non riesce.  Al contrario, la gestione delle eccezioni ripetute che possono essere generate dal metodo <xref:System.DateTime.Parse%2A> può rappresentare una proposta piuttosto dispendiosa in un'applicazione Web.  
  
## Compilazione del codice  
 Per compilare il codice, creare una pagina Web [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] senza code\-behind.  Copiare quindi l'esempio nella pagina Web in modo che sostituisca tutto il code\-behind.  La pagina Web [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] deve contenere i controlli seguenti:  
  
-   Un controllo <xref:System.Web.UI.WebControls.Label> al quale non viene fatto riferimento nel codice.  Impostarne la proprietà <xref:System.Web.UI.WebControls.TextBox.Text%2A> su "Immettere un numero:".  
  
-   Un controllo <xref:System.Web.UI.WebControls.TextBox> denominato `DateString`.  
  
-   Un controllo <xref:System.Web.UI.WebControls.Button> denominato `OKButton`.  Impostarne la proprietà <xref:System.Web.UI.WebControls.Button.Text%2A> su "OK".  
  
-   Un controllo <xref:System.Web.UI.WebControls.HiddenField> denominato `DateInfo`.  
  
## Sicurezza di .NET Framework  
 Per impedire che un utente inserisca uno script nel flusso HTML, l'input dell'utente non deve essere mai restituito direttamente nella risposta del server.  Tale input deve essere invece codificato utilizzando il metodo <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=fullName>.  
  
## Vedere anche  
 [Esecuzione di operazioni di formattazione](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [Stringhe di formato di data e ora standard](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)   
 [Stringhe di formato di data e ora personalizzato](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)   
 [Analisi delle stringhe di data e ora](../../../docs/standard/base-types/parsing-datetime.md)