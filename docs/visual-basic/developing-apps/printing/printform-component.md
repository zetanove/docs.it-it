---
title: Componente PrintForm (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- PrintForm component [Visual Basic]
ms.assetid: 03de98b8-b54c-4764-91d7-83c64e974750
caps.latest.revision: 19
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f0c51ef0131c874ed33af7a19f9145a790d14ade
ms.lasthandoff: 03/13/2017

---
# <a name="printform-component-visual-basic"></a>Componente PrintForm (Visual Basic)
Il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente di stampare un'immagine di un Windows Form in fase di esecuzione.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> Il relativo comportamento sostituisce quello del metodo `PrintForm` nelle versioni precedenti di Visual Basic.  
  
 I controlli PowerPacks non sono più inclusi in Visual Studio, ma è possibile scaricarli dall' [Area download](http://www.microsoft.com/en-us/download/details.aspx?id=25169).  
  
## <a name="printform-component-overview"></a>Cenni preliminari sul componente PrintForm  
 Uno scenario comune per Windows Form consiste nel creare un form che è formattato in modo simile a un modulo cartaceo o un report, quindi nello stampare un'immagine del form. Sebbene sia possibile utilizzare un <xref:System.Drawing.Printing.PrintDocument>componente a tale scopo, richiederebbe una grande quantità di codice.</xref:System.Drawing.Printing.PrintDocument> Il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente consente di stampare un'immagine di un form a una stampante, a una finestra di anteprima di stampa o in un file senza utilizzare un <xref:System.Drawing.Printing.PrintDocument>component.</xref:System.Drawing.Printing.PrintDocument> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 Il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente si trova nel **Visual Basic Power Packs** scheda della finestra di **della casella degli strumenti**.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> Quando viene trascinato in un form, è visualizzato nella barra dei componenti, la piccola area sotto il bordo inferiore del form. Quando si seleziona il componente, le proprietà che ne definiscono il comportamento possono essere impostate nella finestra **Proprietà** . Tutte queste proprietà possono essere impostate anche nel codice. È inoltre possibile creare un'istanza di <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente nel codice senza aggiungere il componente in fase di progettazione.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 Quando si stampa un form, vengono stampati tutti gli elementi nell'area client del form. Sono inclusi tutti i controlli e qualsiasi testo o immagine disegnata nel form mediante i metodi grafici. Per impostazione predefinita, la barra del titolo del form, le barre di scorrimento e il bordo non vengono stampati. Inoltre, per impostazione predefinita, il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente stampa solo la parte visibile del form.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> Ad esempio, se l'utente ridimensiona il form in fase di esecuzione, vengono stampati solo i controlli e la grafica attualmente visibili.  
  
 La stampante predefinita utilizzata per il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente è determinato dalle impostazioni del Pannello di controllo del sistema operativo.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
 Una volta iniziata la stampa, uno standard <xref:System.Drawing.Printing.PrintDocument>viene visualizzata la finestra di dialogo Stampa.</xref:System.Drawing.Printing.PrintDocument> Questa finestra di dialogo consente agli utenti di annullare il processo di stampa.  
  
### <a name="key-methods-properties-and-events"></a>Metodi, proprietà ed eventi principali  
 Il metodo principale del <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente è il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>(metodo), che consente di stampare un'immagine del form su una stampante, finestra di anteprima di stampa o un file.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> Esistono due versioni di <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>metodo:</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>  
  
-   Versione di base senza parametri:`Print()`  
  
-   Versione di overload con parametri che specificano il comportamento di stampa:`Print(printForm As Form, printFormOption As PrintOption)`  
  
     Il parametro `PrintOption` del metodo di overload determina l'implementazione sottostante usata per stampare il form, se vengono stampati la barra del titolo, le barre di scorrimento e il bordo e se vengono stampate le parti scorrevoli del form.  
  
 Il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>è una proprietà chiave del <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>component.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> Questa proprietà determina se l'output viene inviato a una stampante, visualizzato in una finestra di anteprima di stampa o salvato come file EPS (Encapsulated PostScript). Se il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>è impostata su <xref:System.Drawing.Printing.PrintAction>, <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A>proprietà specifica il percorso e nome file.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A> </xref:System.Drawing.Printing.PrintAction> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>  
  
 La <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrinterSettings%2A>proprietà fornisce l'accesso a un <xref:System.Drawing.Printing.PrintDocument.PrinterSettings%2A>oggetto che consente di specificare impostazioni come la stampante da utilizzare e il numero di copie da stampare</xref:System.Drawing.Printing.PrintDocument.PrinterSettings%2A> sottostante</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrinterSettings%2A> È inoltre possibile eseguire query sulle funzionalità della stampante, ad esempio il supporto per il colore o duplex. Questa proprietà non viene visualizzata nella finestra **Proprietà** : è accessibile solo dal codice.  
  
 Il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Form%2A>proprietà viene utilizzata per specificare il form da stampare quando si richiama il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente a livello di codice.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> </xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Form%2A> Se il componente viene aggiunto a un form in fase di progettazione, tale form è quello predefinito.  
  
 Chiave di eventi per il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>componente includono quanto segue:</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
-   <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.BeginPrint>evento.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.BeginPrint> Si verifica quando il <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>viene chiamato il metodo e prima della prima pagina verrà stampato.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>  
  
-   <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.EndPrint>evento.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.EndPrint> Si verifica dopo la stampa dell'ultima pagina.  
  
-   <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.QueryPageSettings>evento.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.QueryPageSettings> Si verifica immediatamente prima della stampa di ogni pagina.  
  
### <a name="remarks"></a>Note  
 Se un modulo contiene testo o grafica creati mediante <xref:System.Drawing.Graphics>, usare metodi di base <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>(`Print()`) metodo per stamparlo.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A> </xref:System.Drawing.Graphics> Potrebbe non eseguire il rendering di grafica in alcuni sistemi operativi quando il metodo di overload <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>metodo viene utilizzato.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>  
  
 Se la larghezza di un form è maggiore della larghezza della carta della stampante, il lato destro del form potrebbe essere troncato. Quando si progettano moduli per la stampa, assicurarsi che il form sia contenuto su carta in formato standard.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato un utilizzo comune del <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>component.</xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm>  
  
```  
' Visual Basic.  
Dim pf As New PrintForm  
pf.Form = Me  
pf.PrintAction = PrintToPrinter  
pf.Print()  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A></xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.Print%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A></xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>   
 [Procedura: stampare un Form utilizzando il componente PrintForm](../../../visual-basic/developing-apps/printing/how-to-print-a-form-by-using-the-printform-component.md)   
 [Procedura: stampare l'Area Client di un Form](../../../visual-basic/developing-apps/printing/how-to-print-the-client-area-of-a-form.md)   
 [Procedura: stampare aree Client e Non Client di un Form](../../../visual-basic/developing-apps/printing/how-to-print-client-and-non-client-areas-of-a-form.md)   
 [Procedura: Stampare un form scorrevole](../../../visual-basic/developing-apps/printing/how-to-print-a-scrollable-form.md)
