---
title: "Modifiche apportate allo spazio dei nomi System.Uri nella versione 2.0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 35883fe9-2d09-4d8b-80ca-cf23a941e459
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Modifiche apportate allo spazio dei nomi System.Uri nella versione 2.0
Diverse modifiche apportate alla classe <xref:System.Uri?displayProperty=fullName>.  Queste modifiche hanno corretto il comportamento non corretto, usabilità avanzato e con sicurezza avanzata.  
  
## Membri obsoleti e deprecato  
 Costruttori:  
  
-   Tutti i costruttori che accettano un parametro `dontEscape`.  
  
 Metodi:  
  
-   <xref:System.Uri.CheckSecurity%2A>  
  
-   <xref:System.Uri.Escape%2A>  
  
-   <xref:System.Uri.Canonicalize%2A>  
  
-   <xref:System.Uri.Parse%2A>  
  
-   <xref:System.Uri.IsReservedCharacter%2A>  
  
-   <xref:System.Uri.IsBadFileSystemCharacter%2A>  
  
-   <xref:System.Uri.IsExcludedCharacter%2A>  
  
-   <xref:System.Uri.EscapeString%2A>  
  
## Modifiche  
  
-   Per gli schemi URI ritenuti di non disporre di una parte di query \(file, FTP e altre\), “?„ il carattere viene sempre utilizzato caratteri di escape e non è considerato l'inizio di una parte <xref:System.Uri.Query%2A>.  
  
-   Per gli URI impliciti del file \(nel formato “c:\\directory\\file @name.txt„\), il \(" \# "\) del carattere del frammento viene utilizzato caratteri di escape sempre a meno che non utilizzare caratteri di escapee completo sia necessario o <xref:System.Uri.LocalPath%2A> è `true`.  
  
-   Il supporto di hostname UNC è stato rimosso, la specifica IDN per la rappresentazione di hostname internazionali è stata adottata.  
  
-   <xref:System.Uri.LocalPath%2A> restituisce sempre una stringa completa senza codice di escape.  
  
-   <xref:System.Uri.ToString%2A> non utilizzare caratteri di escape un “%„ utilizzato caratteri di escape, “? „, o “\#„.  
  
-   <xref:System.Uri.Equals%2A> ora include parte <xref:System.Uri.Query%2A> nel controllo di uguaglianza.  
  
-   “\=\=„ Operatori e “\! \=„ vengono sostituiti e collegati a <xref:System.Uri.Equals%2A> il metodo.  
  
-   <xref:System.Uri.IsLoopback%2A> ora disponibili i risultati coerenti.  
  
-   L'uri “`file:///path`„ non è più convertito in “file:\/\/path„.  
  
-   “\#„ viene riconosciuto come carattere di terminazione di nome host.  Ovvero “http:\/\/consoto.com\#fragment„ viene convertito a “http:\/\/contoso.com\/\#fragment„.  
  
-   Un bug quando si combinano un URI base con un frammento è stato corretto.  
  
-   Un bug in <xref:System.Uri.HostNameType%2A> è corretto.  
  
-   Un bug nell'analisi di NNTP è corretto.  
  
-   Un URI del form HTTP: contoso.com ora genera un'eccezione di analisi.  
  
-   Framework gestisce correttamente il userinfo in un URI.  
  
-   La compressione di percorso dell'URI è fissa in modo da non consentire a un URI interrotto il file system sulla radice.  
  
## Vedere anche  
 <xref:System.Uri?displayProperty=fullName>