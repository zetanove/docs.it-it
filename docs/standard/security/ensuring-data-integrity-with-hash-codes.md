---
title: "Ensuring Data Integrity with Hash Codes | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "generating hash"
  - "verifying hash codes"
  - "cryptography [.NET Framework], hash"
  - "data integrity"
  - "checking hash codes"
  - "encryption [.NET Framework], hash"
  - "hash"
ms.assetid: 33660f33-b70f-4dca-8c87-ab35cfc2961a
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# Ensuring Data Integrity with Hash Codes
Un valore hash è un valore numerico di lunghezza fissa che identifica in modo univoco i dati.  I valori hash rappresentano grandi quantità di dati sotto forma di valori numerici molto più piccoli, pertanto vengono usati con le firme digitali.  È possibile firmare un valore hash in modo più efficiente rispetto alla firma di un valore più grande.  I valori hash sono anche utili per verificare l'integrità dei dati inviati attraverso canali non sicuri.  Il valore hash dei dati ricevuti può essere confrontato con il valore hash dei dati inviati per determinare se i dati sono stati modificati.  
  
 Questo argomento descrive come generare e verificare codici hash usando le classi nello spazio dei nomi <xref:System.Security.Cryptography?displayProperty=fullName>.  
  
## Generazione di un hash  
 Le classi hash gestite possono eseguire l'hashing di una matrice di byte o di un oggetto flusso gestito.  L'esempio seguente usa l'algoritmo hash SHA1 per creare un valore hash per una stringa.  L'esempio usa la classe <xref:System.Text.UnicodeEncoding> per convertire la stringa in una matrice di byte sottoposti ad hashing tramite la classe <xref:System.Security.Cryptography.SHA1Managed>.  Il valore hash viene quindi visualizzato nella console.  
  
 [!code-csharp[GeneratingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/generatingahash/cs/program.cs#1)]
 [!code-vb[GeneratingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/generatingahash/vb/program.vb#1)]  
  
 Questo codice visualizza la stringa seguente nella console:  
  
 `59 4 248 102 77 97 142 201 210 12 224 93 25 41 100 197 213 134 130 135`  
  
## Verifica di un hash  
 I dati possono essere confrontati con un valore hash per determinarne l'integrità.  In genere, viene eseguito l'hashing dei dati in un determinato momento e il valore hash viene protetto in un determinato modo.  Successivamente, i dati possono essere sottoposti di nuovo a hashing e confrontati con il valore protetto.  Se i valori hash corrispondono, i dati non sono stati modificati.  Se i valori hash non corrispondono, i dati sono stati danneggiati.  Affinché questo sistema funzioni, l'hash protetto deve essere crittografato o mantenuto segreto a tutte le parti non attendibili.  
  
 L'esempio seguente confronta il valore hash precedente di una stringa con un nuovo valore hash.  L'esempio analizza in ciclo ogni byte dei valori hash ed effettua un confronto.  
  
 [!code-csharp[VerifyingAHash#1](../../../samples/snippets/csharp/VS_Snippets_CLR/verifyingahash/cs/program.cs#1)]
 [!code-vb[VerifyingAHash#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/verifyingahash/vb/program.vb#1)]  
  
 Se i due valori hash corrispondono, il codice visualizza quanto segue nella console:  
  
```  
The hash codes match.  
```  
  
 Se non corrispondono, il codice visualizza quanto segue:  
  
```  
The hash codes do not match.  
```  
  
## Vedere anche  
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)