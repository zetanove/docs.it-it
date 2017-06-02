---
title: "Security and On-the-Fly Code Generation | Microsoft Docs"
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
  - "code security, on-the-fly code generation"
  - "on-the-fly code generation"
  - "security [.NET Framework], on-the-fly code generation"
  - "secure coding, on-the-fly code generation"
ms.assetid: 6d221724-bb21-4d76-90c3-0ee2a2e69be2
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Security and On-the-Fly Code Generation
Alcune librerie funzionano tramite la generazione e l'esecuzione di codice per eseguire alcune operazioni per il chiamante.  Il problema di fondo è costituito dalla generazione di codice per conto di codice meno attendibile e dalla relativa esecuzione con attendibilità superiore  e diventa più grave quando il chiamante è in grado di influenzare la generazione di codice, per cui è necessario che venga generato solo codice sicuro.  
  
 È preferibile sapere esattamente quale tipo di codice si genera in ogni momento;  in altre parole, è necessario avere un controllo totale sui valori ottenuti da un utente, che si tratti di stringhe racchiuse tra virgolette, che devono essere sottoposte a escape per evitare che includano elementi di codice non previsti, identificatori, di cui è necessario verificare la validità, o altri elementi.  Gli identificatori possono rappresentare un pericolo in quanto la modifica di un assembly compilato può determinare la comparsa di caratteri insoliti negli identificatori, che ne possono provocare il blocco; questa condizione, tuttavia, costituisce raramente una vulnerabilità di sicurezza.  
  
 È preferibile generare codice tramite la reflection emit, che spesso consente di evitare gran parte di questi problemi.  
  
 Durante la compilazione del codice, stabilire se un programma dannoso è in grado di modificarlo.  In un lasso di tempo molto breve, il codice dannoso può modificare il codice sorgente sul disco prima che il compilatore sia in grado di leggerlo o prima che sia possibile caricare nel codice il file DLL.  In questo caso è necessario proteggere la directory che contiene file di questo tipo tramite la sicurezza per l'accesso al codice o un elenco di controllo di accesso \(ACL\), se necessario.  
  
 Se un chiamante è in grado di influenzare il codice generato in modo tale da provocare un errore di compilazione, può esistere una vulnerabilità di sicurezza.  
  
 Eseguire il codice generato con il livello più basso di impostazioni di autorizzazione, usando <xref:System.Security.Permissions.SecurityAction>[Deny](http://msdn.microsoft.com/it-it/6b4d2e01-c504-4ac3-b50e-d6f5e7f5df25).  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)