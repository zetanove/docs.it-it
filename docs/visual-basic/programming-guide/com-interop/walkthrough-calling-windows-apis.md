---
title: "Walkthrough: Calling Windows APIs (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DLLs, calling"
  - "Windows API, walkthroughs"
  - "platform invoke, walkthroughs"
  - "API calls, walkthroughs [Visual Basic]"
  - "Windows API, calling"
  - "walkthroughs [Visual Basic], API calls"
  - "DllImport attribute, calling Windows API"
  - "Declare statement, declaring DLL functions"
ms.assetid: 9280ca96-7a93-47a3-8d01-6d01be0657cb
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Walkthrough: Calling Windows APIs (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le API di Windows sono librerie a collegamento dinamico \(DLL, Dynamic Link Library\) che fanno parte del sistema operativo Windows.  È possibile utilizzare le API di Windows per eseguire alcune attività quando è difficile scrivere routine equivalenti.  In Windows è disponibile ad esempio una funzione denominata `FlashWindowEx`, che consente di alternare sfumature chiare e scure nella barra del titolo delle applicazioni.  
  
 Utilizzando le API di Windows è possibile velocizzare i tempi di programmazione, in quanto le API includono molte utili funzionalità già pronte per l'uso.  Tuttavia, utilizzare le API di Windows può essere difficile e, in caso di errore, si verificano grossi problemi.  
  
 Le API di Windows rappresentano una categoria di interoperabilità speciale,  non utilizzano codice gestito, non dispongono di librerie dei tipi incorporate e utilizzano tipi di dati diversi da quelli utilizzati in Visual Studio.  Tenendo conto di tali differenze, e poiché le API di Windows non sono oggetti COM, l'interoperabilità con le API di Windows e [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] viene realizzata mediante platform invoke \(PInvoke\).  Le chiamate della piattaforma sono un servizio che consente al codice gestito di chiamare le funzioni non gestite implementate in una DLL.  Per ulteriori informazioni, vedere [Consuming Unmanaged DLL Functions](../Topic/Consuming%20Unmanaged%20DLL%20Functions.md).  È possibile utilizzare PInvoke in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] mediante l'istruzione `Declare` o attraverso l'applicazione dell'attributo `DllImport` a una routine vuota.  
  
 Le chiamate delle API di Windows costituivano un elemento importante della programmazione in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], ma con [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] in genere non sono necessarie.  Se possibile, si consiglia di utilizzare codice gestito da [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] anziché chiamate di API di Windows, per eseguire le attività.  Nella procedura dettagliata descritta di seguito sono fornite tutte le informazioni necessarie per l'utilizzo delle API di Windows.  
  
 [!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
## Chiamate API tramite l'istruzione Declare  
 Il metodo più comune per chiamare le API di Windows consiste nell'utilizzare l'istruzione `Declare`.  
  
#### Per dichiarare una routine DLL  
  
1.  Determinare il nome della funzione che si desidera chiamare, gli argomenti, i tipi degli argomenti e i valori restituiti, nonché il nome e il percorso della DLL che li contiene.  
  
    > [!NOTE]
    >  Per informazioni dettagliate sulle API di Windows, fare riferimento alla documentazione dell'SDK di Windows a 32 bit in API di Windows in Platform SDK.  Per ulteriori informazioni sulle costanti utilizzate dalle API di Windows, vedere i file di intestazione disponibili in Platform SDK, ad esempio Windows.h.  
  
2.  Aprire un nuovo progetto Applicazione Windows scegliendo **Nuovo** dal menu **File** e quindi **Progetto**.  Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
3.  Selezionare **Applicazione Windows** nell'elenco di modelli di progetto di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  Verrà visualizzato il nuovo progetto.  
  
4.  Aggiungere la funzione `Declare` seguente alla classe o al modulo in cui si desidera utilizzare la DLL:  
  
     [!code-vb[VbVbalrInterop#9](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_1.vb)]  
  
### Parti dell'istruzione Declare  
 L'istruzione `Declare` include gli elementi descritti di seguito.  
  
#### Modificatore Auto  
 Il modificatore `Auto` indica al runtime di convertire la stringa sulla base del nome del metodo o, se specificato, al nome di alias secondo le regole di Common Language Runtime.  
  
#### Parole chiave Lib e Alias  
 Il nome che segue la parola chiave `Function` è il nome utilizzato dal programma per accedere alla funzione importata.  Il nome può corrispondere al nome reale della funzione che si sta chiamando. In alternativa, è possibile utilizzare qualsiasi nome di routine valido e quindi utilizzare la parola chiave `Alias` per specificare il nome reale della funzione che si sta chiamando.  
  
 Specificare la parola chiave `Lib` seguita dal nome e dalla posizione della DLL che contiene la funzione che si sta chiamando.  Non è necessario specificare il percorso dei file che si trovano nelle directory di sistema di Windows.  
  
 Utilizzare la parola chiave `Alias` se il nome della funzione che si sta chiamando non è un nome di routine di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] valido o se è in conflitto con il nome di altri elementi dell'applicazione.  `Alias` indica il nome reale della funzione chiamata.  
  
#### Dichiarazioni del tipo di dati e dell'argomento  
 Dichiarare gli argomenti e i relativi tipi di dati  Questa operazione può risultare impegnativa in quanto i tipi di dati utilizzati da Windows non corrispondono a quelli di Visual Studio.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] gran parte del lavoro viene svolta automaticamente mediante un processo denominato *marshalling*, che consiste nella conversione degli argomenti in tipi di dati compatibili.  Per controllare in modo esplicito il marshalling degli argomenti, è possibile utilizzare l'attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute> definito nello spazio dei nomi <xref:System.Runtime.InteropServices>.  
  
> [!NOTE]
>  Le versioni precedenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consentivano di dichiarare parametri `As Any`, pertanto era possibile utilizzare dati di qualsiasi tipo.  In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] è necessario utilizzare un tipo di dati specifico per tutte le istruzioni `Declare`.  
  
#### Costanti di API di Windows  
 Alcuni argomenti includono più costanti.  L'API `MessageBox` descritta in questa procedura dettagliata, ad esempio, accetta un argomento Integer denominato `Typ` che controlla le modalità di visualizzazione della finestra di messaggio.  È possibile determinare il valore numerico di queste costanti esaminando le istruzioni `#define` nel file WinUser.h.  I valori numerici vengono in genere indicati come valori esadecimali, pertanto potrebbe essere necessario utilizzare una calcolatrice per sommarli e convertirli in decimali.  Se ad esempio si desidera combinare le costanti per lo stile esclamativo `MB_ICONEXCLAMATION` 0x00000030 e lo stile Sì\/No `MB_YESNO` 0x00000004, è possibile sommare i numeri e ottenere un risultato di 0x00000034 o 52 decimali.  Sebbene sia possibile utilizzare direttamente il risultato decimale, si consiglia di dichiarare questi valori come costanti nell'applicazione e di combinarli utilizzando l'operatore `Or`.  
  
###### Per dichiarare costanti per le chiamate API di Windows  
  
1.  Consultare la documentazione relativa alla funzione di Windows che si sta chiamando.  Determinare il nome delle costanti utilizzate e il nome del file con estensione h contenente i valori numerici di tali costanti.  
  
2.  Per visualizzare il contenuto del file di intestazione con estensione h e individuare i valori associati alle costanti utilizzate, utilizzare un editor di testo, ad esempio Blocco note.  L'API `MessageBox`, ad esempio, utilizza la costante `MB_ICONQUESTION` per visualizzare un punto interrogativo nella finestra del messaggio.  La definizione di `MB_ICONQUESTION`, che si trova nel file WinUser.h, è la seguente:  
  
     `#define MB_ICONQUESTION             0x00000020L`  
  
3.  Aggiungere istruzioni `Const` equivalenti alla classe o al modulo per rendere disponibili le costanti nell'applicazione.  Di seguito è riportato un esempio:  
  
     [!code-vb[VbVbalrInterop#11](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_2.vb)]  
  
###### Per chiamare la routine DLL  
  
1.  Aggiungere un pulsante denominato `Button1` al form di avvio del progetto, quindi fare doppio clic su di esso per visualizzarne il codice.  Verrà visualizzato il gestore eventi per il pulsante.  
  
2.  Aggiungere codice al gestore eventi `Click` relativo al pulsante aggiunto per chiamare la routine e specificare gli argomenti appropriati.  
  
     [!code-vb[VbVbalrInterop#12](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_3.vb)]  
  
3.  Premere F5 per eseguire il progetto.  Verrà visualizzata la finestra di messaggio con i pulsanti di risposta **Yes** e **No**.  Fare clic su uno dei pulsanti.  
  
#### Marshalling dei dati  
 In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] i tipi di dati dei parametri e dei valori restituiti per le chiamate delle API di Windows vengono convertiti automaticamente, tuttavia è possibile utilizzare l'attributo `MarshalAs` per specificare in modo esplicito tipi di dati non gestiti previsti da un'API.  Per ulteriori informazioni sul marshalling di interoperabilità, vedere [Interop Marshaling](../Topic/Interop%20Marshaling.md).  
  
###### Per utilizzare Declare e MarshalAs in una chiamata API  
  
1.  Determinare il nome della funzione che si desidera chiamare, gli argomenti, i tipi di dati e i valori restituiti.  
  
2.  Per semplificare l'accesso all'attributo `MarshalAs`, aggiungere un'istruzione `Imports` all'inizio del codice della classe o del modulo, come nell'esempio seguente:  
  
     [!code-vb[VbVbalrInterop#13](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
3.  Aggiungere un prototipo di funzione per la funzione importata nella classe o nel modulo utilizzato e applicare l'attributo `MarshalAs` ai parametri o al valore restituito.  Nell'esempio che segue viene eseguito il marshalling come `AsAny` di una chiamata API che prevede il tipo `void*`:  
  
     [!code-vb[VbVbalrInterop#14](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_5.vb)]  
  
## Chiamate API tramite l'attributo DllImport  
 L'attributo `DllImport` fornisce un metodo alternativo di chiamata delle funzioni nelle DLL senza librerie dei tipi.  `DllImport` corrisponde per certi aspetti all'utilizzo di un'istruzione `Declare` ma consente di esercitare un maggiore controllo sulle modalità di chiamata delle funzioni.  
  
 È possibile utilizzare l'attributo `DllImport` con la maggior parte delle chiamate API di Windows purché la chiamata faccia riferimento a un metodo condiviso, o *statico*.  Non è possibile utilizzare metodi che richiedono un'istanza di una classe.  A differenza delle istruzioni `Declare`, le chiamate `DllImport` non possono utilizzare l'attributo `MarshalAs`.  
  
#### Per chiamare un'API di Windows tramite l'attributo DllImport  
  
1.  Aprire un nuovo progetto Applicazione Windows scegliendo **Nuovo** dal menu **File** e quindi **Progetto**.  Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
2.  Selezionare **Applicazione Windows** nell'elenco di modelli di progetto di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  Verrà visualizzato il nuovo progetto.  
  
3.  Aggiungere al form di avvio un pulsante denominato `Button2`.  
  
4.  Fare doppio clic su `Button2` per visualizzare il codice del form.  
  
5.  Per semplificare l'accesso all'attributo `DllImport`, aggiungere un'istruzione `Imports` all'inizio del codice della classe del form di avvio.  
  
     [!code-vb[VbVbalrInterop#13](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
6.  Dichiarare una funzione vuota prima dell'istruzione `End Class` del form e nominare la funzione `MoveFile`.  
  
7.  Applicare i modificatori `Public` e `Shared` alla dichiarazione di funzione e impostare i parametri per `MoveFile` sulla base degli argomenti utilizzati dalla funzione API di Windows.  
  
     [!code-vb[VbVbalrInterop#16](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_6.vb)]  
  
     È possibile assegnare alla funzione qualsiasi nome di routine valido; nella DLL il nome è specificato dall'attributo `DllImport`.  Poiché inoltre questo attributo gestisce il marshalling di interoperabilità per i parametri e i valori restituiti, è possibile scegliere tipi di dati di Visual Studio simili a quelli utilizzati dall'API.  
  
8.  Applicare l'attributo `DllImport` alla funzione vuota.  Il primo parametro indica il nome e il percorso della DLL che contiene la funzione che si sta chiamando.  Non è necessario specificare il percorso dei file che si trovano nelle directory di sistema di Windows.  Il secondo parametro è un argomento denominato che specifica il nome della funzione nell'API di Windows.  In questo esempio l'attributo `DllImport` impone che le chiamate a `MoveFile` vengano inoltrate a `MoveFileW` in KERNEL32.DLL.  Il metodo `MoveFileW` copia un file dal percorso `src` al percorso `dst`.  
  
     [!code-vb[VbVbalrInterop#17](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_7.vb)]  
  
9. Aggiungere codice al gestore eventi `Button2_Click` per chiamare la funzione:  
  
     [!code-vb[VbVbalrInterop#18](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_8.vb)]  
  
10. Creare un file denominato Test.txt e inserirlo nella directory C:\\Tmp del disco rigido.  Se necessario, creare la directory Tmp.  
  
11. Premere F5 per avviare l’applicazione.  Verrà visualizzato il form principale.  
  
12. Fare clic su **Button2**.  Se è possibile spostare il file, verrà visualizzato un messaggio che informa che il file è stato spostato.  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Auto](../../../visual-basic/language-reference/modifiers/auto.md)   
 [Alias](../../../visual-basic/language-reference/statements/alias-clause.md)   
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Creating Prototypes in Managed Code](../Topic/Creating%20Prototypes%20in%20Managed%20Code.md)   
 [Marshaling a Delegate as a Callback Method](../Topic/Marshaling%20a%20Delegate%20as%20a%20Callback%20Method.md)