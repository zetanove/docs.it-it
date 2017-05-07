---
title: Reindirizzamento delle modifiche in .NET Framework 4.5.2 | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2be2a828-9052-4738-a965-d4a836cc6384
caps.latest.revision: 5
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 10af942724ce0207bc6e64f1ebabfdcd2d3488bd
ms.lasthandoff: 04/18/2017

---
# <a name="retargeting-changes-in-the-net-framework-452"></a>Reindirizzamento delle modifiche in .NET Framework 4.5.2
In rari casi, le modifiche di reindirizzamento possono influire sulle app che vengono ricompilate per .NET Framework 4.5.2. A meno che non venga specificato diversamente nelle seguenti tabelle, queste modifiche non influiscono sui file binari destinati a una versione precedente di .NET Framework ma vengono eseguiti nella versione 4.5.2. .NET Framework 4.5.2 include modifiche di reindirizzamento nelle seguenti aree:  
  
-   [Entity Framework](#EF)  
  
-   [Windows Form](#WinForms)  
  
<a name="EF"></a>   
## <a name="entity-framework-retargeting-changes"></a>Modifiche di reindirizzamento di Entity Framework  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Query più semplici quando si usano operazioni di limitazione non ordinate|Tramite le query che producono istruzioni `JOIN` e contengono una chiamata a un'operazione di limitazione senza prima usare <xref:System.Data.Objects.ObjectQuery%601.OrderBy%2A> viene prodotto codice SQL più semplice. Dopo l'aggiornamento a [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], queste query producevano codice SQL più complesso rispetto alle versioni precedenti.|Questa funzionalità è disabilitata per impostazione predefinita. Se Entity Framework genera istruzioni `JOIN` aggiuntive che causano una riduzione del livello delle prestazioni, è possibile abilitare questa funzionalità aggiungendo la voce seguente alla sezione `<appSettings>` del file di configurazione dell'applicazione (app.config):<br /><br /> `<add key="EntityFramework_SimplifyLimitOperations" value="true" />`|Secondario|  
  
<a name="WinForms"></a>   
## <a name="windows-forms-retargeting-changes"></a>Modifiche di reindirizzamento di Windows Form  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Recupero dei dati in formato HTML dagli Appunti con il metodo <xref:System.Windows.Forms.DataObject.GetData%2A?displayProperty=fullName>|Per le app destinate a [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] o che vengono eseguite in .NET Framework 4.5.1 o versioni precedenti, <xref:System.Windows.Forms.DataObject.GetData%2A?displayProperty=fullName> recupera dati in formato HTML sotto forma di stringa ASCII. Di conseguenza, i caratteri non ASCII, ovvero quelli i cui codici ASCII sono maggiori di 0x7F, vengono rappresentati da due caratteri casuali. Ad esempio, é (0xE9) è rappresentato da Ã© (0xC3 0xA9).<br /><br /> Per le app destinate a [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] o versione successiva e che vengono eseguite in .NET Framework 4.5.2, <xref:System.Windows.Forms.DataObject.GetData%2A?displayProperty=fullName> recupera i dati in formato HTML come UTF-8, che rappresenta correttamente i caratteri maggiori di 0x7F.|Se è stata implementata una soluzione alternativa per il problema di codifica con le stringhe in formato HTML, ad esempio codificando in modo esplicito la stringa HTML recuperata dagli Appunti passandola al metodo <xref:System.Text.UTF8Encoding.GetString%2A?displayProperty=fullName>, e si intende ridestinare l'app dalla versione 4 alla versione 4.5, è necessario rimuovere questa soluzione alternativa.|Secondario|  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-2.md)   
 [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Compatibilità delle applicazioni nella versione 4.5.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-1.md)
