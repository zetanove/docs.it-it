---
title: Globalizzazione e localizzazione di applicazioni .NET Framework | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- international applications [.NET Framework]
- globalization [.NET Framework], encoding
- global applications
- internationalization
- world-ready applications
- application development [.NET Framework], globalization
- multilingual application development
ms.assetid: 9a59696b-d89b-45bd-946d-c75da4732d02
caps.latest.revision: 42
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: d6313cea51b98b3b19363f3c465e5adf241ab3d4
ms.lasthandoff: 04/08/2017

---
# <a name="globalizing-and-localizing-net-framework-applications"></a>Globalizzazione e localizzazione di applicazioni .NET Framework
Lo sviluppo di [applicazioni internazionali](http://msdn.microsoft.com/goglobal/bb978433.aspx), tra cui un'applicazione che può essere localizzata in una o più lingue, include i seguenti tre passaggi: globalizzazione, analisi della localizzabilità e localizzazione.  
  
 [Globalizzazione](../../../docs/standard/globalization-localization/globalization.md)  
 Questo passaggio implica la progettazione e la codifica di un'applicazione indipendente dalle impostazioni cultura e dalla lingua che supporti le interfacce utente e i dati internazionali localizzati per tutti gli utenti. Comporta decisioni di progettazione e programmazione non basate su presupposti impostazioni cultura specifiche. Quando un'applicazione globalizzata non viene localizzata, è tuttavia progettata e scritta in modo da poter essere successivamente localizzata in una o più lingue in modo relativamente semplice.  
  
 [Revisione della localizzabilità](../../../docs/standard/globalization-localization/localizability-review.md)  
 Questo passaggio prevede la revisione del codice e del progetto di un'applicazione per verificare che possa essere localizzata facilmente e per identificare potenziali problemi per la localizzazione e la verifica che il codice eseguibile dell'applicazione sia separato dalle relative risorse. Se la fase di globalizzazione ha avuto effetto, l'analisi della localizzabilità confermerà le scelte di codifica e di progettazione effettuate durante la globalizzazione. La fase di localizzabilità può inoltre identificare eventuali problemi rimanenti. In questo modo, il codice sorgente di un'applicazione non deve necessariamente essere modificato durante la fase di localizzazione.  
  
 [Localizzazione](../../../docs/standard/globalization-localization/localization.md)  
 Questo passaggio prevede la personalizzazione di un'applicazione per impostazioni cultura e aree specifiche. Se i passaggi di globalizzazione e possibilità di localizzazione sono stati eseguiti correttamente, la localizzazione consiste principalmente nella traduzione dell'interfaccia utente.  
  
 Se si ci attiene ai seguenti tre passaggi verranno offerti due vantaggi:  
  
-   In questo modo, non è necessario adattare un'applicazione progettata per supportare singole lingue, ad esempio Inglese US (Stati Uniti), per supportare le lingue aggiuntive.  
  
-   Restituisce applicazioni localizzate che sono più stabile e con meno bug.  
  
 In .NET Framework viene fornito supporto esteso per lo sviluppo di applicazioni internazionali e localizzate. In particolare, molti membri del tipo nella libreria di classi .NET Framework facilitano la globalizzazione restituendo valori che riflettono le convenzioni delle impostazioni cultura dell'utente o di impostazioni cultura specifiche. Inoltre, .NET Framework supporta gli assembly satellite, che semplificano il processo di localizzazione di un'applicazione.  
  
 Per altre informazioni, vedere il [Developer Center sulla globalizzazione delle applicazioni](http://go.microsoft.com/fwlink/?LinkId=235015).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Globalizzazione](../../../docs/standard/globalization-localization/globalization.md)  
 Viene descritta la prima fase di creazione di un'applicazione internazionale, che include la progettazione e la codifica di un'applicazione indipendente dalla lingua e dalle impostazioni cultura.  
  
 [Revisione della localizzabilità](../../../docs/standard/globalization-localization/localizability-review.md)  
 Viene descritta la seconda fase di creazione di un'applicazione localizzata, che include l'identificazione dei potenziali blocchi stradali per la localizzazione.  
  
 [Localizzazione](../../../docs/standard/globalization-localization/localization.md)  
 Viene illustrata la fase finale della creazione di un'applicazione localizzata, che include la personalizzazione di un'interfaccia utente dell'applicazione per le aree o le impostazioni cultura specifiche.  
  
 [Operazioni sulle stringhe indipendenti dalle impostazioni cultura](../../../docs/standard/globalization-localization/culture-insensitive-string-operations.md)  
 Viene descritto come utilizzare metodi e classi di .NET Framework definiti come dipendenti dalle impostazioni cultura per impostazione predefinita per ottenere risultati indipendenti dalle impostazioni cultura.  
  
 [Procedure consigliate per lo sviluppo di applicazioni internazionali](../../../docs/standard/globalization-localization/best-practices-for-developing-world-ready-apps.md)  
 Vengono forniti alcuni suggerimenti per la globalizzazione, la localizzazione e lo sviluppo di applicazioni ASP.NET internazionali.  
  
## <a name="reference"></a>Riferimento  
 Spazio dei nomi <xref:System.Globalization?displayProperty=fullName>  
 Contiene le classi che definiscono le informazioni correlate alle impostazioni cultura quali lingua, paese, calendari, formato per date, valute e numeri e tipo di ordinamento delle stringhe.  
  
 Spazio dei nomi <xref:System.Resources>  
 Vengono fornite le classi per la creazione, la manipolazione e l'uso di risorse.  
  
 Spazio dei nomi <xref:System.Text>  
 Contiene le classi che rappresentano le codifiche dei caratteri ASCII, ANSI, Unicode e altri tipi di codifiche.  
  
 [Resgen.exe (generatore di file di risorse)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)  
 Viene descritto l'utilizzo di Resgen.exe per convertire i file con estensione txt e resx (formato risorse basato su XML) in file binari con estensione resources di Common Language Runtime.  
  
 [Winres.exe (editor di risorse di Windows Form)](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)  
 Viene descritto l'uso di Winres.exe per localizzare i form di Windows Form.
