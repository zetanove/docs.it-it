---
title: "RaiseEvent Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.RaiseEventMethod"
  - "vb.RaiseEvent"
  - "RaiseEvent"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "raising events, RaiseEvent statement"
  - "RaiseEvent statement"
  - "event handlers, connecting events to"
ms.assetid: f82e380a-1e6b-4047-bea8-c853f4d2c742
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# RaiseEvent Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di attivare un evento dichiarato a livello di modulo in una classe, form o documento.  
  
## Sintassi  
  
```  
RaiseEvent eventname[( argumentlist )]  
```  
  
## Parti  
 `eventname`  
 Obbligatorio.  Nome dell'evento da attivare.  
  
 `argumentlist`  
 Parametro facoltativo.  Elenco di variabili, matrici o espressioni delimitate da virgole.  È necessario che l'argomento `argumentlist` sia racchiuso tra parentesi.  Se non vi sono argomenti, omettere le parentesi.  
  
## Note  
 Il valore obbligatorio di `eventname` è il nome di un evento dichiarato nel modulo  conforme alle convenzioni di denominazione delle variabili di Visual Basic.  
  
 Se l'evento non è stato dichiarato nel modulo nel quale viene generato si verificherà un errore.  Nel frammento seguente vengono illustrate una dichiarazione di evento e una routine di generazione dell'evento.  
  
 [!code-vb[VbVbalrEvents#37](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_1.vb)]  
  
 Non è possibile utilizzare `RaiseEvent` per generare eventi non dichiarati in modo esplicito nel modulo.  Se ad esempio tutti i form ereditano un evento <xref:System.Windows.Forms.Control.Click> da <xref:System.Windows.Forms.Form?displayProperty=fullName>, non è possibile generare tale evento mediante `RaiseEvent` in un form derivato.  Se si dichiara un evento `Click` nel modulo del form, esso nasconde l'evento <xref:System.Windows.Forms.Control.Click> del form.  È ancora possibile richiamare l'evento <xref:System.Windows.Forms.Control.Click> del form chiamando il metodo <xref:System.Windows.Forms.Control.OnClick%2A>.  
  
 Per impostazione predefinita, un evento definito in Visual Basic viene generato nel relativo gestore eventi nell'ordine di istituzione delle connessioni.  Dato che gli eventi possono essere dotati di parametri `ByRef`, a un processo collegato in seguito possono essere passati parametri modificati da un precedente gestore eventi.  Dopo l'esecuzione del gestore eventi, il controllo viene restituito alla subroutine che ha generato l'evento.  
  
> [!NOTE]
>  Gli eventi non condivisi non devono essere generati all'interno del costruttore della classe in cui sono dichiarati.  Sebbene questi eventi non causino errori di runtime, è possibile che non vengano rilevati dai gestori eventi associati.  Utilizzare il modificatore `Shared` per creare un evento condiviso se è necessario generare un evento da un costruttore.  
  
> [!NOTE]
>  Per modificare il comportamento predefinito degli eventi, specificare un evento personalizzato.  Per eventi personalizzati, l'istruzione `RaiseEvent` consente di richiamare la funzione di accesso `RaiseEvent` dell'evento.  Per ulteriori informazioni sugli eventi personalizzate, vedere [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## Esempio  
 Nell'esempio seguente vengono utilizzati eventi per il conteggio dei secondi da 10 a 0.  Nel codice sono riportati numerosi metodi, proprietà e istruzioni correlati agli eventi, inclusa l'istruzione `RaiseEvent`.  
  
 La classe che genera l'evento viene definita origine e i metodi che lo elaborano vengono definiti gestori eventi.  Un'origine eventi può disporre di più gestori per gli eventi generati.  La generazione di un evento da parte di una classe si verifica anche in tutte le classi per le quali è stato scelto di gestire eventi per tale istanza dell'oggetto.  
  
 Nell'esempio vengono inoltre utilizzati un form \(`Form1`\) con un pulsante \(`Button1`\) e una casella di testo \(`TextBox1`\).  Quando si fa clic sul pulsante, nella prima casella di testo viene visualizzato un conto alla rovescia da 10 a 0 secondi.  Allo scadere dei 10 secondi nella prima casella di testo viene visualizzato "Completato".  
  
 Nel codice di `Form1` sono specificati gli stati di inizio e fine del form,  nonché il codice eseguito quando vengono generati gli eventi.  
  
 Per utilizzare questo esempio, aprire un nuovo progetto di applicazione Windows, aggiungere un pulsante denominato `Button1` e una casella di testo denominata `TextBox1` al form principale con nome `Form1`.  Fare quindi clic con il pulsante destro del mouse sul form e scegliere **Visualizza codice** per aprire l'editor del codice.  
  
 Aggiungere una variabile `WithEvents` alla sezione delle dichiarazioni della classe `Form1`.  
  
 [!code-vb[VbVbalrEvents#14](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_2.vb)]  
  
## Esempio  
 Aggiungere il codice seguente al codice per `Form1`.  Sostituire eventuali procedure duplicate, ad esempio `Form_Load` o `Button_Click`.  
  
 [!code-vb[VbVbalrEvents#15](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/raiseevent-statement_3.vb)]  
  
 Premere F5 per eseguire l'esempio precedente, quindi fare clic sul pulsante con etichetta **Start**.  Verrà avviato il conto alla rovescia dei secondi nella prima casella di testo.  Allo scadere dei 10 secondi nella prima casella di testo viene visualizzato "Completato".  
  
> [!NOTE]
>  Per l'elaborazione degli eventi, il metodo `My.Application.DoEvents` si comporta in modo leggermente diverso rispetto al form.  Per consentire al form di gestire gli eventi direttamente, è possibile ricorrere al multithreading.  Per ulteriori informazioni, vedere [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Vedere anche  
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)   
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [AddHandler Statement](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [RemoveHandler Statement](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)