---
title: "PrintForm Component (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "PrintForm component [Visual Basic]"
ms.assetid: 03de98b8-b54c-4764-91d7-83c64e974750
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# PrintForm Component (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> per [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente di stampare un'immagine di un Windows Form in fase di esecuzione. Il relativo comportamento sostituisce quello del metodo `PrintForm` nelle versioni precedenti di Visual Basic.  
  
 I controlli PowerPacks non sono più inclusi in Visual Studio, ma è possibile scaricarli dall'[Area download](http://www.microsoft.com/en-us/download/details.aspx?id=25169).  
  
## Cenni preliminari sul componente PrintForm  
 Uno scenario comune per Windows Form consiste nel creare un form che è formattato in modo simile a un modulo cartaceo o un report, quindi nello stampare un'immagine del form. Sebbene sia possibile usare un componente <xref:System.Drawing.Printing.PrintDocument> a tale scopo, ciò richiederebbe una grande quantità di codice. Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> consente di stampare un'immagine di un form in una stampante, una finestra di anteprima di stampa o un file senza usare un componente <xref:System.Drawing.Printing.PrintDocument>.  
  
 Il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> è disponibile nella scheda **Visual Basic PowerPacks** della **casella degli strumenti**. Quando viene trascinato in un form, è visualizzato nella barra dei componenti, la piccola area sotto il bordo inferiore del form. Quando si seleziona il componente, le proprietà che ne definiscono il comportamento possono essere impostate nella finestra **Proprietà**. Tutte queste proprietà possono essere impostate anche nel codice. È inoltre possibile creare un'istanza del componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> nel codice senza aggiungere il componente in fase di progettazione.  
  
 Quando si stampa un form, vengono stampati tutti gli elementi nell'area client del form. Sono inclusi tutti i controlli e qualsiasi testo o immagine disegnata nel form mediante i metodi grafici. Per impostazione predefinita, la barra del titolo del form, le barre di scorrimento e il bordo non vengono stampati. Inoltre, per impostazione predefinita, il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> stampa solo la parte visibile del form. Ad esempio, se l'utente ridimensiona il form in fase di esecuzione, vengono stampati solo i controlli e la grafica attualmente visibili.  
  
 La stampante predefinita usata dal componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> è determinata dalle impostazioni del Pannello di controllo del sistema operativo.  
  
 Una volta avviata la stampa, viene visualizzata una finestra di dialogo di stampa <xref:System.Drawing.Printing.PrintDocument> standard. Questa finestra di dialogo consente agli utenti di annullare il processo di stampa.  
  
### Metodi, proprietà ed eventi principali  
 Il metodo principale del componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> è il metodo <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>, che stampa un'immagine del form in una stampante, una finestra di anteprima di stampa o un file. Sono disponibili due versioni del metodo <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>:  
  
-   Una versione di base senza parametri: `Print()`  
  
-   Una versione di overload con parametri che specificano il comportamento di stampa: `Print(printForm As Form, printFormOption As PrintOption)`  
  
     Il parametro `PrintOption` del metodo di overload determina l'implementazione sottostante usata per stampare il form, se vengono stampati la barra del titolo, le barre di scorrimento e il bordo e se vengono stampate le parti scorrevoli del form.  
  
 La proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> è una proprietà chiave del componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>. Questa proprietà determina se l'output viene inviato a una stampante, visualizzato in una finestra di anteprima di stampa o salvato come file EPS \(Encapsulated PostScript\). Se la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> è impostata su <xref:System.Drawing.Printing.PrintAction>, la proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A> specifica il percorso e il nome del file.  
  
 La proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrinterSettings%2A> fornisce l'accesso a un oggetto <xref:System.Drawing.Printing.PrintDocument.PrinterSettings%2A> sottostante, che consente di specificare impostazioni quali la stampante da usare e il numero di copie da stampare. È inoltre possibile eseguire query sulle funzionalità della stampante, ad esempio il supporto per il colore o duplex. Questa proprietà non viene visualizzata nella finestra **Proprietà**: è accessibile solo dal codice.  
  
 La proprietà <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Form%2A> viene usata per specificare il form da stampare quando si richiama il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> a livello di codice. Se il componente viene aggiunto a un form in fase di progettazione, tale form è quello predefinito.  
  
 Gli eventi principali per il componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> includono i seguenti:  
  
-   Evento <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.BeginPrint>. Si verifica quando viene chiamato il metodo <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A> e prima della stampa della prima pagina del documento.  
  
-   Evento <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.EndPrint>. Si verifica dopo la stampa dell'ultima pagina.  
  
-   Evento <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.QueryPageSettings>. Si verifica immediatamente prima della stampa di ogni pagina.  
  
### Note  
 Se un form contiene testo o grafica disegnati mediante i metodi <xref:System.Drawing.Graphics>, usare il metodo <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A> \(`Print()`\) di base per stamparlo. In alcuni sistemi operativi potrebbe non essere eseguito il rendering della grafica quando viene usato il metodo di overload <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>.  
  
 Se la larghezza di un form è maggiore della larghezza della carta della stampante, il lato destro del form potrebbe essere troncato. Quando si progettano moduli per la stampa, assicurarsi che il form sia contenuto su carta in formato standard.  
  
## Esempio  
 Nell'esempio seguente viene illustrato un uso comune del componente <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>.  
  
```  
' Visual Basic. Dim pf As New PrintForm pf.Form = Me pf.PrintAction = PrintToPrinter pf.Print()  
```  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>   
 [Procedura: stampare un form utilizzando il componente PrintForm](../../../visual-basic/developing-apps/printing/how-to-print-a-form-by-using-the-printform-component.md)   
 [Procedura: stampare l'area client di un form](../../../visual-basic/developing-apps/printing/how-to-print-the-client-area-of-a-form.md)   
 [Procedura: stampare aree client e non client di un form](../../../visual-basic/developing-apps/printing/how-to-print-client-and-non-client-areas-of-a-form.md)   
 [Procedura: stampare un form scorrevole](../../../visual-basic/developing-apps/printing/how-to-print-a-scrollable-form.md)