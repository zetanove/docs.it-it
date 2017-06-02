---
title: "Procedura: ripristinare i fusi orari da una risorsa incorporata | Microsoft Docs"
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
  - "fusi orari [.NET Framework], deserializzazione"
  - "fusi orari [.NET Framework], ripristino"
ms.assetid: 6b7b4de9-da07-47e3-8f4c-823f81798ee7
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: ripristinare i fusi orari da una risorsa incorporata
In questo argomento viene descritto come ripristinare i fusi orari salvati in un file di risorse.  Per informazioni e istruzioni sul salvataggio dei fusi orari, vedere [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md).  
  
### Per deserializzare un oggetto TimeZoneInfo da una risorsa incorporata  
  
1.  Se il fuso orario da recuperare non è un fuso orario personalizzato, provare a crearne un'istanza utilizzando il metodo <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A>.  
  
2.  Creare un'istanza di un oggetto <xref:System.Resources.ResourceManager> passando il nome completo del file di risorse incorporate e un riferimento all'assembly che contiene il file di risorse.  
  
     Se non è possibile determinare il nome completo del file di risorse incorporate, utilizzare [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per esaminare il manifesto dell'assembly.  Una voce `.mresource` identifica la risorsa.  Nell'esempio il nome completo della risorsa è `SerializeTimeZoneData.SerializedTimeZones`.  
  
     Se il file di risorse è incorporato nello stesso assembly che contiene il codice per la creazione di istanze del fuso orario, è possibile recuperarne un riferimento chiamando il metodo `static` \(`Shared` in Visual Basic\) <xref:System.Reflection.Assembly.GetExecutingAssembly%2A>.  
  
3.  Se la chiamata al metodo <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> non riesce o se è necessario creare un'istanza di un fuso orario personalizzato, recuperare una stringa che contenga il fuso orario serializzato chiamando il metodo <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>.  
  
4.  Deserializzare i dati del fuso orario chiamando il metodo <xref:System.TimeZoneInfo.FromSerializedString%2A>.  
  
## Esempio  
 Nell'esempio seguente viene deserializzato un oggetto <xref:System.TimeZoneInfo> archiviato in un file di risorse .NET XML incorporate.  
  
 [!code-csharp[TimeZone2.Serialization#3](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#3)]
 [!code-vb[TimeZone2.Serialization#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#3)]  
  
 In questo codice viene illustrata la gestione delle eccezioni per assicurarsi che sia presente un oggetto <xref:System.TimeZoneInfo> richiesto dall'applicazione.  Viene innanzitutto tentata la creazione di un'istanza di un oggetto <xref:System.TimeZoneInfo> recuperandolo dal Registro di sistema mediante il metodo <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A>.  Se non è possibile creare un'stanza del fuso orario, il codice lo recupera dal file di risorse incorporate.  
  
 Poiché i dati per i fusi orari personalizzati \(fusi orari di cui è stata creata un'istanza utilizzando il metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> \) non vengono archiviati nel Registro di sistema, il codice non chiama il metodo <xref:System.TimeZoneInfo.FindSystemTimeZoneById%2A> per creare un'istanza del fuso orario per la stazione Palmer Station, Antartide.  Cerca invece immediatamente il file di risorse incorporate per recuperare una stringa che contenga i dati del fuso orario prima che venga chiamato il metodo <xref:System.TimeZoneInfo.FromSerializedString%2A>.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Aggiungere un riferimento a System.Windows.Forms.dll e System.Core.dll al progetto.  
  
-   Importare gli spazi dei nomi seguenti:  
  
     [!code-csharp[TimeZone2.Serialization#2](../../../samples/snippets/csharp/VS_Snippets_CLR/TimeZone2.Serialization/cs/SerializeTimeZoneData.cs#2)]
     [!code-vb[TimeZone2.Serialization#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/TimeZone2.Serialization/vb/SerializeTimeZoneData.vb#2)]  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md)   
 [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)