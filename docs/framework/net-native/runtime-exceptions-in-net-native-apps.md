---
title: "Eccezioni di runtime in app .NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5f050181-8fdd-4a4e-9d16-f84c22a88a97
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Eccezioni di runtime in app .NET
È importante testare le build di versione dell'app della piattaforma UWP \(Universal Windows Platform\) nelle rispettive piattaforme di destinazione, perché le configurazioni di tipo Debug e di tipo Versione sono completamente diverse. Per impostazione predefinita, la configurazione di tipo Debug usa il runtime di .NET Core per compilare l'app, mentre quella di tipo Versione usa .NET Native per compilare l'app nel codice nativo.  
  
> [!IMPORTANT]
>  Per informazioni sulla gestione delle eccezioni [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md), [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md) e [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) che possono verificarsi durante il test delle versioni finali dell'app, vedere "Passaggio 4: Passaggio 4: Risolvere manualmente i metadati mancanti" nell'argomento [Introduzione](../../../docs/framework/net-native/getting-started-with-net-native.md), nonché [Reflection e .NET Native](../../../docs/framework/net-native/reflection-and-net-native.md) e [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  
  
## Build di tipo Debug e Versione  
 La build di tipo Debug eseguita nel runtime .NET Core non è stata compilata nel codice nativo. In questo modo tutti i servizi normalmente forniti dal runtime sono disponibili per l'app.  
  
 La build di versione viene invece compilata nel codice nativo per le rispettive piattaforme di destinazione, rimuove la maggior parte delle dipendenze da librerie e runtime esterni, oltre a ottimizzare notevolmente il codice garantendo prestazioni ottimali.  
  
 Quando si esegue il debug di build di tipo Versione compilate con .NET Native:  
  
-   Si usa il motore di debug di .NET Native, che è diverso rispetto ai normali strumenti di debug di .NET.  
  
-   Le dimensioni del file eseguibile vengono ridotte il più possibile. Uno dei modi in cui .NET Native riesce a ridurre le dimensioni del file eseguibile consiste nel tagliare significativamente i messaggi di eccezione di runtime, come descritto in maggiore dettaglio nella sezione [Messaggi di eccezione di runtime](#Messages).  
  
-   Il codice viene notevolmente ottimizzato. Questo significa che laddove possibile viene usato l'incorporamento, che sposta il codice dalle routine esterne in quella chiamante.   Il fatto che .NET Native fornisca un runtime specializzato e implementi massicciamente l'incorporamento influisce sullo stack di chiamate visualizzato durante il debug.  Per altre informazioni, vedere la sezione [Stack di chiamate del runtime](#CallStack).  
  
> [!NOTE]
>  Per controllare se le build di tipo Debug e Versione sono compilate con la catena di strumenti .NET Native, selezionare o deselezionare la casella **Compilare con la catena di strumenti .NET Native**. Notare però che per la compilazione della versione di produzione dell'app, Windows Store userà sempre la catena di strumenti .NET Native.  
  
<a name="Messages"></a>   
## Messaggi di eccezione di runtime  
 Per ridurre al minimo le dimensioni dei file eseguibili delle applicazioni, .NET Native non include il testo completo dei messaggi di eccezione. Di conseguenza, è possibile che i messaggi delle eccezioni di runtime generate nelle build di tipo Versione non includano il testo completo, ma solo una sottostringa e un collegamento da aprire per visualizzare altre informazioni. Le informazioni visualizzate sull'eccezione possono ad esempio essere simili a:  
  
```  
  
Exception thrown: '$16_System.AggregateException' in Unknown Module. Additional information: AggregateException_ctor_DefaultMessage If there is a handler for this exception, the program may be safely continued.  
  
```  
  
 Per visualizzare il messaggio di eccezione completo, eseguire la build di tipo Debug. Ad esempio le informazioni sull'eccezione precedente della build di tipo Versione sono simili alle seguenti nella build di tipo Debug:  
  
```  
  
Exception thrown: 'System.AggregateException' in NativeApp.exe. Additional information: Value does not fall within the expected range.  
  
```  
  
<a name="CallStack"></a>   
## Stack di chiamate del runtime  
 A causa dell'incorporamento e di altre ottimizzazioni, lo stack di chiamate visualizzato da un'app compilata con la catena di strumenti .NET Native potrebbe risultare poco utile per identificare chiaramente il percorso di un'eccezione di runtime.  
  
 Per ottenere lo stack completo, eseguire la build di tipo Debug.  
  
## Vedere anche  
 [Debug di app universali di Windows .NET Native](http://blogs.msdn.com/b/visualstudioalm/archive/2015/07/29/debugging-net-native-windows-universal-apps.aspx)   
 [Introduzione](../../../docs/framework/net-native/getting-started-with-net-native.md)