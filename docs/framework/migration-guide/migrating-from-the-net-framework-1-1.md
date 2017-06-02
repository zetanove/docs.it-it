---
title: Migrazione da .NET Framework 1.1 | Documenti di Microsoft
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
- .NET Framework 4.5, migrating from 1.1
- .NET Framework 1.1, migrating to .NET Framework 4.5
ms.assetid: 7ead0cb3-3b19-414a-8417-a1c1fa198d9e
caps.latest.revision: 12
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 6a9df183b13a84f8ded047892c0e4b7f7d5f0d60
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="migrating-from-the-net-framework-11"></a>Migrazione da .NET Framework 1.1
[!INCLUDE[win7](../../../includes/win7-md.md)] e le versioni successive del sistema operativo Windows non supportano [!INCLUDE[net_v11_long](../../../includes/net-v11-long-md.md)]. Di conseguenza, le applicazioni destinate a [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] non verranno eseguite senza modifica in [!INCLUDE[win7](../../../includes/win7-md.md)] o nelle versioni successive del sistema operativo. Questo argomento illustra i passaggi richiesti per eseguire un'applicazione destinata a [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] in [!INCLUDE[win7](../../../includes/win7-md.md)] e nelle versioni successive del sistema operativo Windows. Per altre informazioni su [!INCLUDE[net_v11_long](../../../includes/net-v11-long-md.md)] e [!INCLUDE[win8](../../../includes/win8-md.md)], vedere [Esecuzione delle applicazioni .NET Framework 1.1 in Windows 8 e versioni successive](../../../docs/framework/install/run-net-framework-1-1-apps.md).  
  
## <a name="retargeting-or-recompiling"></a>Reindirizzamento o ricompilazione  
 Per fare in modo che un'applicazione compilata usi [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] per l'esecuzione in [!INCLUDE[win7](../../../includes/win7-md.md)] o in una versione successiva del sistema operativo Windows sono disponibili due modalità:  
  
-   È possibile reindirizzare l'applicazione affinché venga eseguita in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]. Il reindirizzamento richiede l'aggiunta di un elemento [\<supportedRuntime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) al file di configurazione dell'applicazione che ne consenta l'esecuzione in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. Tale file di configurazione prende il form seguente:  
  
    ```xml  
    <configuration>   
       <startup>  
          <supportedRuntime version="v4.0"/>  
       </startup>  
    </configuration>  
    ```  
  
-   È possibile ricompilare l'applicazione con un compilatore destinato a [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. Se è stato originariamente usato Visual Studio 2003 per sviluppare e compilare la soluzione, è possibile aprirla in [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)] e usare la finestra di dialogo **Compatibilità del progetto** per convertire la soluzione e i file di progetto dai formati usati da Visual Studio 2003 al formato Microsoft Build Engine (MSBuild) usato da [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)].  
  
 Indipendentemente dal fatto che si preferisca ricompilare o reindirizzare l'applicazione, è necessario determinare se l'applicazione è interessata dalle modifiche introdotte in versioni successive di .NET Framework. Queste modifiche sono di due tipi:  
  
-   Le modifiche di interruzione che si verificano tra [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] e le versioni successive di .NET Framework.  
  
-   I tipi e i membri del tipo contrassegnati come deprecati o obsoleti tra [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] e le versioni successive di .NET Framework.  
  
 Se si reindirizza o si ricompila l'applicazione, è necessario rivedere sia le modifiche di interruzione e i tipi e i membri obsoleti per ogni versione di .NET Framework rilasciata dopo [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)].  
  
## <a name="breaking-changes"></a>Modifiche di interruzione  
 Quando si verifica una modifica di interruzione, in base alla modifica specifica, è possibile che sia disponibile una soluzione alternativa sia per le applicazioni reindirizzate che per le applicazioni ricompilate. In alcuni casi, è possibile aggiungere un elemento figlio all'elemento [\<runtime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) del file di configurazione dell'applicazione per ripristinare il comportamento precedente. Ad esempio, nel file di configurazione seguente viene ripristinato l'ordinamento della stringa e il comportamento del confronto utilizzato in [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)] che può essere utilizzato con un'applicazione reindirizzata o ricompilata.  
  
```xml  
<configuration>  
   <runtime>  
      <CompatSortNLSVersion enabled="4096"/>  
   </runtime>  
</configuration>  
```  
  
 Tuttavia, in alcuni casi, potrebbe essere necessario modificare il codice sorgente e ricompilare l'applicazione.  
  
 Per stimare l'impatto di possibili modifiche di interruzione sull'applicazione, è necessario rivedere i seguenti elenchi di modifiche:  
  
-   Modifiche ai documenti relative alle[Modifiche sostanziali in .NET Framework 2.0](http://go.microsoft.com/fwlink/?LinkId=125263) in [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)] che possono interessare un'applicazione destinata a [!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)].  
  
-   Modifiche ai documenti relative alle[Modifiche in .NET Framework 3.5 SP1](http://go.microsoft.com/fwlink/?LinkID=186989) tra [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)].  
  
-   Modifiche ai documenti relativi ai[Problemi di migrazione di .NET Framework 4](http://msdn.microsoft.com/library/ee941656\(v=vs.100\).aspx) tra [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)] e [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
## <a name="obsolete-types-and-members"></a>Tipi e membri obsoleti  
 L'impatto di tipi e membri deprecati è piuttosto diverso per le applicazioni reindirizzate e quelle ricompilate. L'utilizzo di tipi e membri obsoleti non influirà su un'applicazione reindirizzata a meno che il tipo o il membro obsoleto non siano stati fisicamente rimossi dall'assembly. La ricompilazione di un'applicazione che usa tipi o membri obsoleti di solito produce un avviso del compilatore piuttosto che un errore del compilatore. Tuttavia, in alcuni casi, produce un errore del compilatore e il codice che usa il tipo o il membro obsoleto non esegue correttamente la compilazione. In questo caso, è necessario riscrivere il codice sorgente che chiama il tipo o il membro obsoleto prima di ricompilare l'applicazione. Per altre informazioni sui tipi e sui membri obsoleti, vedere [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md).  
  
 Per stimare l'impatto di tipi e membri deprecati fin dalla versione di [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)], vedere [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md). Rivedere gli elenchi di tipi e membri obsoleti per [!INCLUDE[net_v20SP1_short](../../../includes/net-v20sp1-short-md.md)], [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].

