---
title: "Assembly su pi&#249; file | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], su più file"
  - "manifesto assembly, assembly su più file"
  - "moduli di codice"
  - "riga di comando (compilatori)"
  - "compilazione di assembly"
  - "punto di ingresso per assembly"
  - "assembly su più file"
ms.assetid: 13509e73-db77-4645-8165-aad8dfaedff6
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Assembly su pi&#249; file
È possibile creare assembly su più file mediante i compilatori da riga di comando o [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] con Visual C\+\+.  È necessario che almeno un file dell'assembly contenga il manifesto dell'assembly.  È inoltre necessario che un assembly che avvia un'applicazione contenga un punto di ingresso, ad esempio un metodo Main o WinMain.  
  
 Si supponga, ad esempio, di disporre di un'applicazione che contiene due moduli di codice, Client.cs e Stringer.cs.  Stringer.cs crea lo spazio dei nomi `myStringer` a cui fa riferimento il codice in Client.cs.  Client.cs contiene il metodo `Main` che è il punto di ingresso dell'applicazione.  In questo esempio si compilano i due moduli di codice, quindi si crea un terzo file contenente il manifesto dell'assembly, che consente il lancio dell'applicazione.  Nel manifesto dell'assembly sono presenti riferimenti sia al modulo `Client` che al modulo `Stringer`.  
  
> [!NOTE]
>  Negli assembly su più file è consentito un solo punto di ingresso, anche se l'assembly dispone di più moduli di codice.  
  
 La creazione di un assembly su più file potrebbe risultare consigliabile per svariate ragioni:  
  
-   Per combinare moduli scritti in linguaggi diversi.  L'assembly su più file viene solitamente creato per questa ragione.  
  
-   Per ottimizzare il download di un'applicazione inserendo i tipi raramente utilizzati in un modulo che viene scaricato solo quando necessario.  
  
    > [!NOTE]
    >  Se si creano applicazioni il cui download verrà eseguito utilizzando il tag `<object>` con Microsoft Internet Explorer, è importante creare assembly su più file.  In uno scenario di questo tipo si crea un file distinto dai moduli di codice e contenente solo il manifesto dell'assembly.  In Internet Explorer viene eseguito prima di tutto il download del manifesto dell'assembly, quindi vengono creati thread di lavoro per eseguire il download di eventuali moduli o assembly aggiuntivi necessari.  Durante il download del file contenente il manifesto dell'assembly, Internet Explorer non risponderà all'input dell'utente.  Dimensioni ridotte del file contenente il manifesto dell'assembly implicano una riduzione del tempo di assenza di risposta da parte di Internet Explorer.  
  
-   Per combinare moduli di codice scritti da diversi sviluppatori.  Benché i singoli sviluppatori siano in grado di compilare ogni modulo di codice nell'assembly, è possibile che questa operazione provochi l'esposizione di alcuni tipi, che non risultano esposti se tutti i moduli vengono inseriti in un assembly su più file.  
  
 Una volta creato l'assembly, è possibile firmare il file contenente il manifesto dell'assembly \(e quindi l'assembly\) o assegnare un nome sicuro al file \(e all'assembly\) e inserirlo nella Global Assembly Cache.  
  
## Vedere anche  
 [Procedura: Compilare un assembly su più file](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)   
 [Programmazione con gli assembly](../../../docs/framework/app-domains/programming-with-assemblies.md)