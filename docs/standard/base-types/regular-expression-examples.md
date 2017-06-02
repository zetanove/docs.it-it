---
title: "Esempi di espressioni regolari | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "espressioni regolari [.NET Framework], esempi"
  - "espressioni regolari [.NET Framework]"
  - "stringhe [.NET Framework], espressioni regolari"
ms.assetid: e9fd53f2-ed56-4b09-b2ea-e9bc9d65e6d6
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# Esempi di espressioni regolari
In questa sezione vengono riportati esempi di codice in cui viene illustrato l'utilizzo di espressioni regolari in applicazioni comuni.  
  
> [!NOTE]
>  Lo spazio dei nomi <xref:System.Web.RegularExpressions> contiene un determinato numero di oggetti di espressioni regolari che implementano modelli di espressioni regolari predefiniti per l'analisi delle stringhe da documenti HTML, XML e ASP.NET.  La classe <xref:System.Web.RegularExpressions.TagRegex> identifica, ad esempio, i tag iniziali di una stringa mentre la classe <xref:System.Web.RegularExpressions.CommentRegex> identifica i commenti ASP.NET di una stringa.  
  
## In questa sezione  
 [Esempio: ricerca di HREF](../../../docs/standard/base-types/regular-expression-example-scanning-for-hrefs.md)  
 Viene fornito un esempio in cui viene cercata una stringa di input e vengono visualizzati tutti i valori href\="…" e le relative posizioni nella stringa.  
  
 [Esempio: modifica dei formati di data](../../../docs/standard/base-types/regular-expression-example-changing-date-formats.md)  
 Viene fornito un esempio in cui le date in formato mm\/gg\/aa vengono sostituite con le date in formato gg\-mm\-aa.  
  
 [Procedura: Estrarre un protocollo e un numero di porta da un URL](../../../docs/standard/base-types/how-to-extract-a-protocol-and-port-number-from-a-url.md)  
 Viene fornito un esempio in cui da una stringa contenente un URL vengono estratti un protocollo e un numero di porta.  L'analisi di "http:\/\/www.contoso.com:8080\/lettere\/readme.html" restituirebbe ad esempio "http:8080".  
  
 [Procedura: Rimuovere caratteri non validi da una stringa](../../../docs/standard/base-types/how-to-strip-invalid-characters-from-a-string.md)  
 Viene fornito un esempio in cui da una stringa vengono eliminati i caratteri alfanumerici non validi.  
  
 [Procedura: Verificare che le stringhe siano in formato di posta elettronica valido](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md)  
 Viene fornito un esempio che è possibile utilizzare per verificare che il formato di posta elettronica di una stringa sia valido.  
  
## Riferimenti  
 <xref:System.Text.RegularExpressions>  
 Vengono fornite informazioni di riferimento sulla libreria di classi per lo spazio dei nomi di .NET Framework **System.Text.RegularExpressions**.  
  
## Sezioni correlate  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)  
 Viene fornita una panoramica dell'aspetto delle espressioni regolari relativo al linguaggio di programmazione.  
  
 [Modello a oggetti delle espressioni regolari](../../../docs/standard/base-types/the-regular-expression-object-model.md)  
 Vengono descritte le classi di espressioni regolari contenute nello spazio dei nomi `System.Text.RegularExpression` e vengono forniti esempi per il loro utilizzo.  
  
 [Dettagli sul comportamento delle espressioni regolari](../../../docs/standard/base-types/details-of-regular-expression-behavior.md)  
 Vengono fornite informazioni sulle funzionalità e il funzionamento delle espressioni regolari di .NET Framework.  
  
 [Linguaggio di espressioni regolari \- Riferimento rapido](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)  
 Vengono fornite informazioni sul set di caratteri, di operatori e di costrutti utilizzabili per definire le espressioni regolari.