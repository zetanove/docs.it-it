---
title: "Funzioni canoniche | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: bbcc9928-36ea-4dff-9e31-96549ffed958
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Funzioni canoniche
Contenuto della sezione vengono illustrate le funzioni canoniche supportate da tutti i provider di dati e che possono essere usate da tutte le tecnologie di query.  Le funzioni canoniche non possono essere estese da un provider.  
  
 Queste funzioni canoniche vengono convertite nella funzionalità dell'origine dati corrispondente per il provider.  In questo modo è possibile esprimere le chiamate alle funzioni con un formato comune per tutte le origini dati.  
  
 Poiché queste funzioni canoniche sono indipendenti dalle origini dati, i relativi tipi di argomento e tipi restituiti sono definiti in termini di tipi nel modello concettuale.  Alcune origini dati potrebbero tuttavia non supportare tutti i tipi nel modello concettuale.  
  
 Quando si usano funzioni canoniche in una query [!INCLUDE[esql](../../../../../../includes/esql-md.md)], la funzione appropriata viene chiamata nell'origine dati.  
  
 Per tutte le funzioni canoniche sono specificati in modo esplicito sia il comportamento in caso di input null che le condizioni di errore.  I provider dell'archivio devono essere conformi a tale comportamento, ma questo comportamento non viene applicato da [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)].  
  
 Per gli scenari LINQ, le query su [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] comportano il mapping dei metodi CLR ai metodi nell'origine dati sottostante.  I metodi CLR sono mappati alle funzioni canoniche, pertanto un set di metodi specifico può essere mappato correttamente indipendentemente dall'origine dati.  
  
## Spazio dei nomi delle funzioni canoniche  
 Lo spazio dei nomi per le funzioni canoniche è <xref:System.Data.Metadata.Edm>.  Lo spazio dei nomi <xref:System.Data.Metadata.Edm> viene incluso automaticamente in tutte le query.  Se tuttavia viene importato un altro spazio dei nomi contenente una funzione con lo stesso nome di una funzione canonica \(nello spazio dei nomi <xref:System.Data.Metadata.Edm>\), è necessario specificare lo spazio dei nomi.  
  
## Contenuto della sezione  
 [Funzioni canoniche di aggregazione](../../../../../../docs/framework/data/adonet/ef/language-reference/aggregate-canonical-functions.md)  
 Vengono illustrate le funzioni canoniche [!INCLUDE[esql](../../../../../../includes/esql-md.md)] di aggregazione.  
  
 [Funzioni canoniche matematiche](../../../../../../docs/framework/data/adonet/ef/language-reference/math-canonical-functions.md)  
 Vengono illustrate le funzioni canoniche [!INCLUDE[esql](../../../../../../includes/esql-md.md)] matematiche.  
  
 [Funzioni canoniche String](../../../../../../docs/framework/data/adonet/ef/language-reference/string-canonical-functions.md)  
 Vengono illustrate le funzioni canoniche [!INCLUDE[esql](../../../../../../includes/esql-md.md)] per i valori stringa.  
  
 [Funzioni canoniche di data e ora](../../../../../../docs/framework/data/adonet/ef/language-reference/date-and-time-canonical-functions.md)  
 Vengono illustrate le funzioni canoniche [!INCLUDE[esql](../../../../../../includes/esql-md.md)] di data e ora.  
  
 [Funzioni canoniche bit per bit](../../../../../../docs/framework/data/adonet/ef/language-reference/bitwise-canonical-functions.md)  
 Vengono illustrate le funzioni canoniche [!INCLUDE[esql](../../../../../../includes/esql-md.md)] bit per bit.  
  
 [Funzioni spaziali](../../../../../../docs/framework/data/adonet/ef/language-reference/spatial-functions.md)  
 Vengono illustrate le funzioni canoniche spaziali di [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
 [Altre funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/other-canonical-functions.md)  
 Vengono illustrate le funzioni non classificate come bit per bit, di data e ora, per i valori stringa, matematiche o di aggregazione.  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Mapping delle funzioni canoniche del modello concettuale alle funzioni SQL Server](../../../../../../docs/framework/data/adonet/ef/conceptual-model-canonical-to-sql-server-functions-mapping.md)   
 [Funzioni definite dall'utente](../../../../../../docs/framework/data/adonet/ef/language-reference/user-defined-functions-entity-sql.md)