---
title: "Trace Switches | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "tracing [.NET Framework], trace switches"
  - "trace switches, about trace switches"
  - "tracing [.NET Framework], level of detail"
  - "switches, trace"
  - "trace switches"
  - "trace switches, creating custom"
ms.assetid: 8ab913aa-f400-4406-9436-f45bc6e54fbe
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# Trace Switches
Le opzioni di traccia consentono di abilitare, disabilitare e filtrare l'output di traccia.  Si tratta di oggetti presenti nel codice che possono essere configurati esternamente tramite il file CONFIG. Esistono tre tipi di opzioni di traccia in .NET Framework, ossia le classi <xref:System.Diagnostics.BooleanSwitch>, <xref:System.Diagnostics.TraceSwitch> e <xref:System.Diagnostics.SourceSwitch>. La classe <xref:System.Diagnostics.BooleanSwitch> funge da opzione di attivazione o disabilitazione per diverse istruzioni di traccia.  Le classi <xref:System.Diagnostics.TraceSwitch> e <xref:System.Diagnostics.SourceSwitch> consentono di attivare un'opzione per un particolare livello di tracciatura, in modo che vengano visualizzati i messaggi di traccia <xref:System.Diagnostics.Trace> o <xref:System.Diagnostics.TraceSource> specificati per quel livello e per tutti i livelli inferiori.  Se si disabilita l'opzione, i messaggi di traccia non verranno visualizzati. Tutte queste classi derivano dalla classe **Switch** \(**MustInherit**\) astratta, come avviene per ogni opzione sviluppata dall'utente.  
  
 Le opzioni di traccia possono essere utili per filtrare informazioni.  Può essere ad esempio necessario visualizzare ogni messaggio di traccia in un modulo di accesso ai dati, ma solo i messaggi di errore nel resto dell'applicazione.  In questo caso, si usa un'opzione di traccia per il modulo di accesso ai dati e un'opzione per il resto dell'applicazione.  Usando il file CONFIG per configurare le opzioni sulle impostazioni appropriate, è possibile controllare il tipo di messaggi di traccia ricevuti. Per altre informazioni, vedere [How to: Create, Initialize and Configure Trace Switches](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md).  
  
 In genere un'applicazione distribuita viene eseguita con le opzioni disabilitate, in modo che non vengano visualizzati messaggi di traccia superflui o non sia necessario compilare file di log durante l'esecuzione dell'applicazione. Se si verifica un problema durante l'esecuzione dell'applicazione, è possibile arrestare l'applicazione, attivare le opzioni e riavviare l'applicazione. I messaggi di tracciatura verranno quindi visualizzati.  
  
 Per usare un'opzione è prima di tutto necessario creare un oggetto opzione da una classe **BooleanSwitch**, da una classe **TraceSwitch** o da una classe di opzione definita dallo sviluppatore. Per altre informazioni sulla creazione di opzioni definite dallo sviluppatore, vedere la classe <xref:System.Diagnostics.Switch> negli argomenti di riferimento su .NET Framework. Si imposta poi un valore di configurazione che specifica quando occorre usare l'oggetto opzione. Si procede quindi alla verifica dell'impostazione dell'oggetto opzione in diversi metodi di traccia **Trace** o **Debug**.  
  
## Livelli di traccia  
 L'uso di **TraceSwitch** comporta considerazioni aggiuntive. Un oggetto **TraceSwitch** ha quattro proprietà che restituiscono valori **Boolean** che indicano se l'opzione è impostata su almeno un livello particolare:  
  
-   <xref:System.Diagnostics.TraceSwitch.TraceError%2A?displayProperty=fullName>  
  
-   <xref:System.Diagnostics.TraceSwitch.TraceWarning%2A?displayProperty=fullName>  
  
-   <xref:System.Diagnostics.TraceSwitch.TraceInfo%2A?displayProperty=fullName>  
  
-   <xref:System.Diagnostics.TraceSwitch.TraceVerbose%2A?displayProperty=fullName>  
  
 I livelli permettono di limitare la quantità di informazioni di traccia ricevute unicamente alle informazioni necessarie per risolvere un problema. Si specifica il livello di dettaglio desiderato nell'output di traccia impostando e configurando le opzioni di traccia al livello di traccia appropriato. È possibile ricevere messaggi di errore, messaggi di avviso, messaggi informativi, messaggi di traccia dettagliati o nessun messaggio.  
  
 È possibile decidere quale tipo di messaggi associare a ogni livello. In genere il contenuto dei messaggi di traccia dipende da ciò che viene associato a ogni livello, ma è possibile stabilire le differenze tra i livelli. È possibile ad esempio fornire descrizioni dettagliate di un problema a livello 3 \(**Info**\), ma fornire solo un numero di riferimento per l'errore a livello 1 \(**Error**\).  È possibile stabilire lo schema più adatto per ogni applicazione.  
  
 Queste proprietà corrispondono ai valori da 1 a 4 dell'enumerazione **TraceLevel**. La tabella seguente elenca i livelli dell'enumerazione **TraceLevel** e i rispettivi valori.  
  
|Valore enumerato|Valore Integer|Tipo di messaggio visualizzato o scritto in una destinazione di output specificata|  
|----------------------|--------------------|----------------------------------------------------------------------------------------|  
|Disattivato|0|nessuno|  
|Errore|1|Solo messaggi di errore.|  
|Avviso|2|Messaggi di avviso e messaggi di errore.|  
|Informazioni|3|Messaggi informativi, messaggi di avviso e messaggi di errore.|  
|Dettagliato|4|Messaggi dettagliati, messaggi informativi, messaggi di avviso e messaggi di errore.|  
  
 Le proprietà **TraceSwitch** indicano il livello di traccia massimo per l'opzione, ovvero l'informazione di traccia viene scritta per il livello specificato e per tutti i livelli inferiori. Se, ad esempio **TraceInfo** è **true**, anche **TraceError** e **TraceWarning** saranno **true** ma **TraceVerbose** potrebbe essere **false**.  
  
 Queste proprietà sono di sola lettura. L'oggetto **TraceSwitch** le imposta automaticamente quando viene impostata la proprietà **TraceLevel**. Ad esempio:  
  
```vb  
Dim myTraceSwitch As New TraceSwitch("SwitchOne", "The first switch") myTraceSwitch.Level = TraceLevel.Info ' This message box displays true, because setting the level to ' TraceLevel.Info sets all lower levels to true as well. MessageBox.Show(myTraceSwitch.TraceWarning.ToString()) ' This messagebox displays false. MessageBox.Show(myTraceSwitch.TraceVerbose.ToString())  
  
```  
  
```csharp  
System.Diagnostics.TraceSwitch myTraceSwitch = new System.Diagnostics.TraceSwitch("SwitchOne", "The first switch"); myTraceSwitch.Level = System.Diagnostics.TraceLevel.Info; // This message box displays true, because setting the level to // TraceLevel.Info sets all lower levels to true as well. MessageBox.Show(myTraceSwitch.TraceWarning.ToString()); // This message box displays false. MessageBox.Show(myTraceSwitch.TraceVerbose.ToString());  
  
```  
  
## Opzioni definite dallo sviluppatore  
 Oltre a fornire **BooleanSwitch** e **TraceSwitch**, è possibile definire opzioni personalizzate ereditando dalla classe **Switch** ed eseguendo l'override dei metodi della classe base con i metodi personalizzati. Per altre informazioni sulla creazione di opzioni definite dallo sviluppatore, vedere la classe <xref:System.Diagnostics.Switch> negli argomenti di riferimento su .NET Framework.  
  
## Vedere anche  
 [Trace Listeners](../../../docs/framework/debug-trace-profile/trace-listeners.md)   
 [How to: Add Trace Statements to Application Code](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)   
 [Tracing and Instrumenting Applications](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)