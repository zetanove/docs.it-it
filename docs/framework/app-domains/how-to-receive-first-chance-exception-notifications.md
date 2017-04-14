---
title: "Procedura: ricevere notifiche di eccezioni first-chance | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "eccezioni, notifiche first-chance"
  - "notifica di eccezioni first-chance"
ms.assetid: 66f002b8-a97d-4a6e-a503-2cec01689113
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: ricevere notifiche di eccezioni first-chance
L'evento <xref:System.AppDomain.FirstChanceException> della classe <xref:System.AppDomain> consente di ricevere una notifica in cui si informa che è stata generata un'eccezione, prima che Common Language Runtime cominci a cercare gestori di eccezioni.  
  
 L'evento viene generato a livello di dominio applicazione.  Un thread di esecuzione può passare attraverso più domini applicazione, pertanto un'eccezione che non viene gestita in un dato dominio applicazione può essere gestita in un altro dominio applicazione.  La notifica si verifica in ogni dominio applicazione che ha aggiunto un gestore per l'evento, finché un dominio applicazione non gestisce l'eccezione.  
  
 Le procedure e gli esempi in questo articolo mostrano come ricevere notifiche di eccezioni first\-chance in un programma semplice che presenta un solo dominio applicazione e in un dominio applicazione che si crea.  
  
 Per un esempio più complesso che riguarda più domini applicazione, vedere l'esempio relativo all'evento <xref:System.AppDomain.FirstChanceException>.  
  
## Ricezione di notifiche di eccezioni first\-chance nel dominio applicazione predefinito  
 Nella procedura riportata di seguito il punto di ingresso per l'applicazione, il metodo `Main()`, viene eseguito nel dominio applicazione predefinito.  
  
#### Per visualizzare notifiche di eccezioni first\-chance nel dominio applicazione predefinito  
  
1.  Definire un gestore eventi per l'evento <xref:System.AppDomain.FirstChanceException> mediante una funzione lambda e collegarlo all'evento.  In questo esempio, il gestore eventi stampa il nome del dominio applicazione in cui l'evento è stato gestito e la proprietà <xref:System.Exception.Message%2A> dell'eccezione.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#2)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#2)]  
  
2.  Generare un'eccezione e rilevarla.  Prima che il runtime individui il gestore eccezioni, viene generato l'evento <xref:System.AppDomain.FirstChanceException> che visualizza un messaggio.  Questo messaggio è seguito dal messaggio visualizzato dal gestore eccezioni.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#3)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#3)]  
  
3.  Generare un'eccezione, ma non rilevarla.  Prima che il runtime cerchi un gestore eccezioni, viene generato l'evento <xref:System.AppDomain.FirstChanceException> che visualizza un messaggio.  Poiché non c'è alcun gestore di eccezioni, l'applicazione viene chiusa.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#4)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#4)]  
  
     Il codice visualizzato nei primi tre passaggi di questa procedura forma un'applicazione console completa.  L'output dell'applicazione varia a seconda del nome del file con estensione exe, perché il nome del dominio applicazione predefinito è costituito dal nome e dall'estensione del file exe.  Di seguito viene riportato output di esempio.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto_simple#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/cs/example.cs#5)]
     [!code-vb[System.AppDomain.FirstChanceException_howto_simple#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto_simple/vb/example.vb#5)]  
  
## Ricezione di notifiche di eccezioni first\-chance in un altro dominio applicazione  
 Se il programma contiene più domini applicazione, è possibile scegliere quali domini applicazione riceveranno le notifiche.  
  
#### Per ricevere notifiche di eccezioni first\-chance in un dominio applicazione che si crea  
  
1.  Definire un gestore eventi per l'evento <xref:System.AppDomain.FirstChanceException>.  In questo esempio viene utilizzato un metodo `static` \(`Shared` in Visual Basic\) che stampa il nome del dominio applicazione in cui l'evento viene gestito e la proprietà <xref:System.Exception.Message%2A> dell'eccezione.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#3)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#3)]  
  
2.  Creare un dominio applicazione e aggiungere il gestore eventi all'evento <xref:System.AppDomain.FirstChanceException> relativo a tale dominio applicazione.  In questo esempio il dominio applicazione è denominato `AD1`.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#2)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#2)]  
  
     È possibile gestire questo evento nel dominio applicazione predefinito nello stesso modo.  Utilizzare la proprietà <xref:System.AppDomain.CurrentDomain%2A?displayProperty=fullName> `static` \(`Shared` in Visual Basic\) in `Main()` per ottenere un riferimento al dominio applicazione predefinito.  
  
#### Per visualizzare notifiche di eccezioni first\-chance nel dominio applicazione  
  
1.  Creare un oggetto `Worker` nel dominio applicazione creato nella procedura precedente.  La classe `Worker` deve essere pubblica e deve derivare da <xref:System.MarshalByRefObject>, come mostrato nell'esempio completo alla fine di questo articolo.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#4)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#4)]  
  
2.  Chiamare un metodo dell'oggetto `Worker` che genera un'eccezione.  In questo esempio il metodo `Thrower` viene chiamato due volte.  La prima volta, l'argomento del metodo è `true`. Ciò fa in modo che il metodo rilevi la propria eccezione.  La seconda volta, l'argomento è `false` e il metodo `Main()` rileva l'eccezione nel dominio applicazione predefinito.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#6)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#6)]  
  
3.  Inserire codice nel metodo `Thrower` per controllare se il metodo gestisce la propria eccezione.  
  
     [!code-csharp[System.AppDomain.FirstChanceException_howto#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#5)]
     [!code-vb[System.AppDomain.FirstChanceException_howto#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#5)]  
  
## Esempio  
 Nell'esempio seguente viene creato un dominio applicazione denominato `AD1` e viene aggiunto un gestore eventi all'evento <xref:System.AppDomain.FirstChanceException> del dominio applicazione.  Nell'esempio viene creata un'istanza della classe `Worker` nel dominio applicazione e viene chiamato un metodo denominato `Thrower` che genera un oggetto <xref:System.ArgumentException>.  A seconda del valore del proprio argomento, il metodo rileva l'eccezione o non riesce a gestirla.  
  
 Ogni volta che il metodo `Thrower` genera un'eccezione in `AD1`, l'evento <xref:System.AppDomain.FirstChanceException> viene generato in `AD1` e il gestore eventi visualizza un messaggio.  Quindi, il runtime cerca un gestore di eccezioni.  Nel primo caso, il gestore di eccezioni viene trovato in `AD1`.  Nel secondo caso, anziché essere gestita in `AD1`, l'eccezione viene rilevata nel dominio applicazione predefinito.  
  
> [!NOTE]
>  Il nome del dominio applicazione predefinito è uguale al nome dell'eseguibile.  
  
 Se si aggiunge un gestore per l'evento <xref:System.AppDomain.FirstChanceException> al dominio applicazione predefinito, l'evento viene generato e gestito prima che il dominio applicazione predefinito gestisca l'eccezione.  Per vedere ciò, aggiungere il codice C\# `AppDomain.CurrentDomain.FirstChanceException += FirstChanceException;` \(in Visual Basic `AddHandler AppDomain.CurrentDomain.FirstChanceException, FirstChanceExceptio`n\) all'inizio di `Main()`.  
  
 [!code-csharp[System.AppDomain.FirstChanceException_howto#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/cs/example.cs#1)]
 [!code-vb[System.AppDomain.FirstChanceException_howto#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.firstchanceexception_howto/vb/example.vb#1)]  
  
## Compilazione del codice  
  
-   Questo esempio è un'applicazione della riga di comando.  Per compilare ed eseguire questo codice in [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)], aggiungere il codice C\# `Console.ReadLine();` \(in Visual Basic `Console.ReadLine()`\) alla fine di `Main()` per impedire la chiusura della finestra di comando prima che sia possibile leggere l'output.  
  
## Vedere anche  
 <xref:System.AppDomain.FirstChanceException>