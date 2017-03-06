---
title: Common Language Runtime (CLR)
description: Common Language Runtime (CLR)
keywords: .NET, .NET Core
author: rpetrusha
ms.author: ronpet
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 7704d9c9-e5fa-4969-a423-081cce0e21e6
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: b789ed861a5df583162f901c1c5bc765c55f7b30
ms.lasthandoff: 03/02/2017

---

# <a name="common-language-runtime-clr"></a>Common Language Runtime (CLR)

In .NET Framework viene fornito un ambiente di runtime, denominato Common Language Runtime, in cui viene eseguito il codice e nel quale sono offerti servizi che facilitano il processo di sviluppo.

I compilatori e gli strumenti dei linguaggi espongono le funzionalità di Common Language Runtime e consentono di scrivere codice che sfrutta i vantaggi di tale ambiente di esecuzione gestito. Il codice sviluppato tramite un compilatore di linguaggio basato su Common Language Runtime viene definito codice gestito e si avvantaggia di funzionalità quali l'integrazione tra i linguaggi, la gestione delle eccezioni con linguaggi diversi, la sicurezza avanzata, il supporto per il controllo delle versioni e la distribuzione, un modello semplificato per l'interazione tra componenti e servizi di debug e di profilatura.

> [!NOTE]
> I compilatori e gli strumenti sono in grado di produrre un output che può essere usato da Common Language Runtime perché il sistema di tipi, il formato dei metadati e l'ambiente di runtime (il sistema di esecuzione virtuale) sono tutti definiti da uno standard pubblico, la specifica di ECMA Common Language Infrastructure. Per altre informazioni, vedere [ECMA C# and Common Language Infrastructure Standards](https://www.visualstudio.com/en-us/mt639507) (Specifiche ECMA C# e Common Language Infrastructure).

Per consentire all'ambiente di esecuzione di fornire servizi al codice gestito, è necessario che i compilatori di linguaggio generino metadati che descrivono i tipi, i membri e i riferimenti presenti nel codice. I metadati sono memorizzati con il codice: ogni file eseguibile trasportabile (PE, Portable Executable) caricabile in Common Language Runtime contiene metadati. I metadati vengono usati nell'ambiente di esecuzione per individuare e caricare classi, disporre istanze in memoria, risolvere chiamate di metodo, generare codice nativo, garantire sicurezza e impostare limiti di contesto per la fase di esecuzione.

Il layout degli oggetti e i riferimenti agli oggetti vengono gestiti automaticamente: quando non sono più in uso, gli oggetti vengono rilasciati. Gli oggetti la cui durata viene amministrata con queste modalità vengono denominati dati gestiti. La procedura di Garbage Collection consente di eliminare il rischio di perdite di memoria e di altri errori comuni di programmazione. Se si impiega codice gestito, è possibile usare nell'applicazione .NET Framework sia dati gestiti che dati non gestiti, anche simultaneamente. Dal momento che i compilatori di linguaggio forniscono autonomamente tipi, quali i tipi primitivi, è possibile che non sempre lo sviluppatore sappia, o abbia l'esigenza di sapere, se i dati che usa sono gestiti.

Common Language Runtime facilita la progettazione di componenti e applicazioni i cui oggetti interagiscano in contesti di linguaggi diversi. Oggetti scritti in linguaggi differenti possono infatti interagire e funzionare in modo strettamente integrato. Una volta definita una classe, ad esempio, è possibile usare un linguaggio differente per derivarne un'altra classe o per chiamarvi un metodo. È anche possibile passare l'istanza di una classe al metodo di una classe scritta in un linguaggio differente. Questa integrazione tra linguaggi è possibile perché i compilatori e gli strumenti dei linguaggi destinati alla fase di esecuzione usano un sistema di tipi comuni, definito dall'ambiente di esecuzione, e seguono le regole di tale ambiente per la definizione di nuovi tipi, oltre che per la creazione, l'utilizzo, il mantenimento e l'associazione a tipi.

In quanto parte dei rispettivi metadati, tutti i componenti gestiti contengono informazioni sui componenti e le risorse in base ai quali sono stati compilati. Il runtime usa tali informazioni per garantire la disponibilità delle versioni specificate del software necessario al funzionamento del componente o dell'applicazione, riducendo così il rischio di interruzioni del codice dovute all'irreperibilità di alcune dipendenze. Le informazioni sui tipi definiti e sulle relative dipendenze vengono invece archiviate con il codice sotto forma di metadati, semplificando così le attività di replica e rimozione dei componenti.

I compilatori e gli strumenti dei linguaggi sono progettati per esporre le funzionalità del runtime secondo modalità concepite per essere utili ed intuitive per gli sviluppatori. Alcune di queste funzionalità potrebbero quindi essere più evidenti in un ambiente operativo anziché in un altro. Il modo di percepire il funzionamento dell'ambiente di esecuzione dipende dai compilatori o dagli strumenti dei linguaggi usati. Il runtime offre i vantaggi seguenti: 

* Possibilità di utilizzare con facilità componenti sviluppati in altri linguaggi.

* La disponibilità dei tipi estensibili forniti da una libreria di classi.

* Funzionalità del linguaggio come ereditarietà, interfacce e overload per la programmazione orientata a oggetti.

* Supporto per il modello di threading Free esplicito che consente la creazione di applicazioni scalabili a thread multipli.

* Supporto per la gestione delle eccezioni strutturata.

* Supporto per gli attributi personalizzati.

* Garbage Collection.

* Utilizzo dei delegati invece dei puntatori a funzioni con conseguente miglioramento dell'indipendenza dai tipi e della sicurezza dei tipi.

## <a name="versions-of-the-common-language-runtime"></a>Versioni di Common Language Runtime

Il numero di versione di .NET Framework non corrisponde necessariamente al numero di versione di CLR inclusa. Nella tabella seguente viene mostrata la correlazione tra due numeri di versione. 

Versione di .NET Framework | Include la versione CLR 
---------------------- | --------------------
1.0 | 1.0
1.1 | 1.1
2.0 | 2.0
3.0 | 2.0
3.5 | 2.0
4 | 4
4.5 (incluse 4.5.1 e 4.5.2) | 4
4.6 (incluse 4.6.1 e 4.6.2) | 4

## <a name="see-also"></a>Vedere anche

[Gestione automatica della memoria](garbagecollection/index.md)

 


