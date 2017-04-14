---
title: "Compatibilit&#224; tra le versioni in .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework 4.5, Compatibilità con le versioni precedenti"
  - "versioni di .NET Framework, compatibilità"
  - ".NET Framework, compatibilità tra versioni"
ms.assetid: 2f25e522-456a-48c3-8a53-e5f39275649f
caps.latest.revision: 35
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 30
---
# Compatibilit&#224; tra le versioni in .NET Framework
Per compatibilità con le versioni precedenti si intende che un'app sviluppata per una particolare versione di una piattaforma sarà eseguita su versioni successive di quella piattaforma.  .NET Framework tenta di ottimizzare la compatibilità con le versioni precedenti: il codice sorgente scritto per una versione di .NET Framework deve essere compilato su versioni successive di .NET Framework e i file binari in esecuzione su una versione di .NET Framework devono comportarsi in modo analogo nelle versioni successive di .NET Framework.  
  
<a name="Apps"></a>   
## Compatibilità tra le versioni per app  
 Per impostazione predefinita, un'app viene eseguita sulla versione di .NET Framework per cui è stata creata.  Se la versione specifica non è presente e il file di configurazione dell'app non definisce le versioni supportate, potrebbe verificarsi un errore di inizializzazione di .NET Framework.  In questo caso, il tentativo di esecuzione dell'app avrà esito negativo.  
  
 Per definire le versioni specifiche in cui viene eseguita l'app, aggiungere uno o più elementi [\<supportedRuntime\>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) al file di configurazione dell'app.  Ogni elemento `<supportedRuntime>` elenca una versione supportata del runtime, con il primo che specifica la versione preferita e l'ultimo che specifica l'ultima versione nell'elenco delle preferenze.  Per altre informazioni, vedere [Procedura: configurare un'applicazione per supportare .NET Framework 4 o 4.5](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md).  
  
## Compatibilità tra le versioni per componenti  
 Un'app è in grado di controllare la versione di .NET Framework in cui viene eseguita, diversamente da un componente.  I componenti e le librerie di classi vengono caricati nel contesto di un'app specifica e pertanto vengono eseguiti automaticamente nella versione di .NET Framework in cui è in esecuzione l'app.  
  
 A causa di questa restrizione, le garanzie di compatibilità sono particolarmente importanti per i componenti.  A partire da .NET Framework 4, è possibile specificare il livello di compatibilità di un componente in più versioni applicando l'attributo <xref:System.Runtime.Versioning.ComponentGuaranteesAttribute?displayProperty=fullName> a tale componente.  Gli strumenti possono usare questo attributo per rilevare le possibili violazioni della garanzia di compatibilità in versioni future di un componente.  
  
## Compatibilità con le versioni precedenti e .NET Framework 4.5  
 .NET Framework 4.5 e le versioni intermedie sono compatibili con le versioni precedenti delle app create con le versioni precedenti di .NET Framework.  In altre parole, le app e i componenti creati con le versioni precedenti funzioneranno senza applicare alcuna modifica in .NET Framework 4.5.  Tuttavia, per impostazione predefinita, le app vengono eseguite sulla versione di Common Language Runtime per la quale sono state sviluppate, pertanto potrebbe essere necessario fornire un file di configurazione per far sì che l'app venga eseguita in .NET Framework 4.5.  Per altre informazioni, vedere la sezione [Compatibilità tra le versioni per app](#Apps) in questo articolo.  
  
 In pratica, questa compatibilità può essere interrotta da modifiche apparentemente irrilevanti in .NET Framework e nelle tecniche di programmazione.  Ad esempio, i miglioramenti nelle prestazioni in .NET Framework 4 possono esporre una race condition che non si era verificata nelle versioni precedenti.  Allo stesso modo, l'utilizzo di un percorso hardcoded per gli assembly .NET Framework, l'esecuzione di un confronto delle uguaglianze con una particolare versione di .NET Framework e l'acquisizione del valore di un campo privato tramite reflection non sono pratiche compatibili con le versioni precedenti.  Inoltre, ogni versione di .NET Framework include correzioni di bug e modifiche correlate alla sicurezza che possono incidere sulla compatibilità di alcune app e componenti.  
  
 Se l'app o il componente non funziona come previsto in .NET Framework 4.5, 4.5.1, 4.5.2 o 4.6, usare i seguenti elenchi di controllo.  
  
-   Controllare questi argomenti per qualsiasi modifica che potrebbe interessare l'app e applicare la soluzione alternativa descritta.  
  
    -   [Problemi relativi alla migrazione di .NET Framework 4](http://go.microsoft.com/fwlink/p/?LinkId=248212)  
  
    -   [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)  
  
    -   [Compatibilità delle applicazioni nella versione 4.5.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-1.md)  
  
    -   [Compatibilità delle applicazioni nella versione 4.5.2](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)  
  
    -   [Compatibilità delle applicazioni nella versione 4.6](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6.md)  
  
-   Se si dispone di un'app .NET Framework 1.1, consultare anche gli argomenti seguenti:  
  
    -   [Modifiche importanti apportate in .NET Framework 2.0](http://go.microsoft.com/fwlink/?LinkID=125263)  
  
    -   [Modifiche apportate in .NET Framework 3.5 SP1](http://go.microsoft.com/fwlink/?LinkId=186989)  
  
-   Se si esegue la ricompilazione del codice sorgente esistente per l'esecuzione in .NET Framework 4.5 o si sviluppa una nuova versione di un'app o di un componente destinato alla versione 4.5 da una codebase sorgente esistente, vedere [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md) per i tipi e i membri obsoleti e applicare la soluzione alternativa descritta.  \(Il codice compilato precedentemente continuerà a essere in esecuzione sui tipi e i membri contrassegnati come obsoleti\).  
  
-   Se si determina che una modifica in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] ha interrotto l'app, vedere [Schema delle impostazioni dell'ambiente di esecuzione](../../../docs/framework/configure-apps/file-schema/runtime/index.md) per stabilire se è possibile usare un'impostazione di runtime nel file di configurazione dell'app per ripristinare il comportamento precedente.  
  
-   Se si rileva un problema non documentato, segnalare un bug [Microsoft Connect](http://go.microsoft.com/fwlink/?LinkID=154815) e scrivere un messaggio all'indirizzo [netfxcf@microsoft.com](mailto:netfxcf@microsoft.com) con il numero del bug.  
  
## Compatibilità ed esecuzione affiancata  
 Se non si riesce a trovare una soluzione alternativa adatta al problema, ricordare che .NET Framework 4.5 viene eseguito affiancato con le versioni 1.1, 2.0 e 3.5 ed è un aggiornamento sul posto che sostituisce la versione 4.  Per app destinate alle versioni 1.1, 2.0 e 3.5, è possibile installare la versione appropriata di .NET Framework nel computer di destinazione per eseguire l'app nell'ambiente migliore.  Per altre informazioni sull'esecuzione side\-by\-side, vedere [Esecuzione affiancata di diverse versioni](../../../docs/framework/deployment/side-by-side-execution.md).  
  
## Vedere anche  
 [Novità](../../../docs/framework/whats-new/index.md)   
 [Elementi obsoleti nella libreria di classi](../../../docs/framework/whats-new/whats-obsolete.md)   
 [Compatibilità delle applicazioni](../../../docs/framework/migration-guide/application-compatibility.md)   
 [Criteri relativi al ciclo di vita del supporto Microsoft .NET Framework](http://go.microsoft.com/fwlink/p/?LinkId=248212)   
 [Problemi di migrazione di .NET Framework 4](http://go.microsoft.com/fwlink/p/?LinkId=248212)