---
title: "User Input Validation in Windows Forms | Microsoft Docs"
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
  - "Windows Forms, validating user input"
  - "validation, Windows Forms user input"
  - "user input, validating in Windows Forms"
  - "validating user input, Windows Forms"
ms.assetid: 4ec07681-1dee-4bf9-be5e-718f635a33a1
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# User Input Validation in Windows Forms
Quando gli utenti inseriscono dati all'interno dell'applicazione, può essere opportuno verificare che i dati siano validi prima di essere utilizzati nell'applicazione.  È possibile fare in modo che alcuni campi di testo non abbiano lunghezza zero, che un campo venga formattato per inserirvi numeri telefonici o altri tipi di dati in formato valido o che una stringa non contenga caratteri non sicuri che potrebbero venire utilizzati per compromettere la sicurezza di un database.  I Windows Form forniscono molte modalità per la convalidare dell'input nell'applicazione.  
  
## Convalida mediante il controllo MaskedTextBox  
 Se è necessario fare in modo che gli utenti inseriscano dati in un formato ben definito, come quello di un numero telefonico o di un codice di identificazione, è possibile utilizzare il controllo <xref:System.Windows.Forms.MaskedTextBox> per eseguire questa operazione rapidamente, utilizzando una quantità minima di codice.  Una *maschera* è una stringa costituita da caratteri in un linguaggio di definizione della maschera che specifica i caratteri che possono essere inseriti in una posizione determinata nella casella di testo.  Il controllo consente la visualizzazione di un gruppo di prompt per l'utente.  Se l'utente digita un valore non corretto, ad esempio una lettera anziché un numero, il controllo rifiuta automaticamente l'input.  
  
 Il linguaggio di definizione della maschera utilizzato da <xref:System.Windows.Forms.MaskedTextBox> è molto flessibile.  Questo consente di specificare i caratteri obbligatori, facoltativi, letterali \(come trattini e parentesi\), di valuta e separatori di data.  Il controllo funziona bene quando associato a un'origine dati.  L'evento <xref:System.Windows.Forms.Binding.Format> in un'associazione dati può essere utilizzato per riformattare i dati in ingresso in modo da renderli compatibili con la mschera mentre l'evento <xref:System.Windows.Forms.Binding.Parse> può essere utilizzato per riformattare I dati in usicta per renderli compatibili con le specifiche del campo dati.  
  
 Per ulteriori informazioni, vedere [Controllo MaskedTextBox](../../../docs/framework/winforms/controls/maskedtextbox-control-windows-forms.md).  
  
## Convalida basata sugli eventi  
 Se si desidera il controllo completo sulla convalida a livello di codice oppure è necessario eseguire controlli di convalida complessi, utilizzare gli eventi di convalida incorporati nella maggior parte dei controlli Windows Form.  I controlli che accettano input dell'utente in formato libero dispongono di un evento <xref:System.Windows.Forms.Control.Validating>, che viene generato ogni volta che il controllo richiede la convalida dei dati.  Nel metodo per la gestione eventi <xref:System.Windows.Forms.Control.Validating> è possibile convalidare l'input dell'utente in molte modalità.  Se ad esempio se dispone di una casella di testo che deve contenere un codice postale, è possibile eseguire la convalida nelle modalità seguenti:  
  
-   Se il codice postale deve appartenere a un gruppo specifico di codici postali, è possibile eseguire un confronto tra stringhe sull'input per convalidare i dati immessi dall'utente.  Se ad esempio il codice postale deve essere incluso nell'insieme {10001, 10002 10003}, è possibile utilizzare un confronto tra stringhe per convalidare i dati.  
  
-   Se il codice postale deve essere incluso in un form specifico, è possibile utilizzare espressioni regolari per convalidare i dati immessi dall'utente.  Convalidare ad esempio il form `#####` o `#####-####`, è possibile utilizzare l'espressione regolare `^(\d{5})(-\d{4})?$`.  Per convalidare il form `A#A #A#`, è possibile utilizzare l'espressione regolare `[A-Z]\d[A-Z] \d[A-Z]\d`.  Per ulteriori informazioni sulle espressioni regolari, vedere [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md) e [Esempi di espressioni regolari](../../../docs/standard/base-types/regular-expression-examples.md).  
  
-   Se il codice postale deve essere un codice postale di Stati Uniti valido, è possibile chiamare un servizio Web di codici postali per convalidare i dati immessi dall'utente.  
  
 All'evento <xref:System.Windows.Forms.Control.Validating> viene fornito un oggetto di tipo <xref:System.ComponentModel.CancelEventArgs>.  Se i dati del controllo non sono validi, è possibile annullare l'evento <xref:System.Windows.Forms.Control.Validating> impostando la proprietà <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> dell'oggetto su `true`.  Se non si imposta la proprietà <xref:System.ComponentModel.CancelEventArgs.Cancel%2A>, in Windows Form si presuppone la riuscita della convalida per il controllo in questione e viene attivato l'evento <xref:System.Windows.Forms.Control.Validated>.  
  
 Per un esempio di codice che convalida un indirizzo di posta elettronica in <xref:System.Windows.Controls.TextBox>, vedere <xref:System.Windows.Forms.Control.Validating>.  
  
### Associazione dati e convalida basata sugli eventi  
 La convalida è molto utile quando i controlli sono associati a un'origine dati, come una tabella di database.  Mediante la convalida, è possibile verificare che i dati del controllo soddisfino il formato richiesto dall'origine dati e che non contengano caratteri speciali come virgolette e barre rovesciate che potrebbero essere di tipo unsafe.  
  
 Quando si utilizza l'associazione dati, i dati presenti nel controllo vengono sincronizzati con l'origine dati durante l'esecuzione dell'evento <xref:System.Windows.Forms.Control.Validating>.  Se si annulla l'evento <xref:System.Windows.Forms.Control.Validating>, i dati non vengono sincronizzati con l'origine dati.  
  
> [!IMPORTANT]
>  Se si utilizza una convalida personalizzata che si verifica dopo l'evento <xref:System.Windows.Forms.Control.Validating>, questa non influirà sull'associazione dati.  Se ad esempio se si dispone del codice in un evento <xref:System.Windows.Forms.Control.Validated> che tenta di annullare l'associazione dati, si verificherà ancora l'associazione dati.  In questo caso, per eseguire una convalida nell'evento <xref:System.Windows.Forms.Control.Validated>, modificare la proprietà **Data Source Update Mode** del controllo \(**in \(Databindings\)**\\**\(Advanced\)**\) da **OnValidation** su **Mai** e aggiugere *Controllo*`.DataBindings["`*\<CAMPO\>*`"].WriteValue()` nel codice di convalida.  
  
### Convalida implicita ed esplicita  
 Quando vengono convalidati i dati di un controllo?  dipende dallo sviluppatore.  È possibile utilizzare la convalida implicita o esplicita, a seconda delle esigenze dell'applicazione.  
  
#### Convalida implicita  
 La convalida implicita convalida i dati mentre l'utente li immette.  È possibile convalidare i dati mentre vengono immessi in un controllo leggendo i tasti durante la pressione, o più comunemente ogni qualvolta l'utente sposta lo stato attivo dell'input da un controllo a quello successivo.  Questo approccio è utile quando si desidera dare all'utente un feedback immediato sui dati che sta elaborando.  
  
 Se si desidera utilizzare la convalida implicita per un controllo, è necessario impostare la proprietà <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> del controllo su `true`.  Se si annulla l'evento <xref:System.Windows.Forms.Control.Validating>, il comportamento del controllo verrà determinato dal valore assegnato a <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A>.  Se è stato assegnato il membro <xref:System.Windows.Forms.AutoValidate>, l'annullamento dell'evento impedirà il verificarsi dell'evento <xref:System.Windows.Forms.Control.Validated>.  Lo stato di attivazione rimarrà sul controllo corrente fino a quando l'utente non modifica i dati in un formato valido.  Se è stato assegnato <xref:System.Windows.Forms.AutoValidate>, l'evento <xref:System.Windows.Forms.Control.Validated> non verrà generato quando si annulla l'evento, ma lo stato di attivazione passerà al controllo successivo.  
  
 L'assegnazione del membro <xref:System.Windows.Forms.AutoValidate> alla proprietà <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> impedisce del tutto la convalida implicita.  Per convalidare i controlli, sarà necessario utilizzare la convalida esplicita.  
  
#### Convalida esplicita  
 La convalida esplicito convalida i dati contemporaneamente.  È possibile convalidare i dati in risposta a un'azione dell'utente, ad esempio facendo clic su un pulsante Salva o un collegamento Avanti.  Quando si verifica l'azione dell'utente, è possibile attivare la convalida esplicita in una delle modalità seguenti:  
  
-   Chiamare <xref:System.Windows.Forms.ContainerControl.Validate%2A> per convalidare l'ultimo controllo nello stato di attivazione.  
  
-   Chiamare <xref:System.Windows.Forms.ContainerControl.ValidateChildren%2A> per convalidare tutti i controlli figlio in un form o un controllo contenitore.  
  
-   Chiamare un metodo personalizzato per convalidare manualmente i dati nei controlli.  
  
#### Comportamento predefinito della convalida implicita per controlli Windows Form  
 I diversi controlli Windows Form dispongono di valori predefiniti diversi per la relativa proprietà <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A>.  Nella tabella riportata di seguito sono elencati i controlli più comuni e le relative impostazioni predefinite.  
  
|Controllo|Comportamento predefinito della convalida|  
|---------------|-----------------------------------------------|  
|<xref:System.Windows.Forms.ContainerControl>|<xref:System.Windows.Forms.AutoValidate>|  
|<xref:System.Windows.Forms.Form>|<xref:System.Windows.Forms.AutoValidate>|  
|<xref:System.Windows.Forms.PropertyGrid>|Proprietà non esposta in Visual Studio|  
|<xref:System.Windows.Forms.ToolStripContainer>|Proprietà non esposta in Visual Studio|  
|<xref:System.Windows.Forms.SplitContainer>|<xref:System.Windows.Forms.AutoValidate>|  
|<xref:System.Windows.Forms.UserControl>|<xref:System.Windows.Forms.AutoValidate>|  
  
## Chiusura del form e override della convalida  
 Quando un controllo mantiene lo stato attivo perché i dati contenuti non sono validi, è impossibile chiudere il form padre in uno di metodi usuali:  
  
-   Facendo clic sul pulsante **Chiudi**.  
  
-   Scegliendo **Chiudi** dal menu **Sistema**.  
  
-   Chiamano il metodo <xref:System.Windows.Forms.Form.Close%2A> a livello di codice  
  
 Talvolta può essere utile permettere all'utente di chiudere il form indipendentemente dalla validità dei valori nei controlli.  È possibile eseguire l'override della convalida e chiudere un form che contiene ancora dati non validi mediante la creazione di un gestore per l'evento <xref:System.Windows.Forms.Form.Closing> del form.  Nell'evento impostare la proprietà <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> su `false`.  Con questa operazione viene imposta la chiusura del form.  Per ulteriori informazioni e un esempio, vedere <xref:System.Windows.Forms.Form.Closing?displayProperty=fullName>.  
  
> [!NOTE]
>  Se si impone la chiusura del form in questo modo, le informazioni presenti nei controlli del form e non ancora salvate andranno perdute.  I form modali inoltre non consentono la convalida del contenuto dei controlli quando vengono chiusi.  È tuttavia possibile utilizzare la convalida per bloccare lo stato attivo di un controllo, ma non se si è interessati al comportamento relativo alla chiusura del form.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Control.Validating?displayProperty=fullName>   
 <xref:System.Windows.Forms.Form.Closing?displayProperty=fullName>   
 <xref:System.ComponentModel.CancelEventArgs?displayProperty=fullName>   
 [Controllo MaskedTextBox](../../../docs/framework/winforms/controls/maskedtextbox-control-windows-forms.md)   
 [Esempi di espressioni regolari](../../../docs/standard/base-types/regular-expression-examples.md)