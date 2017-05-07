---
title: Reindirizzamento delle modifiche in .NET Framework 4.5.1 | Documenti di Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application compatibility
- retargeting changes
- .NET Framework 4.5.1
- retargeting changes, .NET Framework 4.5.1
- retargeting changes, .NET Framework
ms.assetid: 8087326d-77e9-4804-ba33-ff1bb1bec2b8
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0c497561254c0f97f22ac05c7d44224b30ef74d0
ms.lasthandoff: 04/18/2017

---
# <a name="retargeting-changes-in-the-net-framework-451"></a>Reindirizzamento delle modifiche in .NET Framework 4.5.1
In rari casi, le modifiche di reindirizzamento possono influire sulle app che vengono ricompilate per [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]. Non influiscono sui file binari destinati a una versione precedente di .NET Framework ma vengono eseguiti nella versione 4.5.1. [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] include le modifiche di reindirizzamento nelle aree seguenti:  
  
-   [Base](#Core)  
  
-   [ADO.NET](#ADO)  
  
-   [MSBuild](#MSBuild)  
  
 La colonna Ambito nelle tabelle seguenti contiene il significato di ogni modifica:  
  
-   Principale Una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice. Si noti che le modifiche di reindirizzamento non rientrano in questa categoria.  
  
-   Secondaria. Una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.  
  
-   Bordo. Una modifica che influisce sulle app in scenari molto specifici e non comuni.  
  
-   Trasparente. Una modifica che non ha effetti evidenti sullo sviluppatore o sull'utente dell'app. L'app non dovrebbe richiedere variazioni a causa di questa modifica.  
  
<a name="Core"></a>   
## <a name="core-retargeting-changes"></a>Modifiche di reindirizzamento generali  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Attributo <xref:System.ObsoleteAttribute?displayProperty=fullName>|Quando si crea una raccolta di metadati Windows (file con estensione winmd), l'attributo <xref:System.ObsoleteAttribute> viene esportato sia come <xref:System.ObsoleteAttribute> che come [Windows.Foundation.DeprecatedAttribute](http://msdn.microsoft.com/library/windows/apps/windows.foundation.metadata.deprecatedattribute.aspx).|La ricompilazione del codice sorgente esistente che usa l'attributo <xref:System.ObsoleteAttribute> può generare avvisi quando tale codice viene usato da C++/CX o JavaScript.<br /><br /> Non è consigliabile applicare sia <xref:System.ObsoleteAttribute> che [Windows.Foundation.DeprecatedAttribute](http://msdn.microsoft.com/library/windows/apps/windows.foundation.metadata.deprecatedattribute.aspx) al codice negli assembly gestiti, perché potrebbero essere restituiti avvisi di compilazione.<br /><br /> Per altre informazioni, vedere l'argomento di riferimento <xref:System.ObsoleteAttribute>.|Microsoft Edge|  
  
<a name="ADO"></a>   
## <a name="adonet-retargeting-changes"></a>Modifiche di reindirizzamento di ADO.NET  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Classe <xref:System.Data.Common.DbParameter?displayProperty=fullName>|<xref:System.Data.Common.DbParameter.Precision%2A?displayProperty=fullName> e <xref:System.Data.Common.DbParameter.Scale%2A?displayProperty=fullName> vengono implementate come proprietà virtuali pubbliche. Sostituiscono le corrispondenti implementazioni esplicite dell'interfaccia <xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Precision%2A?displayProperty=fullName> e <xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Scale%2A?displayProperty=fullName>.|La modifica interessa solo gli sviluppatori che compilano un provider di database ADO.NET.|Marginale|  
  
<a name="MSBuild"></a>   
## <a name="msbuild-retargeting-changes"></a>Modifiche di reindirizzamento di MSBuild  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Attività `ResolveAssemblyReference`|L'attività genera un avviso, MSB3270, che indica la mancata corrispondenza di un riferimento o di una delle sue dipendenze all'architettura dell'app. Questa situazione si verifica ad esempio se un'app compilata con l'opzione `anycpu` include un riferimento x86. Uno scenario di questo tipo potrebbe provocare un errore dell'app in fase di esecuzione (nel caso descritto, se l'app viene distribuita come processo x64).|Le possibili conseguenze riguardano le aree seguenti:<br /><br /> -   La ricompilazione genera avvisi che non venivano visualizzati quando l'app veniva compilata con una versione precedente di MSBuild. Tuttavia, dal momento che l'avviso identifica una possibile fonte di errore di runtime, deve essere analizzato e affrontato.<br />-   Se gli avvisi vengono considerati errori, la compilazione dell'app non verrà completata.|Secondario|  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche al runtime](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)   
 [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Compatibilità delle applicazioni nella versione 4.5.2](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)
