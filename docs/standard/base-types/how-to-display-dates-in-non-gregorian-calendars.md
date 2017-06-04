---
title: "Procedura: Visualizzare le date in calendari non gregoriani | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "formattazione [.NET Framework], date"
  - "date [.NET Framework], formattazione"
  - "calendari [.NET Framework], visualizzazione di date"
  - "visualizzazione di dati relativi a data e ora"
ms.assetid: ed324eff-4aff-4a76-b6c0-04e6c0d8f5a9
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: Visualizzare le date in calendari non gregoriani
I tipi <xref:System.DateTime> e <xref:System.DateTimeOffset> utilizzano il calendario gregoriano come calendario predefinito.  Ciò significa che la chiamata al metodo `ToString` di un valore di data e ora visualizza la rappresentazione di stringa di tale data e ora nel calendario gregoriano, anche se la data e l'ora sono state create utilizzando un altro calendario.  Questo processo viene illustrato nell'esempio riportato di seguito in cui vengono utilizzate due modalità diverse per creare un valore di data e ora con il calendario persiano ma i valori vengono visualizzati nel calendario gregoriano quando viene chiamato il metodo <xref:System.DateTime.ToString%2A>.  L'esempio riflette due tecniche comuni non corrette per la visualizzazione della data in un determinato calendario.  
  
 [!code-csharp[Formatting.HowTo.Calendar#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#1)]
 [!code-vb[Formatting.HowTo.Calendar#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#1)]  
  
 Per visualizzare la data in un determinato calendario è possibile utilizzare due tecniche differenti.  La prima richiede che il calendario sia il calendario predefinito per determinate impostazioni cultura.  La seconda può essere utilizzata con qualsiasi calendario.  
  
### Per visualizzare la data per il calendario predefinito di determinate impostazione cultura  
  
1.  Creare un'istanza di un oggetto calendario derivato dalla classe <xref:System.Globalization.Calendar> che rappresenta il calendario da utilizzare.  
  
2.  Creare un'istanza di un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura la cui formattazione verrà utilizzata per la visualizzazione della data.  
  
3.  Chiamare il metodo <xref:System.Array.Exists%2A?displayProperty=fullName> per determinare se l'oggetto calendario è un membro della matrice restituita dalla proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName>.  Ciò indica che il calendario può fungere da calendario predefinito per l'oggetto <xref:System.Globalization.CultureInfo>.  Se non è un membro della matrice, seguire le istruzioni riportate nella sezione "Per visualizzare la data in un calendario qualsiasi".  
  
4.  Assegnare l'oggetto calendario alla proprietà <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A> dell'oggetto <xref:System.Globalization.DateTimeFormatInfo> restituito dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName>.  
  
    > [!NOTE]
    >  La classe <xref:System.Globalization.CultureInfo> dispone anche di una proprietà <xref:System.Globalization.CultureInfo.Calendar%2A>.  È tuttavia costante e di sola lettura e non viene modificata per riflettere il nuovo calendario predefinito assegnato alla proprietà <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=fullName>.  
  
5.  Chiamare il metodo <xref:System.DateTime.ToString%2A> o <xref:System.DateTime.ToString%2A> e passare l'oggetto <xref:System.Globalization.CultureInfo> il cui calendario predefinito è stato modificato nel passaggio precedente.  
  
### Per visualizzare la data in un calendario qualsiasi  
  
1.  Creare un'istanza di un oggetto calendario derivato dalla classe <xref:System.Globalization.Calendar> che rappresenta il calendario da utilizzare.  
  
2.  Determinare gli elementi di data e ora da visualizzare nella rappresentazione di stringa del valore di data e ora.  
  
3.  Per ogni elemento di data e ora da visualizzare, chiamare il metodo `Get` dell'oggetto calendario.  Sono disponibili i metodi seguenti:  
  
    -   <xref:System.Globalization.Calendar.GetYear%2A>, per visualizzate l'anno nel calendario appropriato.  
  
    -   <xref:System.Globalization.Calendar.GetMonth%2A>, per visualizzate il mese nel calendario appropriato.  
  
    -   <xref:System.Globalization.Calendar.GetDayOfMonth%2A>, per visualizzate il numero del giorno del mese nel calendario appropriato.  
  
    -   <xref:System.Globalization.Calendar.GetHour%2A>, per visualizzate l'ora del giorno nel calendario appropriato.  
  
    -   <xref:System.Globalization.Calendar.GetMinute%2A>, per visualizzate i minuti dell'ora nel calendario appropriato.  
  
    -   <xref:System.Globalization.Calendar.GetSecond%2A>, per visualizzate i secondi del minuto nel calendario appropriato.  
  
    -   <xref:System.Globalization.Calendar.GetMilliseconds%2A>, per visualizzate i millisecondi del secondo nel calendario appropriato.  
  
## Esempio  
 Nell'esempio viene visualizzata una data utilizzando due calendari diversi.  La data viene visualizzata dopo aver definito il calendario Hijri come calendario predefinito per le impostazioni cultura ar\-JO e utilizzando il calendario persiano che non è supportato come calendario facoltativo nelle impostazioni cultura fa\-IR.  
  
 [!code-csharp[Formatting.HowTo.Calendar#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#2)]
 [!code-vb[Formatting.HowTo.Calendar#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#2)]  
  
 Ogni oggetto <xref:System.Globalization.CultureInfo> può supportare uno o più calendari, indicati dalla proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A>.  Uno di questi è designato come calendario predefinito delle impostazioni cultura e viene restituito dalla proprietà di sola lettura <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName>.  È possibile designare come impostazione predefinita un altro calendario facoltativo assegnando un oggetto <xref:System.Globalization.Calendar> che rappresenta tale calendario alla proprietà <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=fullName> restituita dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName>.  Alcuni calendari, ad esempio quello persiano rappresentato dalla classe <xref:System.Globalization.PersianCalendar>, non fungono tuttavia da calendari facoltativi per tutte le impostazioni cultura.  
  
 Nell'esempio viene definita una classe dell'utilità di calendario riutilizzabile `CalendarUtility` per gestire molti dei dettagli relativi alla generazione della rappresentazione di stringa di una data mediante un determinato calendario.  La classe `CalendarUtility` dispone dei membri seguenti:  
  
-   Un costruttore con parametri il cui solo parametro è un oggetto <xref:System.Globalization.Calendar> nel quale deve essere rappresentata una data.  Viene assegnato a un campo privato della classe.  
  
-   `CalendarExists`, un metodo privato che restituisce un valore Boolean che indica se il calendario rappresentato dall'oggetto `CalendarUtility` è supportato dall'oggetto <xref:System.Globalization.CultureInfo> passato al metodo come parametro.  Il metodo esegue il wrapping di una chiamata al metodo <xref:System.Array.Exists%2A?displayProperty=fullName> al quale passa la matrice <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName>.  
  
-   `HasSameName`, un metodo privato assegnato al delegato <xref:System.Predicate%601> che viene passato come parametro al metodo <xref:System.Array.Exists%2A?displayProperty=fullName>.  Ogni membro della matrice viene passato al metodo finché quest'ultimo non restituisce `true`.  Il metodo determina se il nome di un calendario facoltativo è identico a quello del calendario rappresentato dall'oggetto `CalendarUtility`.  
  
-   `DisplayDate`, un metodo pubblico di overload al quale vengono passati due parametri, ovvero un valore <xref:System.DateTime> o <xref:System.DateTimeOffset> da esprimere nel calendario rappresentato dall'oggetto `CalendarUtility` e le impostazioni cultura le cui regole di formattazione devono essere utilizzate.  Il comportamento di restituzione di la rappresentazione di stringa di una data varia a seconda che il calendario di destinazione sia supportato dalle impostazioni cultura le cui regole di formattazione devono essere utilizzate.  
  
 Indipendentemente dal calendario utilizzato per creare un valore <xref:System.DateTime> o <xref:System.DateTimeOffset> in questo esempio, il valore viene in genere espresso in formato gregoriano  in quanto i tipi <xref:System.DateTime> e <xref:System.DateTimeOffset> non mantengono le informazioni del calendario.  Internamente vengono rappresentati come numero di cicli trascorsi dopo la mezzanotte del 1 gennaio 0001. L'interpretazione dipende dal calendario.  L'interpretazione di tale numero dipende dal calendario .  Per la maggior parte delle impostazioni cultura, il calendario predefinito è il calendario gregoriano.  
  
## Compilazione del codice  
 Per questo esempio di codice è richiesto un riferimento a System.Core.dll.  
  
 Compilare il codice alla riga di comando utilizzando csc.exe o vb.exe.  Per compilare il codice in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], inserirlo in un modello di progetto di applicazione console.  
  
## Vedere anche  
 [Esecuzione di operazioni di formattazione](../../../docs/standard/base-types/performing-formatting-operations.md)