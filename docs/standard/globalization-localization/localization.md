---
title: "Localizzazione | Microsoft Docs"
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
  - "sviluppo di applicazioni [.NET Framework], localizzazione"
  - "blocchi di codice"
  - "impostazioni cultura, localizzazione"
  - "applicazioni globali, localizzazione"
  - "globalizzazione [.NET Framework], localizzazione"
  - "applicazioni internazionali [.NET Framework], localizzazione"
  - "localizzazione [.NET Framework], informazioni"
  - "risorse (localizzazione)"
  - "blocchi di interfacce utente"
  - "applicazioni world-ready, localizzazione"
ms.assetid: 49d520d7-92d7-44ee-bb24-8b615db1d41b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Localizzazione
La localizzazione è il processo di traduzione delle risorse di un'applicazione nelle versioni localizzate per tutte le impostazioni cultura che verranno supportate dall'applicazione.  Prima di intraprendere il processo di localizzazione, è necessario avere completato la fase per verificare la [Revisione della localizzabilità](../../../docs/standard/globalization-localization/localizability-review.md) per verificare che l'applicazione globalizzata sia pronta per la localizzazione.  
  
 Un'applicazione pronta per la localizzazione è divisa in due blocchi concettuali: un blocco che contiene tutti gli elementi dell'interfaccia utente e un blocco che contiene il codice eseguibile.  Il blocco che contiene l'interfaccia utente include solo gli elementi dell'interfaccia utente localizzabili, come ad esempio le stringhe, i messaggi di errore, le finestre di dialogo, i menu, le risorse di oggetti incorporati e così via per le impostazioni cultura di sistema.  Il blocco che contiene il codice include solo il codice applicativo dell'applicazione da utilizzare per tutte le impostazioni cultura supportate.  In Common Language Runtime viene supportato un modello di risorse basato sugli assembly satellite grazie al quale il codice eseguibile dell'applicazione viene separato dalle relative risorse.  Per ulteriori informazioni sull'implementazione di questo modello, vedere [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md).  
  
 Per ciascuna versione localizzata dell'applicazione, aggiungere un nuovo assembly satellite contenente il blocco dell'interfaccia utente localizzata tradotto nella lingua appropriata per le impostazioni cultura di destinazione.  Il blocco contenente il codice per tutte le impostazioni cultura deve restare lo stesso.  La combinazione di una versione localizzata del blocco contenente l'interfaccia utente con il blocco contenente il codice genera una versione localizzata dell'applicazione.  
  
 Con [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] viene fornito l'Editor risorse di Windows Form \(Winres.exe\), che consente di localizzare rapidamente Windows Form per le impostazioni cultura di destinazione.  Per informazioni sull'utilizzo di questo strumento, vedere [Winres.exe \(Windows Forms Resource Editor\)](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md).  
  
## Vedere anche  
 [Globalizzazione e localizzazione](../../../docs/standard/globalization-localization/index.md)   
 [Revisione della localizzabilità](../../../docs/standard/globalization-localization/localizability-review.md)   
 [Globalizzazione](../../../docs/standard/globalization-localization/globalization.md)   
 [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md)