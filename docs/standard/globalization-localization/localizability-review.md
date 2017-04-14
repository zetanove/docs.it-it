---
title: "Revisione della localizzabilit&#224; | Microsoft Docs"
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
  - "applicazioni a livello mondiale, localizzabilità"
  - "sviluppo di applicazioni [.NET Framework], localizzazione"
  - "localizzabilità [.NET Framework]"
  - "applicazioni internazionali [.NET Framework], localizzabilità"
  - "globalizzazione [.NET Framework], localizzabilità"
  - "impostazioni cultura, localizzabilità"
  - "localizzazione [.NET Framework], localizzabilità"
  - "applicazioni globali, localizzabilità"
  - "risorse (localizzazione)"
ms.assetid: 3aee2fbb-de47-4e37-8fe4-ddebb9719247
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Revisione della localizzabilit&#224;
La revisione di localizzabilità è un passaggio intermedio nello sviluppo di un'applicazione internazionale.  Verifica che un'applicazione globalizzata è pronta per la localizzazione e identifica tutto il codice o qualsiasi aspetto dell'interfaccia utente che richiedono una gestione speciale.  Questo passaggio contribuisce a garantire che durante il processo di localizzazione non verranno introdotti difetti funzionali nell'applicazione.  Quando tutti i problemi generati dall'analisi di localizzazione sono stati indirizzati, l'applicazione è pronta per la localizzazione.  Se la revisione di localizzabilità è completa, non è necessario modificare qualsiasi codice sorgente durante il processo di localizzazione.  
  
 La revisione di localizzabilità consiste nei seguenti tre controlli:  
  
-   [Sono implementati i requisiti di globalizzazione?](#global)  
  
-   [Le funzionalità dipendenti dalle impostazioni cultura vengono gestite correttamente?](#culture)  
  
-   [Si è testata l'applicazione con dati internazionali?](#test)  
  
<a name="global"></a>   
## Implementazione dei requisiti di globalizzazione  
 Se l'applicazione è stata progettata e sviluppata con la localizzazione e se sono stati seguiti i requisiti descritti nell'articolo di [Globalizzazione](../../../docs/standard/globalization-localization/globalization.md), la revisione di localizzabilità sarà ampiamente una sessione di controllo di qualità.  In caso contrario, durante questa fase è necessario rivedere e implementare i requisiti per la [globalizzazione](../../../docs/standard/globalization-localization/globalization.md) e la correzione degli errori nel codice sorgente che impediscono la localizzazione.  
  
<a name="culture"></a>   
## Gestione delle funzionalità dipendenti dalle impostazioni cultura  
 .NET Framework non fornisce supporto a livello di codice in numerose aree che variano notevolmente dalle impostazioni cultura.  Nella maggior parte dei casi, è necessario scrivere codice personalizzato per gestire le aree funzionali come segue:  
  
-   Indirizzi  
  
-   Numeri di telefono.  
  
-   Formati di carta.  
  
-   Unità di misura utilizzate per le lunghezze, i pesi, l'area, il volume e le temperature.  Benché .NET Framework non offra il supporto incorporato per la conversione tra le unità di misura, è possibile utilizzare la proprietà <xref:System.Globalization.RegionInfo.IsMetric%2A?displayProperty=fullName> per determinare se un paese o una particolare area utilizza il sistema metrico, come illustrato di seguito.  
  
     [!code-csharp[Conceptual.Localizability#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.localizability/cs/ismetric1.cs#1)]
     [!code-vb[Conceptual.Localizability#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.localizability/vb/ismetric1.vb#1)]  
  
<a name="test"></a>   
## Test dell'applicazione  
 Prima di localizzare l'applicazione, è necessario testarla utilizzando i dati internazionali in versioni internazionali del sistema operativo.  Sebbene la maggior parte dell'interfaccia utente non sia localizzata in questa fase, sarà possibile rilevare problemi come i seguenti:  
  
-   I dati serializzati che non si deserializzano correttamente nella versione del sistema operativo.  
  
-   Dati numerici che non riflettono le convenzioni delle impostazioni cultura correnti.  Ad esempio, i numeri possono essere visualizzati con i separatori di gruppi, separatori decimali, o simboli di valuta non corretti.  
  
-   Informazioni di data e ora che non riflettono le convenzioni delle impostazioni cultura correnti.  Ad esempio, i numeri che rappresentano il mese e il giorno possono apparire nell'ordine errato, separatori di data possono essere errati, o le informazioni del fuso orario possono essere errate.  
  
-   Risorse che non sono disponibili in quanto non sono identificate le impostazioni cultura predefinite dell'applicazione.  
  
-   Stringhe visualizzate in modo anomalo per impostazioni cultura specifiche.  
  
-   Confronti di stringhe o confronti per l'uguaglianza che restituiscono risultati imprevisti.  
  
 Se sono stati seguiti i requisiti di globalizzazione quando si compila l'applicazione, gestite correttamente le funzionalità dipendenti dalle impostazioni cultura e identificati e risolti i problemi di localizzazione che sono sorti durante i test, è possibile procedere al passaggio successivo, [Localizzazione](../../../docs/standard/globalization-localization/localization.md).  
  
## Vedere anche  
 [Globalizzazione e localizzazione](../../../docs/standard/globalization-localization/index.md)   
 [Localizzazione](../../../docs/standard/globalization-localization/localization.md)   
 [Globalizzazione](../../../docs/standard/globalization-localization/globalization.md)   
 [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md)