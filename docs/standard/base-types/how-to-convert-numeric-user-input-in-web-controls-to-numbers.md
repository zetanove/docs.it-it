---
title: "Procedura: convertire in numeri l&#39;input numerico dell&#39;utente nei controlli Web | Microsoft Docs"
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
  - "conversione dell'input utente numerico in numero"
  - "formattazione [.NET Framework], numeri"
  - "numeri (formattazione) [.NET Framework]"
  - "numeri [.NET Framework], conversione dell'input utente numerico in numero"
  - "stringhe di formato numerico [.NET Framework]"
  - "analisi delle stringhe [.NET Framework], stringhe numeriche"
ms.assetid: f27ddfb8-7479-4b79-8879-02a3bd8402d4
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: convertire in numeri l&#39;input numerico dell&#39;utente nei controlli Web
Poiché una pagina Web può essere visualizzata in qualsiasi parte del mondo, gli utenti possono inserire dati numerici in un controllo <xref:System.Web.UI.WebControls.TextBox> utilizzando un numero quasi illimitato di formati.  Di conseguenza, è molto importante determinare le impostazioni locali e le impostazioni cultura dell'utente della pagina Web,  in modo da applicarne le convenzioni di formattazione quando si analizza l'input dell'utente.  
  
### Per convertire l'input numerico da un controllo Web TextBox in un numero  
  
1.  Determinare se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> è compilata.  In caso contrario, andare al passaggio 6.  
  
2.  Se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A> è compilata, recuperarne il primo elemento.  Il primo elemento indica la lingua e l'area predefinite o preferite dell'utente.  
  
3.  Creare un'istanza di un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura preferite dell'utente chiamando il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName>.  
  
4.  Chiamare `TryParse` o il metodo `Parse` del tipo numerico nel quale si desidera convertire l'input dell'utente.  Utilizzare un overload del metodo `TryParse` o del metodo `Parse` con un parametro `provider` e passare uno degli elementi seguenti:  
  
    -   L'oggetto <xref:System.Globalization.CultureInfo> creato al passaggio 3.  
  
    -   L'oggetto <xref:System.Globalization.NumberFormatInfo> restituito dalla proprietà <xref:System.Globalization.CultureInfo.NumberFormat%2A> dell'oggetto <xref:System.Globalization.CultureInfo> creato al passaggio 3.  
  
5.  Se la conversione non riesce, ripetere i passaggi da 2 a 4 per ogni elemento rimanente nella matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A>.  
  
6.  Se la conversione ancora non riesce o se la matrice di stringhe restituita dalla proprietà <xref:System.Web.HttpRequest.UserLanguages%2A> è vuota, analizzare la stringa utilizzando le impostazioni cultura inglese, restituita dalla proprietà <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio seguente è riportata la pagina code\-behind completa per un Web Form che richiede all'utente di immettere un valore numerico in un controllo <xref:System.Web.UI.WebControls.TextBox> e lo converte in un numero.  Tale numero viene quindi raddoppiato e visualizzato utilizzando le stesse regole di formattazione dell'input originale.  
  
 [!code-csharp[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/cs/NumericUserInput1.aspx.cs#1)]
 [!code-vb[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/vb/NumericUserInput1.aspx.vb#1)]  
  
 La proprietà <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> viene compilata con i nomi delle impostazioni cultura contenuti nelle intestazioni `Accept-Language` incluse in una richiesta HTTP.  Non tutti i browser, tuttavia, includono intestazioni `Accept-Language` nelle rispettive richieste e inoltre le intestazioni possono essere del tutto rimosse dall'utente.  Per questo motivo è importante disporre di impostazioni cultura di fallback durante l'analisi dell'input dell'utente.  In genere le impostazioni cultura di fallback corrispondono alla lingua inglese restituita da <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.  Gli utenti possono anche specificare i nomi delle impostazioni cultura in una casella di testo di Internet Explorer, rischiando tuttavia di inserire nomi non validi.  È pertanto indispensabile utilizzare la gestione delle eccezioni durante la creazione di un'istanza di un oggetto <xref:System.Globalization.CultureInfo>.  
  
 Quando viene recuperata da una richiesta HTTP inviata da Internet Explorer, la matrice <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> viene compilata in base alla preferenza dell'utente.  Il primo elemento della matrice contiene il nome delle impostazioni cultura\/area primarie dell'utente.  Se la matrice contiene elementi aggiuntivi, Internet Explorer assegna loro arbitrariamente un identificatore di qualità, separato dal nome delle impostazioni cultura con un punto e virgola.  Una voce per le impostazioni cultura fr\-FR può ad esempio avere il formato `fr-FR;q=0.7`.  
  
 Nell'esempio viene chiamato il costruttore <xref:System.Globalization.CultureInfo.%23ctor%2A> il cui parametro `useUserOverride` è impostato su `false` per creare un nuovo oggetto <xref:System.Globalization.CultureInfo>.  In questo modo, se il nome delle impostazioni cultura è il nome predefinito sul server, il nuovo oggetto <xref:System.Globalization.CultureInfo> creato dal costruttore della classe contiene le impostazioni cultura predefinite e non riflette le impostazioni sottoposte a override mediante l'applicazione **Opzioni internazionali e della lingua** del server.  È improbabile che i valori delle impostazioni sottoposte a override sul server si trovino sul sistema dell'utente o vengano riflessi nell'input dell'utente.  
  
 Il codice può chiamare il metodo `Parse` o `TryParse` del tipo numerico nel quale verrà convertito l'input dell'utente.  Chiamate ripetute a un metodo di analisi potrebbero richiedere una singola operazione di analisi.  Di conseguenza, il metodo `TryParse` è preferibile in quanto restituisce `false` se un'operazione di analisi non riesce.  Al contrario, la gestione delle eccezioni ripetute che possono essere generate dal metodo `Parse` può rappresentare una proposta piuttosto dispendiosa in un'applicazione Web.  
  
## Compilazione del codice  
 Per compilare il codice, copiarlo in una pagina code\-behind di [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] in modo che sostituisca tutto il codice esistente.  La pagina Web [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] deve contenere i controlli seguenti:  
  
-   Un controllo <xref:System.Web.UI.WebControls.Label> al quale non viene fatto riferimento nel codice.  Impostarne la proprietà <xref:System.Web.UI.WebControls.TextBox.Text%2A> su "Immettere un numero:".  
  
-   Un controllo <xref:System.Web.UI.WebControls.TextBox> denominato `NumericString`.  
  
-   Un controllo <xref:System.Web.UI.WebControls.Button> denominato `OKButton`.  Impostarne la proprietà <xref:System.Web.UI.WebControls.Button.Text%2A> su "OK".  
  
 Modificare il nome della classe da `NumericUserInput` nel nome della classe definita dall'attributo `Inherits` della direttiva `Page` della pagina di [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)].  Modificare il nome del riferimento all'oggetto `NumericInput` nel nome definito dall'attributo `id` del tag `form` della pagina di [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)].  
  
## Sicurezza di .NET Framework  
 Per impedire che un utente inserisca uno script nel flusso HTML, l'input dell'utente non deve essere mai restituito direttamente nella risposta del server.  Tale input deve essere invece codificato utilizzando il metodo <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=fullName>.  
  
## Vedere anche  
 [Esecuzione di operazioni di formattazione](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [Analisi di stringhe numeriche](../../../docs/standard/base-types/parsing-numeric.md)