---
title: "Procedura: eseguire la conversione tra codifiche legacy e Unicode (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "conversioni [C#], da codifica legacy a Unicode"
  - "stringhe [C#], conversione tra codifiche"
ms.assetid: 4eed7d8e-47ab-4a7c-8b95-9645a0ef000b
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: eseguire la conversione tra codifiche legacy e Unicode (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In C\#, tutte le stringhe in memoria sono codificate come Unicode \(UTF\-16\).  I dati trasferiti da un archivio a un oggetto `string` vengono automaticamente convertiti in UTF\-16.  Se i dati contengono solo valori ASCII compresi tra 0 e 127, non sono richieste operazioni aggiuntive.  Se invece il testo di origine contiene valori di byte ASCII estesi \(da 128 a 255\), per impostazione predefinita i caratteri estesi saranno interpretati sulla base della tabella codici corrente.  Per specificare che il testo di origine deve essere interpretato sulla base di una tabella codici diversa, utilizzare la classe <xref:System.Text.Encoding?displayProperty=fullName> come mostrato nell'esempio seguente.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come convertire un file di testo codificato in ASCII a 8 bit, interpretando il testo di origine sulla base della tabella codici 737 di Windows.  
  
 [!code-cs[csProgGuideStrings#34](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-convert-between-legacy-encodings-and-unicode_1.cs)]  
  
## Vedere anche  
 [Stringhe](../../../csharp/programming-guide/strings/index.md)