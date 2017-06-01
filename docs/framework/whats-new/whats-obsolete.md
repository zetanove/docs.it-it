---
title: Elementi obsoleti nella libreria di classi .NET Framework | Microsoft Docs
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
- obsolete [.NET Framework]
- what's obsolete [.NET Framework]
- deprecated [.NET Framework]
ms.assetid: d356a43a-73df-4ae2-a457-b9628074c7cd
caps.latest.revision: 19
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 68c71e26ac5e5a1872ac006d02adec84c1fb63da
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="what39s-obsolete-in-the-net-framework-class-library"></a>Elementi obsoleti nella libreria di classi .NET Framework
.NET Framework cambia nel corso del tempo. In ogni nuova versione vengono aggiunti nuovi tipi e membri dei tipi che forniscono nuove funzionalità. Anche i tipi esistenti e i relativi membri cambiano nel tempo. Alcuni tipi, ad esempio, perdono di importanza in quanto la tecnologia che supportano viene sostituita da una nuova tecnologia, e alcuni metodi vengono sostituiti da altri più nuovi che sono più adatti o più completi in termini di funzionalità.  
  
 Sia in .NET Framework sia in Common Language Runtime si cerca di supportare la compatibilità con le versioni precedenti, grazie alla quale le applicazioni sviluppate con una versione di .NET Framework possono essere eseguite nella versione di .NET Framework successiva. Ciò rende difficile la semplice rimozione di un tipo o di un membro del tipo. Per ovviare a questa difficoltà, si indica che un tipo o un membro del tipo non deve più essere usato contrassegnandolo come obsoleto o deprecato. La deprecazione di un tipo o di un membro ne implica il contrassegno, in modo che gli sviluppatori sappiano che verrà rimosso e abbiano il tempo di rispondere a tale rimozione. Tuttavia, il codice esistente che usa il tipo o il membro continua a essere eseguito nella nuova versione di .NET Framework.  
  
> [!NOTE]
>  Se applicati ai tipi e ai membri di .NET Framework, i termini *obsoleto* e *deprecato* hanno lo stesso significato.  
  
## <a name="the-obsoleteattribute-attribute"></a>Attributo ObsoleteAttribute  
 .NET Framework indica che un tipo o un membro di tipo è obsoleto contrassegnandolo con l'attributo <xref:System.ObsoleteAttribute>. L'applicazione dell'attributo a un tipo o un membro indica che quel tipo o membro sarà rimosso nelle versioni future di .NET Framework, senza causare interruzioni nel codice compilato che lo usa.  
  
 Oltre a indicare che un tipo o un membro di tipo è obsoleto, <xref:System.ObsoleteAttribute> definisce il modo in cui il compilatore gestisce il codice sorgente che include il tipo o il membro. Il compilatore può compilare il codice generando però un messaggio di avviso oppure può considerare l'uso del tipo o membro come un errore. Nel primo caso, il codice può essere compilato correttamente, ma un messaggio di avviso indica che il tipo o membro è obsoleto. Nel secondo caso, la compilazione non riesce.  
  
 Anche se la compilazione produce un errore anziché un messaggio di avviso, <xref:System.ObsoleteAttribute> non influisce sul comportamento in fase di esecuzione. In altre parole, le applicazioni che usano il tipo o membro e che sono state compilate correttamente verranno sempre eseguite correttamente. Soltanto il tentativo di ricompilare un'applicazione che usa il tipo o membro avrà esito negativo.  
  
## <a name="how-to-handle-obsolete-types-and-members"></a>Come gestire tipi e membri obsoleti  
 Quando si aggiorna e si ricompila il codice esistente, l'uso di un tipo o membro obsoleto che genera un avviso del compilatore nell'applicazione è perfettamente accettabile. Tuttavia, è consigliabile rivedere il messaggio di avviso del compilatore per stabilire se sia opportuno modificare il codice dell'applicazione. Se il messaggio non indica un'alternativa adatta, adottare una delle soluzioni seguenti:  
  
-   Modificare il codice rimuovendo l'uso del tipo o membro, se possibile.  
  
     -oppure-  
  
-   Rivedere la documentazione di quest'area tecnologica per stabilire come rispondere a questa deprecazione.  
  
 Si può scegliere di non ricompilare il codice esistente con una versione successiva di .NET Framework. È possibile invece specificare la versione di .NET Framework con la quale eseguire il codice compilato esistente. Si supponga ad esempio di avere un'applicazione denominata app1.exe, compilata con [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)], e di voler eseguire l'applicazione in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]. La procedura da adottare è la seguente:  
  
1.  Creare un file di configurazione per l'eseguibile principale e denominarlo *NomeApp*.exe.config, dove *NomeApp* è il nome dell'eseguibile dell'applicazione. Nel caso dell'applicazione denominata app1.exe dell'esempio, il nome del file di configurazione da creare sarebbe app1.exe.config.  
  
2.  Aggiungere il codice seguente al file di configurazione.  
  
    ```xml  
    <configuration>  
       <startup>   
          <supportedRuntime version="v4.0" />  
       </startup>  
    </configuration>  
    ```  
  
 La tabella seguente elenca i valori di stringa che è possibile assegnare all'attributo `version` per scegliere come destinazione una versione di .NET Framework specifica.  
  
|Versione di .NET Framework|Stringa `version`|
|-|-|  
|4.7|v4.0|  
|4.6 (incluse 4.6.1 e 4.6.2)|v4.0|  
|4.5 (incluse 4.5.1 e 4.5.2)|v4.0|  
|4|v4.0|  
|3.5|v2.0.50727|  
|2.0|v2.0.50727|  
|1.1|v1.1.4322|  
|1.0|v1.0.3705|  
  
## <a name="obsolete-lists-for-the-net-framework-45-and-46"></a>Elenchi degli elementi obsoleti per .NET Framework 4.5 e 4.6  
 [Tipi obsoleti](../../../docs/framework/whats-new/obsolete-types.md)  
  
 [Membri obsoleti](../../../docs/framework/whats-new/obsolete-members.md)  
  
## <a name="obsolete-lists-for-previous-versions"></a>Elenchi di elementi obsoleti per le versioni precedenti  
 [Tipi obsoleti in .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=224224)  
  
 [Membri obsoleti in .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=224227)  
  
 [Elenco degli elementi obsoleti di .NET Framework 3.5](http://go.microsoft.com/fwlink/?LinkId=163710)  
  
 [Elenco degli elementi obsoleti di .NET Framework 2.0](http://go.microsoft.com/fwlink/?LinkID=125264)  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento \<supportedRuntime>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)
