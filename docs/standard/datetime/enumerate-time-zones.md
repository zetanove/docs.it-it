---
title: "Procedura: enumerare i fusi orari presenti in un computer | Microsoft Docs"
ms.custom: ""
ms.date: "04/10/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "enumerazione dei fusi orari [.NET Framework]"
  - "fusi orari [.NET Framework], enumerazione"
ms.assetid: bb7a42ab-6bd9-4c5c-b734-5546d51f8669
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: enumerare i fusi orari presenti in un computer
Per poter utilizzare correttamente un determinato fuso orario è necessario che le relative informazioni siano disponibili nel sistema.  Nei sistemi operativi Windows XP e Windows Vista tali informazioni vengono archiviate nel Registro di sistema.  Sebbene nel mondo esistano molti fusi orari, le informazioni presenti nel Registro di sistema sono tuttavia relative solo a una parte di essi.  Inoltre, il Registro di sistema è una struttura dinamica il cui contenuto è soggetto a modifiche intenzionali e accidentali.  Di conseguenza, un'applicazione non può sempre presupporre che un determinato fuso orario sia definito e disponibile in un sistema.  Il primo passaggio per molte applicazioni che si basano sulle informazioni del fuso orario è determinare se i fusi orari richiesti sono disponibili nel sistema locale o fornire all'utente un elenco di fusi orari da selezionare.  A tale scopo, è necessario che un'applicazione sia in grado di enumerare i fusi orari definiti in un sistema locale.  
  
> [!NOTE]
>  Se un'applicazione si basa sulla presenza di un determinato fuso orario che non può essere definito in un sistema locale, è possibile garantirne la presenza serializzando e deserializzando le informazioni sul fuso orario.  È quindi possibile aggiungere il fuso orario a un elenco in modo da poter essere selezionato dall'utente dell'applicazione.  Per ulteriori informazioni, vedere [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) e [Procedura: ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md).  
  
### Per enumerare i fusi orari presenti nel sistema locale  
  
1.  Chiamare il metodo <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=fullName>.  Il metodo restituisce una raccolta <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> generica di oggetti <xref:System.TimeZoneInfo>.  Le voci della raccolta sono ordinate in base alla relativa proprietà <xref:System.TimeZoneInfo.DisplayName%2A>.  Di seguito è riportato un esempio.  
  
     [!code-csharp[System.TimeZone2.Concepts#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#1)]
     [!code-vb[System.TimeZone2.Concepts#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#1)]  
  
2.  Enumerare i singoli oggetti <xref:System.TimeZoneInfo> della raccolta utilizzando un ciclo `foreach` \(in C\#\) o un ciclo `For Each`.`Next` \(in Visual Basic\) ed eseguire tutte le elaborazioni necessarie su ogni oggetto.  Nel codice seguente, ad esempio, viene enumerata la raccolta <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> degli oggetti <xref:System.TimeZoneInfo> restituiti nel passaggio 1 ed elencato il nome visualizzato di ogni fuso orario nella console.  
  
     [!code-csharp[System.TimeZone2.Concepts#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#12)]
     [!code-vb[System.TimeZone2.Concepts#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#12)]  
  
### Per visualizzare un elenco di fusi orari presenti nel sistema locale  
  
1.  Chiamare il metodo <xref:System.TimeZoneInfo.GetSystemTimeZones%2A?displayProperty=fullName>.  Il metodo restituisce una raccolta <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> generica di oggetti <xref:System.TimeZoneInfo>.  
  
2.  Assegnare la raccolta restituita nel passaggio 1 alla proprietà `DataSource` di un controllo elenco Windows Forms o ASP.NET.  
  
3.  Recuperare l'oggetto <xref:System.TimeZoneInfo> selezionato dall'utente.  
  
 L'esempio si riferisce a un'applicazione Windows.  
  
## Esempio  
 Nell'esempio viene avviata un'applicazione Windows in cui i fusi orari definiti in un sistema vengono visualizzati in una casella di riepilogo.  Nell'esempio viene quindi visualizzata una finestra di dialogo che contiene il valore della proprietà <xref:System.TimeZoneInfo.DisplayName%2A> dell'oggetto del fuso orario selezionato dall'utente.  
  
 [!code-csharp[System.TimeZone2.Concepts#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#2)]
 [!code-vb[System.TimeZone2.Concepts#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#2)]  
  
 La maggior parte dei controlli elenco, ad esempio il controllo <xref:System.Windows.Forms.ListBox?displayProperty=fullName> o <xref:System.Web.UI.WebControls.BulletedList?displayProperty=fullName>, consente di assegnare una raccolta di variabili oggetto alla relativa proprietà `DataSource`, purché tale raccolta implementi l'interfaccia <xref:System.Collections.IEnumerable>. Tale operazione viene eseguita dalla classe <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>. Per visualizzare un singolo oggetto della raccolta, il controllo chiama il metodo `ToString` di tale oggetto per estrarre la stringa utilizzata per rappresentare l'oggetto.  Nel caso di oggetti <xref:System.TimeZoneInfo>, il metodo `ToString` restituisce il nome visualizzato dell'oggetto <xref:System.TimeZoneInfo> \(il valore della relativa proprietà <xref:System.TimeZoneInfo.DisplayName%2A>\).  
  
> [!NOTE]
>  Poiché i controlli elenco chiamano il metodo `ToString` di un oggetto, è possibile assegnare una raccolta di oggetti <xref:System.TimeZoneInfo> al controllo, visualizzare un nome significativo per ogni oggetto del controllo e recuperare l'oggetto <xref:System.TimeZoneInfo> selezionato dall'utente.  In questo modo non è più necessario estrarre una stringa per ogni oggetto della raccolta, assegnare la stringa a una raccolta assegnata a sua volta alla proprietà `DataSource` del controllo, recuperare la stringa selezionata dall'utente e infine utilizzare questa stringa per estrarre l'oggetto descritto.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Core.dll al progetto.  
  
-   Importare gli spazi dei nomi seguenti:  
  
     <xref:System> \(in codice C\#\)  
  
     <xref:System.Collections.ObjectModel>  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)   
 [Procedura: ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)