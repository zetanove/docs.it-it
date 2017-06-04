---
title: "Panoramica sul fuso orario | Microsoft Docs"
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
  - "regolazione (regola) [.NET Framework]"
  - "ora ambigua [.NET Framework]"
  - "ora legale [.NET Framework]"
  - "regola fissa [.NET Framework]"
  - "regola mobile [.NET Framework]"
  - "ora non valida [.NET Framework]"
  - "fusi orari [.NET Framework], informazioni sui fusi orari"
  - "fusi orari [.NET Framework], creazione"
  - "fusi orari [.NET Framework], terminologia"
  - "classe TimeZoneInfo, informazioni sulla classe TimeZoneInfo"
  - "transizione (tempo) [.NET Framework]"
ms.assetid: c4b7ed01-5e38-4959-a3b6-ef9765d6ccf1
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Panoramica sul fuso orario
La classe <xref:System.TimeZoneInfo> semplifica la creazione di applicazioni che dipendono dal fuso orario.  La classe <xref:System.TimeZone> supporta l'utilizzo del fuso orario locale e dell'ora UTC \(Coordinated Universal Time\).  La classe <xref:System.TimeZoneInfo> supporta entrambi questi fusi orari nonché tutti i fusi orari per i quali esistono informazioni predefinite nel Registro di sistema.  La classe <xref:System.TimeZoneInfo> può anche essere utilizzata per definire fusi orari personalizzati di cui non sono disponibili informazioni nel sistema.  
  
## Concetti di base sul fuso orario  
 Un fuso orario è un'area geografica in cui viene utilizzata la stessa ora.  In genere, ma non sempre, i fusi orari adiacenti riportano un'ora di differenza.  Tutti i fusi orari del mondo sono definiti in base alla differenza con l'ora UTC \(Coordinated Universal Time\).  
  
 Molti fusi orari del mondo supportano l'ora legale.  L'ora legale ha lo scopo di sfruttare al meglio la luce del giorno portando l'orario avanti di un'ora in primavera o all'inizio dell'estate e ritornando all'orario standard ufficiale alla fine dell'estate o in autunno.  Questi passaggi da ora solare a ora legale e viceversa sono noti come regole di regolazione.  
  
 La transizione da ora solare a ora legale e viceversa in un determinato fuso orario può essere definita da una regola di regolazione fissa o mobile.  Una regola di regolazione fissa imposta la transizione da ora solare a ora legale e viceversa su una determinata data dell'anno.  Ad esempio, una transizione da ora legale a ora solare che si verifica il 25 ottobre di ogni anno segue una regola di regolazione fissa.  Le regole di regolazione mobili in base alle quali la transizione da ora legale a ora solare e viceversa avviene in un determinato giorno di una determinata settimana di un determinato mese sono molto più comuni.  Ad esempio, una transizione da ora solare a ora legale che si verifica la terza domenica di marzo segue una regola di regolazione mobile.  
  
 Per i fusi orari che supportano regole di regolazione, la transizione da ora legale a ora solare e viceversa crea due tipi di orari anomali: orari non validi e orari ambigui.  Un'ora non valida è un'ora inesistente creata dalla transizione da ora solare a ora legale.  Ad esempio, se la transizione si verifica un determinato giorno alle 2:00 AM e provoca il passaggio alle 3:00 AM, ogni volta l'intervallo tra le 2:00 AM e le 2:59:99 AM non è valido.  Un'ora ambigua è un'ora che può essere associata a due ore diverse di un singolo fuso orario.  Viene creata dalla transizione da ora legale a ora solare.  Ad esempio, se la transizione si verifica un determinato giorno alle 2:00 AM e provoca il passaggio dall'1:00 AM, ogni intervallo tra le 1:00 AM e l'1:59:99 AM può essere interpretato sia come ora solare che ora legale.  
  
## Terminologia relativa al fuso orario  
 Nella tabella riportata di seguito vengono definiti i termini utilizzati generalmente con i fusi orari e le applicazioni che dipendono dal fuso orario.  
  
|Termine|Definizione|  
|-------------|-----------------|  
|Regola di regolazione|Una regola che definisce quando si verifica la transizione da ora solare a ora legale e viceversa.  Ogni regola di regolazione ha una data di inizio e una data di fine che definiscono il periodo di applicazione della regola \(ad esempio la regola di regolazione è in vigore dall'1 gennaio 1986 al 31 dicembre 2006\), un delta \(la quantità di tempo da applicare all'ora solare in funzione dell'applicazione della regola di regolazione\) e le informazioni sulla data e ora specifiche in cui si verificano le transizioni durante il periodo di modifica.  Le transizioni possono seguire una regola fissa o una regola mobile.|  
|Ora ambigua|Un'ora che può essere associata a due ore diverse di un singolo fuso orario.  Si verifica quando l'orario viene portato indietro, ad esempio durante la transizione da ora legale a ora solare di un fuso orario.  Ad esempio, se la transizione si verifica un determinato giorno alle 2:00 AM e provoca il passaggio dall'1:00 AM, ogni intervallo tra le 1:00 AM e l'1:59:99 AM può essere interpretato sia come ora solare che ora legale.|  
|Regola fissa|Una regola di regolazione che imposta una determinata data per la transizione da ora solare a ora legale e viceversa.  Ad esempio, una transizione da ora legale a ora solare che si verifica il 25 ottobre di ogni anno segue una regola di regolazione fissa.|  
|Regola mobile|Una regola di regolazione che imposta un determinato giorno di una determinata settimana di un determinato mese per la transizione da ora legale a ora solare e viceversa.  Ad esempio, una transizione da ora solare a ora legale che si verifica la terza domenica di marzo segue una regola di regolazione mobile.|  
|Ora non valida|Un'ora inesistente, ovvero il risultato della transizione da ora solare a ora legale.  Si verifica quando l'orario viene portato avanti, ad esempio durante la transizione da ora solare a ora legale di un fuso orario.  Ad esempio, se la transizione si verifica un determinato giorno alle 2:00 AM e provoca il passaggio alle 3:00 AM, ogni volta l'intervallo tra le 2:00 AM e le 2:59:99 AM non è valido.|  
|Tempo di transizione|Informazioni su un cambiamento di ora specifico, ad esempio il passaggio da ora legale a ora solare o viceversa, in un determinato fuso orario.|  
  
## Fusi orari e la classe TimeZoneInfo  
 In .NET Framework un oggetto <xref:System.TimeZoneInfo> rappresenta un fuso orario.  La classe <xref:System.TimeZoneInfo> include il metodo <xref:System.TimeZoneInfo.GetAdjustmentRules%2A> che restituisce una matrice di oggetti <xref:System.TimeZoneInfo.AdjustmentRule>.  Ogni elemento di questa matrice fornisce informazioni sulla transizione da ora solare a ora legale e viceversa per un determinato periodo di tempo. Per i fusi orari che non supportano l'ora legale, il metodo restituisce una matrice vuota. Ogni oggetto <xref:System.TimeZoneInfo.AdjustmentRule> dispone di una proprietà <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionStart%2A> e <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionEnd%2A> che definiscono la data e ora specifiche per la transizione da ora solare a ora legale e viceversa.  La proprietà <xref:System.TimeZoneInfo.TransitionTime.IsFixedDateRule%2A> indica se la transizione è fissa o mobile.  
  
 .NET Framework si basa sulle informazioni del fuso orario fornite dal sistema operativo Windows e archiviate nel Registro di sistema.  A causa del numero di fusi orari della terra, non tutti i fusi orari esistenti sono rappresentati nel Registro di sistema.  Inoltre, poiché il Registro di sistema è una struttura dinamica, è possibile aggiungere o rimuovere fusi orari predefiniti.  Infine, nel Registro di sistema non sono contenuti necessariamente i dati dei fusi orari storici.  Ad esempio, nel Registro di sistema di Windows XP sono contenuti i dati relativi a un solo insieme di regolazioni di fuso orario.  Windows Vista supporta dati del fuso orario dinamici, ovvero un singolo fuso orario può avere più regole di regolazione da applicare a specifici intervalli di anni.  Tuttavia, la maggior parte dei fusi orari definiti nel Registro di sistema di Windows Vista e che supportano l'ora legale dispongono solo di una o due regole di regolazione predefinite.  
  
 La dipendenza della classe <xref:System.TimeZoneInfo> dal Registro di sistema indica che un'applicazione che dipende dal fuso orario non è in grado di determinare se un determinato fuso orario è definito nel Registro di sistema.  Di conseguenza, quando si tenta di creare un'istanza di un fuso orario specifico \(diverso dal fuso orario locale o dal fuso orario rappresentato dall'ora UTC\) è necessario utilizzare la gestione delle eccezioni.  È inoltre necessario fornire un metodo che consente all'applicazione di continuare se non è possibile creare un'istanza di un oggetto <xref:System.TimeZoneInfo> richiesto dal Registro di sistema.  
  
 Per gestire l'assenza di un fuso orario richiesto, la classe <xref:System.TimeZoneInfo> include il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> che può essere utilizzato per creare fusi orari personalizzati non presenti nel Registro di sistema.  Per informazioni dettagliate sulla creazione di un fuso orario personalizzato, vedere [Procedura: creare fusi orari senza regole di regolazione](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) e [Procedura: creare fusi orari con regole di regolazione](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md).  Inoltre, è possibile utilizzare il metodo <xref:System.TimeZoneInfo.ToSerializedString%2A> per convertire un fuso orario appena creato in una stringa e salvarlo in un archivio dati, ad esempio un database, un file di testo, il Registro di sistema o una risorsa dell'applicazione.  È quindi possibile utilizzare il metodo <xref:System.TimeZoneInfo.FromSerializedString%2A> per convertire nuovamente questa stringa in un oggetto <xref:System.TimeZoneInfo>.  Per ulteriori informazioni, vedere [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) e [Procedura: ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md).  
  
 Poiché ogni fuso orario è caratterizzato da un offset di base dall'ora UTC e da un offset dall'ora UTC che riflette tutte le regole di regolazione esistenti, un'ora di un fuso orario può essere facilmente convertita nell'ora di un altro fuso orario.  A tale scopo, l'oggetto <xref:System.TimeZoneInfo> include diversi metodi di conversione, tra cui:  
  
-   <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> che converte l'ora UTC nell'ora di un determinato fuso orario.  
  
-   <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> che converte l'ora di un determinato fuso orario nell'ora UTC.  
  
-   <xref:System.TimeZoneInfo.ConvertTime%2A> che converte l'ora di un determinato fuso orario nell'ora di un altro determinato fuso orario.  
  
-   <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A> che utilizza gli identificatori del fuso orario, anziché gli oggetti <xref:System.TimeZoneInfo>, come parametri per convertire l'ora di un determinato fuso orario nell'ora di un altro determinato fuso orario.  
  
 Per informazioni dettagliate sulla conversione degli orari tra fusi orari, vedere [Conversione degli orari tra fusi orari](../../../docs/standard/datetime/converting-between-time-zones.md).  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)