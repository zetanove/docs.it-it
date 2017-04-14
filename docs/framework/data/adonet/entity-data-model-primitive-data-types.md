---
title: "Entity Data Model: tipi di dati primitivi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7635168e-0566-4fdd-8391-7941b0d9f787
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Entity Data Model: tipi di dati primitivi
Entity Data Model \(EDM\) supporta un set di tipi di dati primitivi astratti \(ad esempio, String, Boolean, Int32 e così via\) usati per definire le [proprietà](../../../../docs/framework/data/adonet/property.md) in un modello concettuale.  Questi tipi di dati primitivi sono proxy per i tipi di dati primitivi effettivi supportati nell'ambiente di archiviazione o host, ad esempio un database SQL Server o Common Language Runtime \(CLR\).  EDM non definisce la semantica di operazioni o conversioni su tipi di dati primitivi. Questa semantica viene definita dall'ambiente di archiviazione o host.  I tipi di dati primitivi in EDM sono in genere associati ai corrispondenti tipi di dati primitivi nell'ambiente di archiviazione o host.  Per informazioni su come Entity Framework esegue il mapping di tipi primitivi in EDM ai tipi di dati di SQL Server, vedere [SqlClient per i tipi Entity Framework](../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-types.md).  
  
> [!NOTE]
>  EDM non supporta raccolte di tipi di dati primitivi.  
  
 Per informazioni sui tipi di dati strutturati in EDM, vedere [tipo di entità](../../../../docs/framework/data/adonet/entity-type.md) e [tipo complesso](../../../../docs/framework/data/adonet/complex-type.md).  
  
## Tipi di dati primitivi supportati in Entity Data Model  
 Nella tabella seguente vengono elencati i tipi di dati primitivi supportati da EDM.  Nella tabella vengono inoltre elencati i [facet](../../../../docs/framework/data/adonet/facet.md) applicabili a ogni tipo di dati primitivi.  
  
|Tipi di dati primitivi|Descrizione|Facet applicabili|  
|----------------------------|-----------------|-----------------------|  
|Binario|Contiene dati binari.|MaxLength, FixedLength, Nullable, Default|  
|Boolean|Contiene il valore `true` o `false`.|Nullable, Default|  
|Byte|Contiene un Unsigned Integer a 8 bit.|Precision, Nullable, Default|  
|DateTime|Rappresenta una data e un'ora.|Precision, Nullable, Default|  
|DateTimeOffset|Contiene una data e un'ora come offset in minuti rispetto all'ora GMT.|Precision, Nullable, Default|  
|Decimal|Contiene un valore numerico con scala e precisione fisse.|Precision, Nullable, Default|  
|Double|Contiene un numero a virgola mobile con precisione a 15 cifre.|Precision, Nullable, Default|  
|Float|Contiene un numero a virgola mobile con precisione a sette cifre.|Precision, Nullable, Default|  
|Guid|Contiene un identificatore univoco a 16 byte.|Precision, Nullable, Default|  
|Int16|Contiene un Signed Integer a 16 bit.|Precision, Nullable, Default|  
|Int32|Contiene un Signed Integer a 32 bit.|Precision, Nullable, Default|  
|Int64|Contiene un Signed Integer a 64 bit.|Precision, Nullable, Default|  
|SByte|Contiene un Signed Integer a 8 bit.|Precision, Nullable, Default|  
|String|Contiene dati di tipo carattere.|Unicode, FixedLength, MaxLength, Collation, Precision, Nullable, Default|  
|utente|Contiene un'ora del giorno.|Precision, Nullable, Default|  
  
## Vedere anche  
 [Concetti chiave di Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)