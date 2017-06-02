---
title: "Ricerca dei fusi orari definiti in un sistema locale | Microsoft Docs"
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
  - "fuso orario locale (accesso)"
  - "identificatori dei fusi orari [.NET Framework]"
  - "fusi orari [.NET Framework], ricerca di fusi orari del sistema locale"
  - "fusi orari [.NET Framework], locali"
  - "fusi orari [.NET Framework], recupero"
  - "fusi orari [.NET Framework], UTC"
  - "UTC (ora), ricerca di fusi orari del sistema locale"
ms.assetid: 3f63b1bc-9a4b-4bde-84ea-ab028a80d3e1
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Ricerca dei fusi orari definiti in un sistema locale
La classe <xref:System.TimeZoneInfo> non espone un costruttore pubblico.  Di conseguenza, non è possibile usare la parola chiave `new` per creare un nuovo oggetto <xref:System.TimeZoneInfo>.  Le istanze degli oggetti <xref:System.TimeZoneInfo> vengono invece create recuperando le informazioni sui fusi orari predefiniti dal Registro di sistema oppure creando un fuso orario personalizzato.  Questo argomento descrive la creazione dell'istanza di un fuso orario da dati archiviati nel Registro di sistema.  Inoltre, le proprietà `static` \(`shared` in Visual Basic\) della classe <xref:System.TimeZoneInfo> forniscono accesso all'ora Coordinated Universal Time \(UTC\) e al fuso orario locale.  
  
> [!NOTE]
>  Per i fusi orari non definiti nel Registro di sistema, è possibile creare fusi orari personalizzati chiamando gli overload del metodo <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A>.  La creazione di un fuso orario personalizzato viene descritta negli argomenti [Procedura: creare fusi orari senza regole di regolazione](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md) e [Procedura: creare fusi orari con regole di regolazione](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md).  Inoltre, è possibile creare l'istanza di un oggetto <xref:System.TimeZoneInfo> ripristinando l'oggetto da una stringa serializzata con il metodo <xref:System.TimeZoneInfo.FromSerializedString%2A>.  La serializzazione e la deserializzazione di un oggetto <xref:System.TimeZoneInfo> vengono descritte negli argomenti [Procedura: salvare fusi orari in una risorsa incorporata](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md) e [Procedura: ripristinare i fusi orari da una risorsa incorporata](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md).  
  
## Accesso a singoli fusi orari  
 La classe <xref:System.TimeZoneInfo> fornisce due oggetti fuso orario predefiniti che rappresentano l'ora UTC e il fuso orario locale.  Questi oggetti sono disponibili rispettivamente nelle proprietà <xref:System.TimeZoneInfo.Utc%2A> e <xref:System.TimeZoneInfo.Local%2A>.  Per istruzioni sull'accesso all'ora UTC o ai fusi orari locali, vedere [Procedura: accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](../../../docs/standard/datetime/access-utc-and-local.md).  
  
 È anche possibile creare l'istanza di un oggetto <xref:System.TimeZoneInfo> che rappresenta qualsiasi fuso orario definito nel Registro di sistema.  Per istruzioni sulla creazione dell'istanza di un oggetto fuso orario specifico, vedere [Procedura: creare un'istanza di un oggetto TimeZoneInfo](../../../docs/standard/datetime/instantiate-time-zone-info.md).  
  
## Identificatori del fuso orario  
 L'identificatore del fuso orario è un campo chiave che identifica in modo univoco il fuso orario.  Benché la maggior parte delle chiavi sia relativamente breve, in confronto l'identificatore del fuso orario è piuttosto lungo.  Nella maggior parte dei casi, il suo valore corrisponde alla proprietà <xref:System.TimeZoneInfo.StandardName%2A?displayProperty=fullName>, che viene usata per fornire il nome dell'ora solare del fuso orario.  Esistono tuttavia alcune eccezioni.  Il modo migliore per assicurarsi di specificare un identificatore univoco consiste nell'enumerare i fusi orari disponibili nel sistema e annotare gli identificatori associati.  
  
## Vedere anche  
 [Date, ora e fusi orari](../../../docs/standard/datetime/index.md)   
 [Procedura: accedere agli oggetti predefiniti dell'ora UTC e del fuso orario locale](../../../docs/standard/datetime/access-utc-and-local.md)   
 [Procedura: creare un'istanza di un oggetto TimeZoneInfo](../../../docs/standard/datetime/instantiate-time-zone-info.md)   
 [Conversione degli orari tra fusi orari](../../../docs/standard/datetime/converting-between-time-zones.md)