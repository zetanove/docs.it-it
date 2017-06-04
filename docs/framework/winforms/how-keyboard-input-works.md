---
title: "How Keyboard Input Works | Microsoft Docs"
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
  - "keyboard input, about keyboard input"
  - "keyboards, keyboard input"
  - "Windows Forms, keyboard input"
ms.assetid: 9a29433c-a180-49bb-b74c-d187786584c8
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# How Keyboard Input Works
Gli input della tastiera vengono elaborati in Windows Form mediante la generazione di eventi della tastiera in risposta a messaggi di Windows.  La maggior parte delle applicazioni Windows Form elabora gli input della tastiera solo tramite la gestione dei relativi eventi.  È tuttavia necessario comprendere il funzionamento dei messaggi della tastiera per implementare scenari di input della tastiera più avanzati, come l'intercettazione dei tasti prima che vengano inviati a un controllo.  In questo argomento vengono descritti i tipi di dati riconosciuti da Windows Form e viene fornita una panoramica sulla modalità di invio dei messaggi della tastiera.  Per informazioni sugli eventi della tastiera, vedere [Using Keyboard Events](../../../docs/framework/winforms/using-keyboard-events.md).  
  
## Tipi di tasti  
 Windows Form identifica gli input della tastiera come codici di tasti virtuali rappresentati dall'enumerazione bit per bit <xref:System.Windows.Forms.Keys>.  Con l'enumerazione <xref:System.Windows.Forms.Keys>, è possibile combinare la pressione di una serie di tasti per ottenere un valore singolo.  Questi valori corrispondono ai valori associati ai messaggi di Windows WM\_KEYDOWN e WM\_SYSKEYDOWN.  La maggior parte delle pressioni fisiche dei tasti può essere rilevata gestendo l'evento <xref:System.Windows.Forms.Control.KeyDown> o l'evento <xref:System.Windows.Forms.Control.KeyUp>.  I tasti carattere costituiscono un sottoinsieme dell'enumerazione <xref:System.Windows.Forms.Keys> e corrispondono ai valori associati ai messaggi di Windows WM\_CHAR e WM\_SYSCHAR.  Se la combinazione dei tasti premuti produce un carattere, è possibile individuare il carattere gestendo l'evento <xref:System.Windows.Forms.Control.KeyPress>.  In alternativa, è possibile utilizzare la classe <xref:Microsoft.VisualBasic.Devices.Keyboard>, esposta dall'interfaccia di programmazione di Visual Basic, per individuare i tasti premuti e inviare i tasti.  Per ulteriori informazioni, vedere [Accessing the Keyboard](../Topic/Accessing%20the%20Keyboard%20\(Visual%20Basic\).md).  
  
## Ordine degli eventi della tastiera  
 Come riportato in precedenza, in un controllo possono verificarsi 3 eventi collegati alla tastiera.  Nella sequenza descritta di seguito è illustrato l'ordine generale degli eventi.  
  
1.  L'utente preme il tasto "a", il tasto viene pre\-elaborato e inviato e viene generato un evento <xref:System.Windows.Forms.Control.KeyDown>.  
  
2.  L'utente tiene premuto il tasto "a", il tasto viene pre\-elaborato e inviato e viene generato un evento <xref:System.Windows.Forms.Control.KeyPress>.  
  
     Questo evento si verifica più volte per il tempo in cui l'utente tiene premuto il tasto.  
  
3.  L'utente rilascia il tasto "a", il tasto viene pre\-elaborato e inviato e viene generato un evento <xref:System.Windows.Forms.Control.KeyUp>.  
  
## Pre\-elaborazione dei tasti  
 Come altri messaggi, i messaggi della tastiera sono elaborati nel metodo <xref:System.Windows.Forms.Control.WndProc%2A> di un form o di un controllo.  Tuttavia, prima che i messaggi della tastiera vengano elaborati, il metodo <xref:System.Windows.Forms.Control.PreProcessMessage%2A> chiama uno o più metodi che possono essere sottoposti a override per gestire tasti di caratteri speciali e tasti fisici.  È possibile eseguire l'override di questi metodi per individuare e filtrare alcuni tasti prima che i messaggi vengano elaborati dal controllo.  Nella tabella riportata di seguito viene illustrata l'azione da effettuare e il relativo metodo, secondo l'ordine di esecuzione dei metodi.  
  
### Pre\-elaborazione per un evento KeyDown  
  
|Azione|Metodo collegato|Note|  
|------------|----------------------|----------|  
|Verificare la presenza di un tasto di comando, ad esempio un tasto di scelta rapida o un tasto di scelta rapida di menu.|<xref:System.Windows.Forms.Control.ProcessCmdKey%2A>|Questo metodo elabora un tasto di comando, che ha la precedenza sui tasti normali.  Se il metodo restituisce `true`, il messaggio del tasto non viene inviato e non vengono generati eventi del tasto.  Se restituisce `false`, viene chiamato il metodo <xref:System.Windows.Forms.Control.IsInputKey%2A>`.`|  
|Verificare la presenza di un tasto speciale che richieda la pre\-elaborazione o di un tasto carattere normale che deve generare un evento <xref:System.Windows.Forms.Control.KeyDown> ed essere inviato a un controllo.|<xref:System.Windows.Forms.Control.IsInputKey%2A>|Se il metodo restituisce `true`, il controllo è un carattere normale e viene generato un evento <xref:System.Windows.Forms.Control.KeyDown>.  Se restituisce `false`, viene chiamato il metodo <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>. **Note:**  Per verificare che un controllo ottenga un tasto o una combinazione di tasti, è possibile gestire l'evento <xref:System.Windows.Forms.Control.PreviewKeyDown> e impostare la proprietà <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A> di <xref:System.Windows.Forms.PreviewKeyDownEventArgs> su `true` per il tasto o i tasti desiderati.|  
|Verificare la presenza di un tasto di navigazione \(ESC, TAB, ritorno a capo o tasti di direzione\).|<xref:System.Windows.Forms.Control.ProcessDialogKey%2A>|Questo metodo elabora un tasto fisico che impiega funzionalità speciali all'interno del controllo, come il passaggio dello stato di attivazione dal controllo al controllo padre e viceversa.  Se il controllo diretto non gestisce il tasto, viene chiamato il metodo <xref:System.Windows.Forms.Control.ProcessDialogKey%2A> sul controllo padre e così via fino al primo controllo nella gerarchia.  Se il metodo restituisce `true`, la pre\-elaborazione è completa e non vengono generati eventi del tasto.  Se restituisce `false`, viene generato un evento <xref:System.Windows.Forms.Control.KeyDown>.|  
  
### Pre\-elaborazione per un evento KeyPress  
  
|Azione|Metodo collegato|Note|  
|------------|----------------------|----------|  
|Verificare che il tasto sia un carattere normale che dovrà essere elaborato dal controllo|<xref:System.Windows.Forms.Control.IsInputChar%2A>|Se il carattere è un carattere normale, questo metodo restituisce `true`, viene generato l'evento <xref:System.Windows.Forms.Control.KeyPress> e non si verifica alcuna ulteriore pre\-elaborazione.  In caso contrario, verrà chiamato il metodo <xref:System.Windows.Forms.Control.ProcessDialogChar%2A>.|  
|Verificare che il carattere rappresenti un tasto di scelta \(come &OK su un pulsante\)|<xref:System.Windows.Forms.Control.ProcessDialogChar%2A>|Questo metodo, simile al metodo <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>, viene chiamato nella parte superiore della gerarchia dei controlli.  Se il controllo è un controllo contenitore, viene verificata la presenza di tasti di scelta chiamando il metodo <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> sul controllo stesso e sui controlli figlio.  Se <xref:System.Windows.Forms.Control.ProcessDialogChar%2A> restituisce `true`, l'evento <xref:System.Windows.Forms.Control.KeyPress> non viene generato.|  
  
## Elaborazione dei messaggi della tastiera  
 Una volta che i messaggi della tastiera raggiungono il metodo <xref:System.Windows.Forms.Control.WndProc%2A> di un form o di un controllo, vengono elaborati da un gruppo di metodi che è possibile sottoporre a override.  Ciascuno di questi metodi restituisce un valore <xref:System.Boolean> che specifica se il messaggio della tastiera è stato elaborato e utilizzato dal controllo.  Se uno dei metodi restituisce `true`, il messaggio viene considerato gestito e non viene passato al controllo base o al controllo padre per l'ulteriore elaborazione.  In caso contrario, il messaggio rimane nella relativa coda e può essere elaborato in un altro metodo nel controllo base o nel controllo padre.  Nella tabella riportata di seguito sono riportati i metodi che elaborano i messaggi della tastiera.  
  
|Metodo|Note|  
|------------|----------|  
|<xref:System.Windows.Forms.Control.ProcessKeyMessage%2A>|Questo metodo elabora tutti i messaggi della tastiera ricevuti dal metodo <xref:System.Windows.Forms.Control.WndProc%2A> del controllo.|  
|<xref:System.Windows.Forms.Control.ProcessKeyPreview%2A>|Questo metodo invia il messaggio della tastiera al controllo padre del controllo.  Se <xref:System.Windows.Forms.Control.ProcessKeyPreview%2A> restituisce `true`, non viene generato alcun evento della tastiera. In caso contrario, viene chiamato il metodo <xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A>.|  
|<xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A>|Questo metodo genera gli eventi <xref:System.Windows.Forms.Control.KeyDown>, <xref:System.Windows.Forms.Control.KeyPress> e <xref:System.Windows.Forms.Control.KeyUp>, a seconda dei casi.|  
  
## Override dei metodi della tastiera  
 Quando un messaggio della tastiera viene pre\-elaborato ed elaborato, sono disponibili per l'override molti metodi. Alcuni di essi sono tuttavia preferibili ad altri.  Nella tabella riportata di seguito sono descritte le attività che è possibile eseguire e i metodi migliori per sottoporre a override i metodi della tastiera.  Per ulteriori informazioni sull'override dei metodi, vedere [NOT IN BUILD: Overriding Properties and Methods](http://msdn.microsoft.com/it-it/2167e8f5-1225-4b13-9ebd-02591ba90213).  
  
|Task|Metodo|  
|----------|------------|  
|Intercettare un tasto di navigazione e generare l'evento <xref:System.Windows.Forms.Control.KeyDown>,  ad esempio per gestire i tasti TAB e ritorno a capo in una casella di testo.|Eseguire l'override di <xref:System.Windows.Forms.Control.IsInputKey%2A>. **Note:**  In alternativa, è possibile gestire l'evento <xref:System.Windows.Forms.Control.PreviewKeyDown> e impostare <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A> di <xref:System.Windows.Forms.PreviewKeyDownEventArgs> su `true` per il tasto o i tasti desiderati.|  
|Gestire input speciali o di navigazione in un controllo,  ad esempio se si desidera utilizzare i tasti freccia nel controllo elenco per selezionare un altro elemento.|Eseguire l'override di <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>.|  
|Intercettare un tasto di navigazione e generare l'evento <xref:System.Windows.Forms.Control.KeyPress>,  ad esempio se si desidera disporre di più tasti freccia da premere per accelerare lo spostamento tra gli elementi in un controllo casella di selezione.|Eseguire l'override di <xref:System.Windows.Forms.Control.IsInputChar%2A>.|  
|Gestire input speciali o di navigazione durante un evento <xref:System.Windows.Forms.Control.KeyPress>,  ad esempio se si desidera tenere premuto il tasto "r" per selezionare gli elementi che iniziano con la lettera r in un controllo elenco.|Eseguire l'override di <xref:System.Windows.Forms.Control.ProcessDialogChar%2A>.|  
|Gestire tasti di scelta personalizzati, ad esempio se si desidera gestire tasti di scelta presenti su pulsanti creati dal proprietario in una barra degli strumenti.|Eseguire l'override di <xref:System.Windows.Forms.Control.ProcessMnemonic%2A>.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.Keys>   
 <xref:System.Windows.Forms.Control.WndProc%2A>   
 <xref:System.Windows.Forms.Control.PreProcessMessage%2A>   
 [My.Computer.Keyboard Object](../../../ocs/visual-basic/language-reference/objects/my-computer-keyboard-object.md)   
 [Accessing the Keyboard](../Topic/Accessing%20the%20Keyboard%20\(Visual%20Basic\).md)   
 [Using Keyboard Events](../../../docs/framework/winforms/using-keyboard-events.md)