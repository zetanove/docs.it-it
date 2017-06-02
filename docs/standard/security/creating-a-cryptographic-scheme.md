---
title: "Creating a Cryptographic Scheme | Microsoft Docs"
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
  - "encryption [.NET Framework], creating cryptographic schemes"
  - "cryptography [.NET Framework], creating cryptographic schemes"
ms.assetid: d40c509f-5a5e-46cc-94cb-a951e9ab6843
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Creating a Cryptographic Scheme
I componenti di crittografia di .NET Framework possono essere combinati per creare diversi schemi per la crittografia e la decrittografia dei dati.  
  
 Uno schema di crittografia semplice per la crittografia e la decrittografia dei dati può specificare i passaggi seguenti:  
  
1.  Ogni parte genera una coppia di chiavi pubblica\/privata.  
  
2.  Le parti si scambiano le chiavi pubbliche.  
  
3.  Ogni parte genera una chiave segreta per la crittografia TripleDES, ad esempio, e crittografa la nuova chiave creata usando la chiave pubblica dell'altra parte.  
  
4.  Ogni parte invia i dati all'altra parte e combina la chiave segreta dell'altra parte con la propria, in un ordine specifico, per creare una nuova chiave segreta.  
  
5.  Le parti avviano quindi una conversazione usando la crittografia simmetrica.  
  
 La creazione di uno schema di crittografia non è un'attività banale.  Per altre informazioni sull'uso della crittografia, vedere l'argomento Crittografia nella documentazione di Platform SDK all'indirizzo http:\/\/msdn.microsoft.com\/library.  
  
## Vedere anche  
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)