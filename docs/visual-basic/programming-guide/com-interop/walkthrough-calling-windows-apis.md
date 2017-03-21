---
title: 'Procedura dettagliata: Chiamata delle API di Windows (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- DLLs, calling
- Windows API, walkthroughs
- platform invoke, walkthroughs
- API calls, walkthroughs [Visual Basic]
- Windows API, calling
- walkthroughs [Visual Basic], API calls
- DllImport attribute, calling Windows API
- Declare statement, declaring DLL functions
ms.assetid: 9280ca96-7a93-47a3-8d01-6d01be0657cb
caps.latest.revision: 20
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 5001ccebb0a5b8cadd4e856342601506cf1d033f
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-calling-windows-apis-visual-basic"></a>Procedura dettagliata: chiamata delle API di Windows (Visual Basic)
API di Windows sono librerie a collegamento dinamico (DLL) che fanno parte del sistema operativo Windows. Utilizzarli per eseguire attività quando è difficile scrivere routine equivalenti. Ad esempio, Windows fornisce una funzione denominata `FlashWindowEx` che consente di rendere la barra del titolo di un'applicazione alternare sfumature chiare e scure.  
  
 Il vantaggio di utilizzare le API di Windows nel codice è che è possibile risparmiare tempo sviluppo perché contengono molte utili funzionalità che sono già scritto e in attesa di essere utilizzato. Lo svantaggio è che le API di Windows può risultare difficile lavorare con e grossi quando le cose vanno male.  
  
 API di Windows rappresentano una categoria speciale di interoperabilità. API di Windows non utilizzano codice gestito, non dispongono di librerie dei tipi e utilizzare tipi di dati che sono diversi da quelli utilizzati con Visual Studio. A causa di queste differenze, e poiché le API di Windows non sono oggetti COM, l'interoperabilità con le API di Windows e [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] viene realizzata mediante platform invoke, o PInvoke. Platform invoke è un servizio che consente al codice per chiamare funzioni non gestite implementate in DLL gestito. Per ulteriori informazioni, vedere [utilizzo di funzioni DLL non gestite](http://msdn.microsoft.com/library/eca7606e-ebfb-4f47-b8d9-289903fdc045). È possibile utilizzare PInvoke in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] utilizzando il `Declare` istruzione o l'applicazione di `DllImport` attributo a una routine vuota.  
  
 Chiamate API Windows sono una parte importante di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] programmazione in passato, ma in genere non sono necessarie con [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]. Quando possibile, utilizzare codice gestito di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] per eseguire attività, invece di chiamate API Windows. Questa procedura dettagliata vengono fornite informazioni per i casi in cui tramite le API di Windows è necessaria.  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="api-calls-using-declare"></a>Chiamate API tramite dichiarare  
 È il modo più comune per chiamare le API di Windows utilizzando il `Declare` istruzione.  
  
#### <a name="to-declare-a-dll-procedure"></a>Per dichiarare una routine DLL  
  
1.  Determinare il nome della funzione da chiamare, più argomenti, tipi di argomenti e restituire valore, nonché il nome e percorso della DLL che lo contiene.  
  
    > [!NOTE]
    >  Per informazioni complete sulle API di Windows, vedere la documentazione di Win32 SDK nell'API di Windows Platform SDK. Per ulteriori informazioni sulle costanti che utilizzano le API di Windows, esaminare i file di intestazione, ad esempio incluso in SDK della piattaforma Windows. h.  
  
2.  Aprire un nuovo progetto applicazione Windows, fare clic su **New** sul **File** menu e quindi fare clic su **progetto**. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Selezionare **applicazione Windows** dall'elenco di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] modelli di progetto. Viene visualizzato il nuovo progetto.  
  
4.  Aggiungere il codice seguente `Declare` funzione alla classe o modulo in cui si desidera utilizzare la DLL:  
  
     [!code-vb[9 VbVbalrInterop](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_1.vb)]  
  
### <a name="parts-of-the-declare-statement"></a>Parti dell'istruzione Declare  
 Il `Declare` istruzione include i seguenti elementi.  
  
#### <a name="auto-modifier"></a>Modificatore Auto  
 Il `Auto` modificatore indica al runtime di convertire la stringa in base al nome di metodo in base alle regole di common language runtime (o nome di alias se specificato).  
  
#### <a name="lib-and-alias-keywords"></a>Parole chiave lib e Alias  
 Il nome che segue il `Function` (parola chiave) è il nome del programma utilizzato per accedere alla funzione importata. Può essere lo stesso nome reale della funzione che si sta chiamando oppure è possibile utilizzare qualsiasi nome di routine valido e quindi utilizzano il `Alias` (parola chiave) per specificare il nome reale della funzione che si sta chiamando.  
  
 Specificare il `Lib` (parola chiave), seguito dal nome e percorso della DLL che contiene la funzione che si sta chiamando. Non è necessario specificare il percorso dei file presenti nella directory di sistema Windows.  
  
 Utilizzare il `Alias` (parola chiave) se il nome della funzione che si sta chiamando non è valido [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] nome della stored procedure o in conflitto con il nome di altri elementi all'interno dell'applicazione. `Alias`indica il nome reale della funzione chiamata.  
  
#### <a name="argument-and-data-type-declarations"></a>Argomento e le dichiarazioni di tipi di dati  
 Dichiarare gli argomenti e i tipi di dati. Può essere difficile poiché i tipi di dati che utilizza Windows non corrispondono ai tipi di dati di Visual Studio. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]gran parte del lavoro è la conversione di argomenti di tipi di dati compatibili, un processo denominato *marshalling*. È possibile controllare in modo esplicito la modalità di marshalling di argomenti utilizzando il <xref:System.Runtime.InteropServices.MarshalAsAttribute>attributo definito nel <xref:System.Runtime.InteropServices>dello spazio dei nomi.</xref:System.Runtime.InteropServices> </xref:System.Runtime.InteropServices.MarshalAsAttribute>  
  
> [!NOTE]
>  Le versioni precedenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consentivano di dichiarare parametri `As Any`, vale a dire che i dati di tutti i dati tipo può essere utilizzato. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]è necessario utilizzare un tipo di dati specifico per tutti `Declare` istruzioni.  
  
#### <a name="windows-api-constants"></a>Costanti di API Windows  
 Alcuni argomenti sono combinazioni di costanti. Ad esempio, il `MessageBox` API descritta in questa procedura dettagliata accetta un argomento integer denominato `Typ` che controlla come viene visualizzata la finestra di messaggio. È possibile determinare il valore numerico di queste costanti esaminando il `#define` istruzioni nel file winuser. I valori numerici vengono in genere visualizzati in formato esadecimale, pertanto è consigliabile utilizzare una calcolatrice per sommarli e convertirli in decimale. Ad esempio, se si desidera combinare le costanti per lo stile esclamativo `MB_ICONEXCLAMATION` 0x00000030 e Sì/alcuno stile `MB_YESNO` 0x00000004, è possibile aggiungere i numeri e ottenere un risultato di 0x00000034 o 52 decimali. Anche se è possibile utilizzare direttamente il risultato decimale, è preferibile dichiarare questi valori come costanti nell'applicazione e combinarli tramite il `Or` operatore.  
  
###### <a name="to-declare-constants-for-windows-api-calls"></a>Per dichiarare le costanti per le chiamate API Windows  
  
1.  Consultare la documentazione per la funzione Windows che si sta chiamando. Determinare il nome di costanti utilizzate e il nome del file con estensione h che contiene i valori numerici per queste costanti.  
  
2.  Utilizzare un editor di testo, ad esempio Blocco note, per visualizzare il contenuto del file di intestazione (h) e trovare i valori associati alle costanti. Ad esempio, il `MessageBox` API utilizza la costante `MB_ICONQUESTION` per visualizzare un punto interrogativo nella finestra di messaggio. La definizione per `MB_ICONQUESTION` in winuser. H e viene visualizzato come segue:  
  
     `#define MB_ICONQUESTION             0x00000020L`  
  
3.  Aggiungere equivalente `Const` istruzioni per la classe o un modulo per rendere le costanti disponibili per l'applicazione. Ad esempio:  
  
     [!code-vb[VbVbalrInterop&#11;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_2.vb)]  
  
###### <a name="to-call-the-dll-procedure"></a>Per chiamare la routine DLL  
  
1.  Aggiungere un pulsante denominato `Button1` per l'avvio del modulo per il progetto e quindi fare doppio clic per visualizzare il codice. Il gestore eventi per il pulsante viene visualizzato.  
  
2.  Aggiungere codice per il `Click` gestore dell'evento del pulsante aggiunto per chiamare la routine e specificare gli argomenti appropriati:  
  
     [!code-vb[VbVbalrInterop&#12;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_3.vb)]  
  
3.  Eseguire il progetto premendo F5. La finestra di messaggio viene visualizzata con entrambi **Sì** e **n** pulsanti di risposta. Fare clic su uno.  
  
#### <a name="data-marshaling"></a>Marshalling dei dati  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Converte i tipi di dati dei parametri e valori restituiti per le chiamate API Windows, ma si possono utilizzare automaticamente il `MarshalAs` attributo per specificare in modo esplicito i tipi di dati non gestiti che prevede un'API. Per ulteriori informazioni sul marshalling di interoperabilità, vedere [marshalling di interoperabilità](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a).  
  
###### <a name="to-use-declare-and-marshalas-in-an-api-call"></a>Per utilizzare Declare e MarshalAs in una chiamata API  
  
1.  Determinare il nome della funzione da chiamare, gli argomenti, tipi di dati e valore restituito.  
  
2.  Per semplificare l'accesso per il `MarshalAs` attributo, aggiungere un `Imports` all'inizio del codice per la classe o modulo, come nell'esempio seguente:  
  
     [!code-vb[13 VbVbalrInterop](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
3.  Aggiungere un prototipo di funzione per la funzione importata nella classe o modulo si utilizza e applicare il `MarshalAs` per i parametri dell'attributo o valore restituito. Nell'esempio seguente, una chiamata API che prevede il tipo `void*` viene sottoposto a marshalling come `AsAny`:  
  
     [!code-vb[VbVbalrInterop&#14;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_5.vb)]  
  
## <a name="api-calls-using-dllimport"></a>Chiamate API tramite DllImport  
 Il `DllImport` attributo fornisce un metodo alternativo di chiamare funzioni nelle DLL senza librerie dei tipi. `DllImport`è quasi equivalente all'utilizzo di un `Declare` istruzione ma fornisce maggiore controllo sulla modalità di chiamata delle funzioni.  
  
 È possibile utilizzare `DllImport` con la maggior parte delle API di Windows chiama, purché la chiamata fa riferimento a una scheda SCSI (talvolta chiamato *statico*) metodo. È possibile utilizzare metodi che richiedono un'istanza di una classe. A differenza di `Declare` istruzioni `DllImport` chiamate è possono utilizzare il `MarshalAs` attributo.  
  
#### <a name="to-call-a-windows-api-using-the-dllimport-attribute"></a>Per chiamare un'API di Windows utilizzando l'attributo DllImport  
  
1.  Aprire un nuovo progetto applicazione Windows, fare clic su **New** sul **File** menu e quindi fare clic su **progetto**. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Selezionare **applicazione Windows** dall'elenco di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] modelli di progetto. Viene visualizzato il nuovo progetto.  
  
3.  Aggiungere un pulsante denominato `Button2` al form di avvio.  
  
4.  Fare doppio clic su `Button2` per visualizzare il codice per il form.  
  
5.  Per semplificare l'accesso a `DllImport`, aggiungere un `Imports` all'inizio del codice per la classe di form di avvio:  
  
     [!code-vb[13 VbVbalrInterop](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
6.  Dichiarare una funzione vuota prima di `End Class` istruzione per il form e il nome di funzione `MoveFile`.  
  
7.  Applicare il `Public` e `Shared` i modificatori di dichiarazione di funzione e impostare i parametri per `MoveFile` basata sugli argomenti viene utilizzata la funzione API Windows:  
  
     [!code-vb[VbVbalrInterop&#16;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_6.vb)]  
  
     La funzione può avere qualsiasi nome di routine valido; il `DllImport` attributo specifica il nome della DLL. Gestisce inoltre il marshalling di interoperabilità per i parametri e valori restituiti, è possibile scegliere i tipi di dati di Visual Studio sono simili ai dati dei tipi utilizzati dall'API.  
  
8.  Applicare il `DllImport` attributo alla funzione vuota. Il primo parametro è il nome e il percorso della DLL che contiene la funzione che si sta chiamando. Non è necessario specificare il percorso dei file presenti nella directory di sistema Windows. Il secondo parametro è un argomento denominato che specifica il nome della funzione nell'API di Windows. In questo esempio, il `DllImport` attributo impone che le chiamate a `MoveFile` deve essere inoltrato al `MoveFileW` in KERNEL32. DLL. Il `MoveFileW` metodo copia un file dal percorso di `src` al percorso `dst`.  
  
     [!code-vb[VbVbalrInterop n.&17;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_7.vb)]  
  
9. Aggiungere codice per il `Button2_Click` gestore eventi per chiamare la funzione:  
  
     [!code-vb[VbVbalrInterop&#18;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_8.vb)]  
  
10. Creare un file denominato test. txt e inserirlo nella directory C:\Tmp sul disco rigido. Se necessario, creare la directory Tmp.  
  
11. Premere F5 per avviare l’applicazione. Viene visualizzato il form principale.  
  
12. Fare clic su **Button2**. Se il file può essere spostato, viene visualizzato il messaggio "il file è stato spostato correttamente".  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Runtime.InteropServices.DllImportAttribute></xref:System.Runtime.InteropServices.DllImportAttribute>   
 <xref:System.Runtime.InteropServices.MarshalAsAttribute></xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Declare (istruzione)](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Automatico](../../../visual-basic/language-reference/modifiers/auto.md)   
 [Alias](../../../visual-basic/language-reference/statements/alias-clause.md)   
 [Interoperabilità COM](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Creazione di prototipi nel codice gestito](http://msdn.microsoft.com/library/ecdcf25d-cae3-4f07-a2b6-8397ac6dc42d)   
 [Marshalling di un delegato come metodo di Callback](http://msdn.microsoft.com/library/6ddd7866-9804-4571-84de-83f5cc017a5a)
