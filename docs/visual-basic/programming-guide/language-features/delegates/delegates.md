---
title: "Delegates (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "delegates [Visual Basic]"
  - "Visual Basic code, delegates"
ms.assetid: 410b60dc-5e60-4ec0-bfae-426755a2ee28
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Delegates (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

I delegati sono oggetti che fanno riferimento ai metodi.  Talvolta sono anche descritti come *puntatori a funzione indipendenti dai tipi* in quanto sono analoghi ai puntatori a funzione utilizzati in altri linguaggi di programmazione.  Tuttavia, diversamente dai puntatori a funzione, i delegati [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] rappresentano un tipo di riferimento basato sulla classe <xref:System.Delegate?displayProperty=fullName>.  I delegati possono fare riferimento sia ai metodi condivisi, ovvero metodi che possono essere chiamati senza un'istanza specifica di una classe, che ai metodi di istanza.  
  
## Delegati ed eventi  
 I delegati risultano utili laddove è necessario un intermediario tra una routine chiamante e la routine che viene richiamata.  Si supponga, ad esempio, di desiderare che un oggetto che genera eventi sia in grado di richiamare diversi gestori di eventi in diverse circostanze.  Purtroppo, l'oggetto che genera gli eventi non può prevedere quale gestore eventi gestirà uno specifico evento.  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente di associare in modo dinamico i gestori eventi agli eventi mediante la creazione di un delegato quando viene utilizzata l'istruzione `AddHandler`.  In fase di esecuzione, il delegato inoltrerà le chiamate al gestore di eventi appropriato.  
  
 Sebbene sia possibile creare manualmente i delegati, nella maggior parte dei casi [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] crea automaticamente il delegato con tutti i dettagli necessari.  Un'istruzione `Event` ad esempio consente di definire implicitamente una classe delegata denominata `<EventName>EventHandler` come classe annidata della classe contenente l'istruzione `Event` e con la stessa firma dell'evento.  L'istruzione `AddressOf` crea in modo implicito un'istanza di un delegato che fa riferimento a una routine specifica.  Le seguenti due righe di codice sono equivalenti:  Nella prima riga, si vede la creazione esplicita di un'istanza di `Eventhandler`, con un riferimento a metodo `Button1_Click` inviato come argomento.  La seconda riga è un modo più pratico per eseguire la stessa operazione.  
  
 [!code-vb[VbVbalrDelegates#6](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_1.vb)]  
  
 È possibile utilizzare il metodo abbreviato per creare delegati ogni volta che il compilatore è in grado di determinare il tipo del delegato in base al contesto.  
  
## Dichiarazione di eventi che utilizzano un tipo delegato esistente  
 In alcune situazioni, è possibile dichiarare un evento che utilizzi un tipo delegato esistente come proprio delegato sottostante.  Di seguito è fornito un esempio al riguardo:  
  
 [!code-vb[VbVbalrDelegates#7](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_2.vb)]  
  
 Questa operazione si rivela utile quando si desidera instradare più eventi sullo stesso gestore.  
  
## Parametri e variabili dei delegati  
 È possibile utilizzare i delegati per altre attività non relative a eventi, quali i modelli di threading Free, o con routine che richiedono la chiamata di diverse versioni delle funzioni in fase di esecuzione.  
  
 Ad esempio, si supponga di avere un'applicazione di annunci pubblicitari che include una casella di riepilogo contenente nomi di automobili.  Gli annunci sono ordinati per titolo, che generalmente corrisponde al modello dell'auto.  Si potrebbe verificare un problema qualora il modello di alcune auto fosse preceduto dall'anno di produzione.  Il problema consiste nel fatto che la funzionalità di ordinamento incorporata della casella di riepilogo effettua l'ordinamento solo in base ai codici dei caratteri, posizionando prima tutti gli annunci che iniziano con una data, quindi tutti quelli che iniziano con il modello.  
  
 Per risolvere questo problema, è possibile creare una routine di ordinamento in una classe che utilizzi l'ordinamento alfabetico standard per la maggior parte delle caselle di riepilogo, ma che sia in grado di passare, in fase di esecuzione, alla routine di ordinamento personalizzata per gli annunci relativi alle automobili.  A questo scopo, è necessario passare la routine di ordinamento personalizzata alla classe di ordinamento in fase di esecuzione, utilizzando i delegati.  
  
## Operatore AddressOf ed espressioni lambda  
 Ogni classe delegata definisce un costruttore al quale viene passata la specifica di un metodo di oggetto.  Un argomento di un costruttore di delegato deve essere un riferimento a un metodo o a un'espressione lambda.  
  
 Per specificare un riferimento a un metodo, utilizzare la seguente sintassi:  
  
 `AddressOf` \[`expression`.\]`methodName`  
  
 In fase di compilazione per il tipo di `expression` è necessario specificare il nome di una classe o di un'interfaccia contenente un metodo con il nome specificato e con firma corrispondente a quella della classe delegata.  `methodName` può essere un metodo condiviso o di istanza  ma non è facoltativo, anche se si crea un delegato per il metodo predefinito della classe.  
  
 Per specificare un'espressione lambda, utilizzare la seguente sintassi:  
  
 `Function` \(\[`parm` As `type`, `parm2` As `type2`, ...\]\) `expression`  
  
 L'esempio seguente mostra sia l'operatore `AddressOf` sia espressioni lambda utilizzati per specificare il riferimento per un delegato.  
  
 [!code-vb[VbVbalrDelegates#15](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/delegates_3.vb)]  
  
 La firma della funzione deve corrispondere a quella del tipo delegato.  Per ulteriori informazioni sulle espressioni lambda, vedere [Lambda Expressions](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  Per ulteriori esempi di assegnazioni dell'espressione lambda e `AddressOf` ai delegati, vedere [Relaxed Delegate Conversion](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[How to: Invoke a Delegate Method](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)|Viene fornito un esempio in cui viene illustrato come associare un metodo a un delegato e quindi richiamare il metodo tramite il delegato stesso.|  
|[How to: Pass Procedures to Another Procedure in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)|Viene illustrato come passare una routine a un'altra routine con l'ausilio dei delegati.|  
|[Relaxed Delegate Conversion](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)|Viene descritto come è possibile assegnare subroutine e funzioni a delegati o gestori anche quando le firme non sono identiche.|  
|[Events](../../../../visual-basic/programming-guide/language-features/events/events.md)|Vengono forniti i cenni preliminari sugli eventi di Visual Basic.|