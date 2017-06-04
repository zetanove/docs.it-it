---
title: "Procedura: salvare fusi orari in una risorsa incorporata | Microsoft Docs"
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
  - "fusi orari (oggetti) [.NET Framework], salvataggio"
  - "fusi orari (oggetti) [.NET Framework], serializzazione"
  - "fusi orari [.NET Framework], salvataggio"
ms.assetid: 3c96d83a-a057-4496-abb0-8f4b12712558
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: salvare fusi orari in una risorsa incorporata
Un'applicazione che dipende dal fuso orario richiede spesso la presenza di un determinato fuso orario.  Tuttavia, poiché la disponibilità dei singoli oggetti <xref:System.TimeZoneInfo> dipende dalle informazioni archiviate nel Registro di sistema locale, è possibile che anche i fusi orari generalmente disponibili non siano presenti.  Inoltre, le informazioni sui fusi orari personalizzati di cui viene creata un'istanza mediante il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> non vengono archiviate nel Registro di sistema insieme alle altre informazioni sul fuso orario.  Per assicurare che questi fusi orari siano disponibili quando necessario, è possibile salvarli serializzandoli e successivamente ripristinarli deserializzandoli.  
  
 In genere, la serializzazione di un oggetto <xref:System.TimeZoneInfo> si verifica indipendentemente dall'applicazione che dipende dal fuso orario.  A seconda dell'archivio dati utilizzato per l'archiviazione degli oggetti <xref:System.TimeZoneInfo> serializzati, i dati del fuso orario possono essere serializzati come parte di una routine di configurazione o di installazione, ad esempio quando i dati vengono archiviati in una chiave applicazione del Registro di sistema, o come parte di una routine di utilità che viene eseguita prima della compilazione dell'applicazione finale, ad esempio quando i dati serializzati vengono archiviati in un file di risorse XML .NET \(RESX\).  
  
 Oltre al file di risorse compilato con l'applicazione, è possibile utilizzare molti altri archivi dati per le informazioni sul fuso orario,  tra cui:  
  
-   Registro di sistema.  Notare che un'applicazione deve utilizzare le sottochiavi della relativa chiave applicazione per archiviare i dati del fuso orario personalizzato anziché utilizzare le sottochiavi di HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Time Zones.  
  
-   File di configurazione  
  
-   Altri file di sistema  
  
### Per salvare un fuso orario serializzandolo in un file RESX  
  
1.  Recuperare un fuso orario esistente o creare un nuovo fuso orario.  
  
     Per recuperare un fuso orario esistente, vedere [Procedura: accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](../../../docs/standard/datetime/access-utc-and-local.md) e [Procedura: creare un'istanza di un oggetto TimeZoneInfo](../../../docs/standard/datetime/instantiate-time-zone-info.md).  
  
     Per creare un nuovo fuso orario, chiamare uno degli overload del metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>.  Per ulteriori informazioni, vedere [Procedura: creare fusi orari senza regole di regolazione](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) e [Procedura: creare fusi orari con regole di regolazione](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md).  
  
2.  Chiamare il metodo <xref:System.TimeZoneInfo.ToSerializedString%2A> per creare una stringa contenente i dati del fuso orario.  
  
3.  Creare un'istanza di un oggetto <xref:System.IO.StreamWriter> fornendo il nome e facoltativamente il percorso del file RESX al costruttore della classe <xref:System.IO.StreamWriter>.  
  
4.  Creare un'istanza di un oggetto <xref:System.Resources.ResXResourceWriter> passando l'oggetto <xref:System.IO.StreamWriter> al costruttore della classe <xref:System.Resources.ResXResourceWriter>.  
  
5.  Passare la stringa serializzata del fuso orario al metodo <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=fullName>.  
  
6.  Chiamare il metodo <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=fullName>.  
  
7.  Chiamare il metodo <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=fullName>.  
  
8.  Chiudere l'oggetto <xref:System.IO.StreamWriter> chiamando il metodo <xref:System.IO.StreamWriter.Close%2A>.  
  
9. Aggiungere il file RESX generato al progetto di Visual Studio dell'applicazione.  
  
10. Dalla finestra **Proprietà** di Visual Studio verificare che la proprietà **Operazione di compilazione** del file RESX sia impostata su **Risorsa incorporata**.  
  
## Esempio  
 Nell'esempio seguente viene serializzato un oggetto <xref:System.TimeZoneInfo> che rappresenta l'Ora solare fuso centrale e un oggetto <xref:System.TimeZoneInfo> che rappresenta l'ora della stazione Palmer Station \(Antartide\) in un file di risorse XML .NET denominato SerializedTimeZones.resx.  L'Ora solare fuso centrale viene generalmente definita nel Registro di sistema, mentre l'ora della stazione Palmer Station \(Antartide\) rappresenta un fuso orario personalizzato.  
  
 [!code-csharp[TimeZone2.Serialization#1](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#1)]
 [!code-vb[TimeZone2.Serialization#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#1)]  
  
 In questo esempio vengono serializzati gli oggetti <xref:System.TimeZoneInfo> in modo da essere disponibili in un file di risorse in fase di compilazione.  
  
 Poiché il metodo <xref:System.Resources.ResXResourceWriter.Generate%2A?displayProperty=fullName> aggiunge informazioni sull'intestazione complete in un file di risorse XML .NET, non può essere utilizzato per aggiungere risorse in un file esistente.  Nell'esempio tale condizione viene gestita verificando la presenza del file SerializedTimeZones.resx e, se esiste, archiviando tutte le relative risorse eccetto i due fusi orari serializzati in un oggetto <xref:System.Collections.Generic.Dictionary%602> generico.  Il file esistente viene quindi eliminato e le risorse esistenti vengono aggiunte in un nuovo file SerializedTimeZones.resx.  In questo file vengono inoltre aggiunti i dati dei fusi orari serializzati.  
  
 I campi chiave \(o **Nome**\) delle risorse non devono contenere spazi incorporati.  Il metodo <xref:System.String.Replace%28System.String%2CSystem.String%29> viene chiamato per rimuovere tutti gli spazi incorporati negli identificatori del fuso orario prima che vengano assegnati al file di risorse.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Windows.Forms.dll e System.Core.dll al progetto.  
  
-   Importare gli spazi dei nomi seguenti:  
  
     [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
     [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md)   
 [Procedura: ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)