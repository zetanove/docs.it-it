---
title: "File Encodings (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "character encodings"
  - "files, encoding"
  - "Unicode, file encoding"
  - "file encoding"
ms.assetid: ea2c5f5f-bbb1-4150-9928-b9951fa6bc57
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# File Encodings (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Le codifiche dei file, note anche come codifiche del carattere, specificano come rappresentare i caratteri durante l'elaborazione del testo.  Una codifica potrebbe essere preferibile a un'altra in termini di quali caratteri del linguaggio gestire. Tuttavia, in genere, si preferisce utilizzare Unicode.  
  
 In fase di lettura o scrittura nei file, un'eventuale corrispondenza errata delle codifiche dei file potrebbe generare eccezioni o risultati errati.  
  
## Tipi di codifiche  
 Per l'utilizzo dei file si preferisce utilizzare la codifica Unicode.  Unicode è uno standard universale di codifica dei caratteri che utilizzare i valori di codice a 16 bit per rappresentare tutti i caratteri utilizzati nei sistemi informatici moderni, compresi simboli tecnici e caratteri speciali utilizzati nell'industria grafica.  
  
 I precedenti standard di codifica dei caratteri erano costituiti da set di caratteri tradizionali, ad esempio il set di caratteri Windows ANSI che utilizza valori di codice a 8 bit o combinazioni di valori a 8 bit, per rappresentare i caratteri utilizzati in un linguaggio o regione geografica specifici.  
  
## Classe Encoding  
 La classe <xref:System.Text.Encoding> rappresenta una codifica di caratteri.  Nella tabella riportata di seguito sono elencati e descritti i tipi di codifiche disponibili.  
  
|||  
|-|-|  
|Nome|Descrizione|  
|<xref:System.Text.ASCIIEncoding>|Rappresenta una codifica di caratteri ASCII dei caratteri Unicode.|  
|<xref:System.Text.UnicodeEncoding>|Rappresenta una codifica UTF\-16 dei caratteri Unicode.|  
|<xref:System.Text.UTF32Encoding>|Rappresenta una codifica UTF\-32 dei caratteri Unicode.|  
|<xref:System.Text.UTF7Encoding>|Rappresenta una codifica UTF\-7 dei caratteri Unicode.|  
|<xref:System.Text.UTF8Encoding>|Rappresenta una codifica UTF\-8 dei caratteri Unicode.|  
  
## Vedere anche  
 [Reading from Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)   
 [Writing to Files](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)