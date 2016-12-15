---
title: "WriteOnly (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "WriteOnly"
  - "vb.WriteOnly"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "write-only properties"
  - "WriteOnly keyword"
  - "sensitive data, protecting"
  - "properties [Visual Basic], write-only"
  - "sensitive data"
ms.assetid: 488d2899-b09f-4cee-92f0-6f9f9fc4f944
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# WriteOnly (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che è possibile scrivere ma non leggere una proprietà.  
  
## Note  
  
## Regole  
 **Contesto della dichiarazione.** È possibile utilizzare la parola chiave `WriteOnly` solo a livello di modulo.  In altri termini, il contesto della dichiarazione per una proprietà `WriteOnly` deve essere una classe, una struttura o un modulo e non può essere un file di origine, uno spazio dei nomi o una routine.  
  
 È possibile dichiarare come `WriteOnly` una proprietà ma non una variabile.  
  
## Utilizzo di WriteOnly  
 In alcuni casi è utile che il codice utilizzato sia in grado di impostare un valore senza scoprire di che valore si tratta.  L'accesso a dati sensibili, quali un codice fiscale o una password, ad esempio, deve essere impedito ai componenti che non ne hanno effettuato l'impostazione.  In questi casi è possibile impostare il valore utilizzando una proprietà `WriteOnly`.  
  
> [!IMPORTANT]
>  Quando si definisce e si utilizza una proprietà `WriteOnly`, prendere in considerazione le seguenti misure protettive aggiuntive:  
  
-   **Override.** Se la proprietà è un membro di una classe, consentire l'impostazione predefinita [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md) e non dichiararla come `Overridable` o `MustOverride`.  In questo modo si impedisce l'accesso non desiderato di una classe derivata mediante un override.  
  
-   **Livello di accesso.** Se i dati sensibili della proprietà sono contenuti in una o più variabili, è necessario dichiararli come [Private](../../../visual-basic/language-reference/modifiers/private.md), in modo da impedirne l'accesso da parte di altro codice.  
  
-   **Crittografia.** Archiviare tutti i dati sensibili in forma crittografata anziché in testo normale.  Se in qualche modo codice dannoso riesce ad accedere a quell'area di memoria, sarà più difficile utilizzare i dati.  La crittografia risulta utile anche quando è necessario serializzare i dati sensibili.  
  
-   **Ripristino.** Quando la classe, la struttura o il modulo che definisce la proprietà sta per terminare, ripristinare i valori predefiniti o altri valori non significativi dei dati sensibili.  Questa operazione fornisce una protezione aggiuntiva quando viene consentito l'accesso generale all'area di memoria interessata.  
  
-   **Persistenza.** Se è possibile, evitare di memorizzare dati sensibili in maniera permanente, ad esempio sul disco,  nonché di scrivere dati sensibili negli Appunti.  
  
 È possibile utilizzare il modificatore `WriteOnly` nel seguente contesto:  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## Vedere anche  
 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)