---
title: "Operazioni sulle stringhe indipendenti dalle impostazioni cultura | Microsoft Docs"
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
  - "confronti con distinzione tra maiuscole e minuscole"
  - "impostazioni cultura, operazioni su stringhe senza distinzione di impostazioni cultura"
  - "operazioni su stringhe senza distinzione di impostazioni cultura"
  - "operazioni su stringhe con distinzione di impostazioni cultura"
  - "globalizzazione [.NET Framework], operazioni su stringhe senza distinzione di impostazioni cultura"
  - "localizzazione [.NET Framework], operazioni su stringhe senza distinzione di impostazioni cultura"
  - "stringhe [.NET Framework], operazioni su stringhe senza distinzione di impostazioni cultura"
  - "applicazioni world-ready, operazioni su stringhe senza distinzione di impostazioni cultura"
ms.assetid: e6e2bb94-a95d-44e2-b68c-cfdd1db77784
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Operazioni sulle stringhe indipendenti dalle impostazioni cultura
Le operazioni eseguite sulle stringhe dipendenti dalle impostazioni cultura possono costituire un vantaggio nella creazione di applicazioni progettate per la visualizzazione dei risultati in base alle impostazioni cultura.  Per impostazione predefinita, i metodi dipendenti dalle impostazioni cultura ottengono le impostazioni cultura da utilizzare dalla proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A> del thread corrente.  
  
 Si noti che le operazioni sulle stringhe dipendenti dalle impostazioni cultura, tuttavia, non sempre corrispondono al comportamento desiderato.  L'utilizzo di operazioni dipendenti dalle impostazioni cultura nei casi in cui è preferibile che i risultati siano indipendenti dalle impostazioni cultura può determinare errori nel codice dell'applicazione per le impostazioni cultura con mappatura di maiuscole\/minuscole personalizzata e regole di ordinamento.  Per un esempio, vedere la sezione "Confronti di stringhe che utilizzano le impostazioni cultura correnti" nell'articolo [Procedure consigliate per l'utilizzo di stringhe](../../../docs/standard/base-types/best-practices-strings.md).  
  
 L'opportunità di utilizzare operazioni sulle stringhe dipendenti oppure indipendenti dalle impostazioni cultura è determinata dall'utilizzo dei risultati da parte dell'applicazione.  È in genere preferibile che le operazioni sulle stringhe che determinano la visualizzazione di risultati siano dipendenti dalle impostazioni cultura.  Se in un'applicazione viene visualizzato un elenco ordinato di stringhe localizzate in una casella di riepilogo, ad esempio, l'applicazione dovrebbe eseguire un ordinamento dipendente dalle impostazioni cultura.  
  
 I risultati delle operazioni sulle stringhe utilizzate internamente devono in genere essere indipendenti dalle impostazioni cultura.  In generale, se l'applicazione utilizza nomi file, formati di persistenza o informazioni sui simboli che non vengono visualizzati, è opportuno che i risultati delle operazioni sulle stringhe non varino in base alle impostazioni cultura.  Se in un'applicazione viene confrontata una stringa per determinare se costituisce un tag XML riconosciuto, ad esempio, il confronto deve essere indipendente dalle impostazioni cultura.  Inoltre, se una decisione relativa alla sicurezza è basata sul risultato di un confronto di stringhe o di un'operazione di modifica di maiuscole e minuscole, è necessario che l'operazione sia indipendente dalle impostazioni cultura in modo che il risultato non venga influenzato dal valore di <xref:System.Globalization.CultureInfo.CurrentCulture%2A>.  
  
 Indipendentemente dal fatto che l'applicazione sviluppata comprenda o meno codice per la gestione dei problemi di localizzazione e globalizzazione, è opportuno tenere in considerazione i metodi di .NET Framework che per impostazione predefinita recuperano risultati dipendenti dalle impostazioni cultura.  Il presente argomento ha lo scopo di illustrare il corretto utilizzo di tali metodi da parte delle applicazioni per ottenere risultati indipendenti dalle impostazioni cultura.  
  
## Vedere anche  
 [Globalizzazione e localizzazione](../../../docs/standard/globalization-localization/index.md)