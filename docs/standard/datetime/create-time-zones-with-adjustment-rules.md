---
title: "Procedura: creare fusi orari con regole di regolazione | Microsoft Docs"
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
  - "fusi orari [.NET Framework], e regole di regolazione"
  - "fusi orari [.NET Framework], creazione"
ms.assetid: c52ef192-13a9-435f-8015-3b12eae8c47c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: creare fusi orari con regole di regolazione
Le informazioni precise del fuso orario richieste da un'applicazione possono non essere presenti in un determinato sistema per molte ragioni:  
  
-   Il fuso orario non è mai stato definito nel Registro di sistema locale.  
  
-   I dati sul fuso orario sono stati modificati o rimossi dal Registro di sistema.  
  
-   Il fuso orario non ha informazioni accurate sulle regolazioni del fuso orario per un determinato periodo storico.  
  
 In questi casi, è possibile chiamare il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> per definire il fuso orario richiesto dall'applicazione.  È possibile utilizzare gli overload di questo metodo per creare un fuso orario con o senza regole di regolazione.  Se il fuso orario supporta l'ora legale, è possibile definire le regolazioni con regole di regolazione fisse o mobili. Per le definizioni di questi termini, vedere la sezione "Terminologia relativa al fuso orario" in [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md).  
  
> [!IMPORTANT]
>  I fusi orari personalizzati creati chiamando il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> non vengono aggiunti al Registro di sistema,  ma è possibile accedervi solo tramite il riferimento all'oggetto restituito dalla chiamata al metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>.  
  
 In questo argomento viene illustrato come creare un fuso orario con regole di regolazione.  Per creare un fuso orario che non supporta le regole di regolazione dell'ora legale, vedere [Procedura: creare fusi orari senza regole di regolazione](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md).  
  
### Per creare un fuso orario con le regole di regolazione mobili  
  
1.  Per ogni regolazione, ovvero per ogni transizione da ora solare e viceversa in un determinato intervallo di tempo, effettuare le operazioni seguenti:  
  
    1.  Definire il tempo di transizione iniziale per la regolazione del fuso orario.  
  
         È necessario chiamare il metodo <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=fullName> e passare un valore <xref:System.DateTime> che definisce il tempo della transizione, un valore intero che definisce il mese della transizione, un valore intero che definisce la settimana in cui si verifica la transizione e un valore <xref:System.DayOfWeek> che definisce il giorno della settimana in cui si verifica la transizione.  Questa chiamata al metodo crea un'istanza di un oggetto <xref:System.TimeZoneInfo.TransitionTime>.  
  
    2.  Definire il tempo di transizione finale per la regolazione del fuso orario.  Richiede un'altra chiamata al metodo <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=fullName>.  Questa chiamata al metodo crea un'istanza di un secondo oggetto <xref:System.TimeZoneInfo.TransitionTime>.  
  
    3.  Chiamare il metodo <xref:System.TimeZoneInfo.AdjustmentRule.CreateAdjustmentRule%2A> e passare le date effettive di inizio e di fine della regolazione, un oggetto <xref:System.TimeSpan> che definisce il periodo della transizione e i due oggetti <xref:System.TimeZoneInfo.TransitionTime> che definiscono quando si verifica la transizione da ora solare a ora legale e viceversa.  Questa chiamata al metodo crea un'istanza di un oggetto <xref:System.TimeZoneInfo.AdjustmentRule>.  
  
    4.  Assegnare l'oggetto <xref:System.TimeZoneInfo.AdjustmentRule> a una matrice di oggetti <xref:System.TimeZoneInfo.AdjustmentRule>.  
  
2.  Definire il nome visualizzato del fuso orario.  Il nome visualizzato segue un formato quasi standard in cui l'offset del fuso orario dall'ora UTC \(Coordinated Universal Time\) viene racchiuso tra parentesi e seguito da una stringa che identifica il fuso orario, una o più città del fuso orario o uno o più paesi o regioni del fuso orario.  
  
3.  Definire il nome dell'ora solare del fuso orario.  In genere questa stringa viene utilizzata anche come identificatore del fuso orario.  
  
4.  Definire il nome dell'ora legale del fuso orario.  
  
5.  Se si desidera utilizzare un identificatore diverso dal nome standard del fuso orario, definire l'identificatore del fuso orario.  
  
6.  Creare un'istanza di un oggetto <xref:System.TimeSpan> che definisce l'offset del fuso orario dall'ora UTC.  I fusi orari con ore in avanti rispetto all'ora UTC hanno un offset positivo.  I fusi orari con ore indietro rispetto all'ora UTC hanno un offset negativo.  
  
7.  Chiamare il metodo [TimeZoneInfo.CreateCustomTimeZone\(String, TimeSpan, String, String, String, TimeZoneInfo.AdjustmentRule\<xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=fullName> per creare un'istanza del nuovo fuso orario.  
  
## Esempio  
 Nell'esempio seguente viene definito un fuso Ora solare fuso centrale per gli Stati Uniti che include le regole di regolazione per una varietà di intervalli di tempo dal 1918 a oggi.  
  
 [!code-csharp[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#5)]
 [!code-vb[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#5)]  
  
 Il fuso orario creato in questo esempio ha più regole di regolazione.  È necessario pertanto assicurarsi che le date effettive di inizio e di fine di una regola di regolazione non si sovrappongono con le date di un'altra regola.  In caso di sovrapposizione, viene generata un'eccezione <xref:System.InvalidTimeZoneException>.  
  
 Per le regole di regolazione mobili, viene passato il valore 5 al parametro `week` del metodo <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A> indicando che la transizione si verifica nell'ultima settimana di un determinato mese.  
  
 Nel creare la matrice di oggetti <xref:System.TimeZoneInfo.AdjustmentRule> da utilizzare nella chiamata al metodo [TimeZoneInfo.CreateCustomTimeZone\(String, TimeSpan, String, String, String, TimeZoneInfo.AdjustmentRule\<xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=fullName>, la matrice è stata inizializzata in base alla dimensione richiesta dal numero di regolazioni da creare per il fuso orario.  In questo esempio di codice invece viene chiamato il metodo <xref:System.Collections.Generic.List%601.Add%2A> per aggiungere ogni regola di regolazione a una raccolta <xref:System.Collections.Generic.List%601> generica di oggetti <xref:System.TimeZoneInfo.AdjustmentRule>.  Viene quindi chiamato il metodo <xref:System.Collections.Generic.List%601.CopyTo%2A> per copiare i membri di questa raccolta nella matrice.  
  
 Nell'esempio viene anche utilizzato il metodo <xref:System.TimeZoneInfo.TransitionTime.CreateFixedDateRule%2A> per definire regolazioni a data fissa.  Equivale a chiamare il metodo <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A>, con l'unica differenza che è necessario fornire solo l'ora, il mese e il giorno come parametri di transizione.  
  
 È possibile eseguire il test di questo esempio utilizzando un codice analogo al seguente:  
  
 [!code-csharp[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#7)]
 [!code-vb[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#7)]  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Core.dll al progetto.  
  
-   Importare gli spazi dei nomi seguenti:  
  
     [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
     [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md)   
 [Procedura: creare fusi orari senza regole di regolazione](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)