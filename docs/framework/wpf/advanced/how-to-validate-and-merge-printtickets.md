---
title: "Procedura: convalidare e unire PrintTicket | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "unione di PrintTicket"
  - "PrintTicket, unione"
  - "PrintTicket, convalida"
  - "convalida di PrintTicket"
ms.assetid: 4fe2d501-d0b0-4fef-86af-6ffe6c162532
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Procedura: convalidare e unire PrintTicket
Lo [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] [schema di stampa](http://go.microsoft.com/fwlink/?LinkId=186397) include elementi <xref:System.Printing.PrintCapabilities> e <xref:System.Printing.PrintTicket> flessibili ed estensibili.  Il primo specifica le funzionalità di un dispositivo di stampa, mentre il secondo specifica in che modo il dispositivo deve utilizzare tali funzionalità in relazione a una determinata sequenza di documenti, a un singolo documento o a una singola pagina.  
  
 Di seguito viene riportata una sequenza di attività tipica per un'applicazione che supporta la stampa.  
  
1.  Determinare le funzionalità di una stampante.  
  
2.  Configurare <xref:System.Printing.PrintTicket> affinché utilizzi tali funzionalità.  
  
3.  Convalidare <xref:System.Printing.PrintTicket>.  
  
 In questo articolo viene illustrato come eseguire queste operazioni.  
  
## Esempio  
 Nel semplice esempio riportato di seguito viene unicamente stabilito se la stampante è in grado di supportare la stampa fronte retro.  La procedura principale è la seguente.  
  
1.  Ottenere un oggetto <xref:System.Printing.PrintCapabilities> con il metodo <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>.  
  
2.  Verificare la presenza della funzionalità desiderata.  Nell'esempio riportato di seguito viene eseguito il test della proprietà <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> dell'oggetto <xref:System.Printing.PrintCapabilities> per verificare la presenza della funzionalità di stampa fronte retro con il capovolgimento della pagina sul lato lungo.  Poiché <xref:System.Printing.PrintCapabilities.DuplexingCapability%2A> è una raccolta, viene utilizzato il metodo `Contains` di <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>.  
  
    > [!NOTE]
    >  Questo passaggio non è strettamente necessario.  Tramite il metodo <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> utilizzato di seguito verrà controllata ogni richiesta in <xref:System.Printing.PrintTicket> rispetto alle funzionalità della stampante.  Se la funzionalità richiesta non è supportata dalla stampante, il driver della stampante sostituirà una richiesta alternativa nell'oggetto <xref:System.Printing.PrintTicket> restituito dal metodo.  
  
3.  Se la stampante supporta la stampa fronte retro, nel codice di esempio viene creato un oggetto <xref:System.Printing.PrintTicket> che richiede la stampa fronte retro.  L'applicazione, tuttavia, non specifica ogni possibile impostazione della stampante disponibile nell'elemento <xref:System.Printing.PrintTicket>.  Questa operazione implicherebbe un notevole dispendio di tempo da parte del programmatore e del programma.  Nel codice, invece, viene impostata solo la richiesta di stampa fronte retro e, successivamente, questo oggetto <xref:System.Printing.PrintTicket> viene unito a un oggetto <xref:System.Printing.PrintTicket> esistente, completamente configurato e convalidato, in questo caso l'oggetto <xref:System.Printing.PrintTicket> predefinito dell'utente.  
  
4.  Di conseguenza, nell'esempio viene chiamato il metodo <xref:System.Printing.PrintQueue.MergeAndValidatePrintTicket%2A> per unire il nuovo oggetto <xref:System.Printing.PrintTicket> minimo all'oggetto <xref:System.Printing.PrintTicket> predefinito dell'utente.  Viene restituito un oggetto <xref:System.Printing.ValidationResult> che include il nuovo oggetto <xref:System.Printing.PrintTicket> come una sua proprietà.  
  
5.  Nell'esempio viene quindi testato che il nuovo oggetto <xref:System.Printing.PrintTicket> richieda la stampa fronte retro.  In caso affermativo, viene impostato come nuovo Print Ticket predefinito per l'utente.  Se il passaggio 2 precedente viene omesso e la stampante non supporta la stampa fronte retro sul lato lungo, il risultato del test sarebbe `false`.  Vedere la nota riportata sopra.  
  
6.  L'ultimo passaggio significativo consiste nell'eseguire il commit della modifica apportata alla proprietà <xref:System.Printing.PrintQueue.UserPrintTicket%2A> dell'oggetto <xref:System.Printing.PrintQueue> con il metodo <xref:System.Printing.PrintQueue.Commit%2A>.  
  
 [!code-csharp[PrintTicketManagment#UsingMergeAndValidate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#usingmergeandvalidate)]
 [!code-vb[PrintTicketManagment#UsingMergeAndValidate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#usingmergeandvalidate)]  
  
 Allo scopo di eseguire rapidamente il test di questo esempio, la parte restante viene presentata di seguito.  Creare un progetto e uno spazio dei nomi, quindi incollare entrambi i frammenti di codice di questo articolo nel blocco dello spazio dei nomi.  
  
 [!code-csharp[PrintTicketManagment#UIForMergeAndValidatePTUtility](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrintTicketManagment/CSharp/printticket.cs#uiformergeandvalidateptutility)]
 [!code-vb[PrintTicketManagment#UIForMergeAndValidatePTUtility](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrintTicketManagment/visualbasic/printticket.vb#uiformergeandvalidateptutility)]  
  
## Vedere anche  
 <xref:System.Printing.PrintCapabilities>   
 <xref:System.Printing.PrintTicket>   
 <xref:System.Printing.PrintServer.GetPrintQueues%2A>   
 <xref:System.Printing.PrintServer>   
 <xref:System.Printing.EnumeratedPrintQueueTypes>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Printing.PrintQueue.GetPrintCapabilities%2A>   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [Schema di stampa](http://go.microsoft.com/fwlink/?LinkId=186397)