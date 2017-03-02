---
title: Principi fondamentali di Garbage Collection
description: Principi fondamentali di Garbage Collection
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 08/16/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 9d5fce64-95a4-4609-8eee-b0ac70078cdb
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 02b0311559071147b38182076f60918b7351cc63
ms.lasthandoff: 03/02/2017

---

# <a name="fundamentals-of-garbage-collection"></a>Principi fondamentali di Garbage Collection

In Common Language Runtime (CLR), Garbage Collector funge da gestore di memoria automatico, offrendo i seguenti vantaggi:

* Consente di sviluppare un'applicazione senza alcun bisogno di liberare memoria. 

* Alloca gli oggetti nell'heap gestito in maniera efficiente. 

* Recupera gli oggetti inutilizzati, ne cancella la memoria e tiene la memoria a disposizione per le future allocazioni. Gli oggetti gestiti ottengono automaticamente contenuto pulito con il quale iniziare, pertanto i costruttori non devono inizializzare ogni campo dati.

* Garantisce protezione per la memoria assicurando che un oggetto non possa usare il contenuto di un altro oggetto.


In questo argomento vengono descritti i concetti principali di Garbage Collection. Include le sezioni seguenti:

* [Nozioni fondamentali sulla memoria](#fundamentals-of-memory)

* [Condizioni per un'operazione di Garbage Collection](#conditions-for-a-garbage-collection)

* [Heap gestito](#the-managed-heap)

* [Generazioni](#generations)

* [Fasi di un'operazione di Garbage Collection](#what-happens-during-a-garbage-collection)

* [Modifica delle risorse non gestite](#manipulating-unmanaged-resources)

## <a name="fundamentals-of-memory"></a>Nozioni fondamentali sulla memoria

Nell'elenco seguente sono riepilogati concetti importanti relativi alla memoria CLR.

* Ogni processo dispone di un proprio spazio degli indirizzi virtuali distinto. Tutti i processi nello stesso computer condividono la stessa memoria fisica e condividono il file di paging, se presente.

* Per impostazione predefinita, nei computer a 32 bit ogni processo dispone di uno spazio degli indirizzi virtuali in modalità utente da 2 GB.

* Uno sviluppatore di applicazioni usa solo lo spazio degli indirizzi virtuali e non modifica mai direttamente la memoria fisica. Il Garbage Collector alloca e libera automaticamente la memoria virtuale nell'heap gestito.

* La memoria virtuale può trovarsi in tre stati: 

    * Libero. Non vi sono riferimenti al blocco di memoria, che è disponibile per l'allocazione.

    * Riservato. Il blocco di memoria è disponibile per l'utilizzo e non può essere usato da un'altra richiesta di allocazione. Non è tuttavia possibile archiviare i dati in questo blocco di memoria fino a quando non viene eseguito il commit. 

    * Eseguito. Il blocco di memoria è assegnato all'archiviazione fisica.

* Lo spazio degli indirizzi virtuali può diventare frammentato. Ciò significa che sono presenti blocchi liberi, noti anche come buchi, nello spazio degli indirizzi. Quando viene richiesta un'allocazione della memoria virtuale, il gestore di memoria virtuale deve trovare un singolo blocco libero con dimensioni sufficienti per soddisfare la richiesta di allocazione. Anche se si dispone di 2 GB di spazio disponibile, l'allocazione che richiede 2 GB avrà esito negativo a meno che tutto lo spazio si trovi in un unico blocco di indirizzi.

* È possibile esaurire la memoria se si esaurisce lo spazio degli indirizzi virtuali da riservare o lo spazio fisico di cui eseguire il commit.

Il file di paging viene usato anche se la pressione della memoria fisica (ovvero, la richiesta di memoria fisica) è bassa. La prima volta che la pressione della memoria fisica è elevata, il sistema operativo deve fare spazio nella memoria fisica per archiviare i dati ed esegue il backup di alcuni dei dati che si trovano nella memoria fisica nel file di paging. Il paging dei dati non viene eseguito fino a quando non è necessario, pertanto è possibile riscontrare il paging in situazioni in cui la pressione della memoria fisica è molto bassa.

## <a name="conditions-for-a-garbage-collection"></a>Condizioni per un'operazione di Garbage Collection

Le operazioni di Garbage Collection vengono eseguite in presenza di una delle seguenti condizioni:

* La memoria fisica del sistema è insufficiente.

* La memoria usata dagli oggetti allocati nell'heap gestito supera una soglia accettabile. Questa soglia viene continuamente modificata durante l'esecuzione del processo.

* Viene chiamato il metodo [GC.Collect](xref:System.GC.Collect). Nella quasi totalità dei casi non è necessario chiamare questo metodo, in quanto il Garbage Collector viene eseguito senza interruzioni. Il metodo viene usato principalmente in situazioni eccezionali e per scopi di test. 

## <a name="the-managed-heap"></a>Heap gestito

Dopo essere stato inizializzato da CLR, il Garbage Collector alloca un segmento di memoria per archiviare e gestire oggetti. Questa memoria è definita heap gestito, in contrapposizione a un heap nativo presente nel sistema operativo. 

Per ogni processo gestito esiste un heap gestito. Tutti i thread nel processo allocano memoria per gli oggetti sullo stesso heap.

> [!IMPORTANT]
> La dimensione dei segmenti allocati dal Garbage Collector è specifica dell'implementazione ed è soggetta a modifiche in qualsiasi momento, tra cui aggiornamenti periodici. L'applicazione non deve dare per scontata o dipendere da una particolare dimensione del segmento, né provare a configurare la quantità di memoria disponibile per le allocazioni di segmenti. 
 
Minore è il numero di oggetti allocati nell'heap, minore sarà il lavoro del Garbage Collector. Quando si allocano oggetti, non usare valori arrotondati per eccesso che superino le proprie esigenze, ad esempio non allocare una matrice di 32 byte se sono necessari solo 15 byte. 

Quando viene attivata un'operazione di Garbage Collection, il Garbage Collector recupera la memoria occupata dagli oggetti inutilizzati. Durante il processo di recupero, gli oggetti attivi vengono compattati in modo da poter essere spostati insieme e lo spazio inutilizzato viene rimosso, riducendo le dimensioni dell'heap. In questo modo si garantisce che gli oggetti allocati insieme restino uniti nell'heap gestito, preservandone la vicinanza.

L'impatto (frequenza e durata) delle operazioni di Garbage Collection è il risultato del volume di allocazioni e della quantità di memoria esclusa nell'heap gestito. 

L'heap può essere considerato l'insieme di due heap: l'heap degli oggetti grandi e l'heap degli oggetti piccoli. 

L'heap oggetti grandi contiene oggetti di dimensioni pari o superiori a 85.000 byte. Gli oggetti sull'heap oggetti grandi sono in genere matrici. È raro che un oggetto istanza sia particolarmente grande. 

## <a name="generations"></a>Generazioni

L'heap è organizzato in generazioni, così da poter gestire oggetti di lunga durata e di breve durata. Durante un'operazione di Garbage Collection vengono recuperati per primi gli oggetti di breve durata, che in genere occupano solo una piccola parte dell'heap. Esistono tre generazioni di oggetti nell'heap: 

* **Generazione 0.** È la generazione più recente e contiene oggetti di breve durata. Un esempio di oggetto di breve durata è una variabile temporanea. Le operazioni di Garbage Collection vengono eseguite il più delle volte in questa generazione. 

  Gli oggetti appena allocati formano una nuova generazione di oggetti e sono implicitamente raccolte di generazione 0, a meno che non siano oggetti grandi, nel qual caso vengono inseriti nell'heap degli oggetti grandi in una raccolta di generazione 2.

  Gran parte degli oggetti vengono recuperati tramite Garbage Collection nella generazione 0 e non passano alla generazione successiva. 

* **Generazione 1.** Questa generazione contiene oggetti di breve durata e funge da buffer tra gli oggetti di breve durata e gli oggetti di lunga durata. 

* **Generazione 2.** Questa generazione contiene oggetti di lunga durata. Un esempio di oggetto di lunga durata è un oggetto in un'applicazione server contenente dati statici che restano attivi per la durata del processo.

Le operazioni di Garbage Collection vengono eseguite in generazioni specifiche a seconda delle condizioni. Raccogliere una generazione significa raccogliere gli oggetti in quella generazione e in tutte le generazioni più recenti. Un'operazione di Garbage Collection di generazione 2 viene definita completa, in quanto recupera tutti gli oggetti in tutte le generazioni, vale a dire tutti gli oggetti nell'heap gestito.

### <a name="survival-and-promotions"></a>Esclusione e promozioni

Gli oggetti che non vengono recuperati durante un'operazione di Garbage Collection sono definiti oggetti esclusi e vengono promossi alla generazione successiva. Gli oggetti esclusi da un'operazione di Garbage Collection di generazione 0 vengono promossi alla generazione 1; gli oggetti esclusi da un'operazione di Garbage Collection di generazione 1 vengono promossi alla generazione 2; gli oggetti esclusi da un'operazione di Garbage Collection di generazione 2 restano nella generazione 2.

Quando il Garbage Collector rileva un tasso di esclusione elevato in una generazione, aumenta la relativa soglia delle allocazioni, in modo che la raccolta successiva generi un recupero di memoria sostanziale. CLR bilancia continuamente due priorità: impedire che il working set di un'applicazione diventi troppo grande e limitare la durata delle operazioni di Garbage Collection.

### <a name="ephemeral-generations-and-segments"></a>Generazioni e segmenti temporanei

Poiché gli oggetti nelle generazioni 0 e 1 sono di breve durata, queste vengono definite generazioni temporanee. 

Le generazioni temporanee devono essere allocate nel segmento di memoria noto come segmento temporaneo. Ogni nuovo segmento acquisito dal Garbage Collector diventa il nuovo segmento temporaneo e contiene gli oggetti esclusi da un'operazione di Garbage Collection di generazione 0. Il segmento temporaneo precedente diventa il nuovo segmento di generazione 2. 


Il segmento temporaneo può includere oggetti di generazione 2, i quali possono usare più segmenti (nella misura richiesta dal processo e consentita dalla memoria). 

La quantità di memoria liberata da un'operazione di Garbage Collection temporanea è limitata alla dimensione del segmento temporaneo. Tale quantità di memoria è proporzionale allo spazio occupato dagli oggetti inutilizzati.

## <a name="what-happens-during-a-garbage-collection"></a>Fasi di un'operazione di Garbage Collection

Un'operazione di Garbage Collection si compone delle seguenti fasi: 

* Una fase di contrassegno in cui vengono individuati tutti gli oggetti attivi e ne viene creato un elenco.

* Una fase di rilocazione in cui vengono aggiornati i riferimenti agli oggetti che saranno compattati. 

* Una fase di compattazione in cui lo spazio occupato dagli oggetti inutilizzati viene recuperato e gli oggetti esclusi compattati. Durante questa fase, gli oggetti rimasti dopo un'operazione di Garbage Collection vengono spostati verso l'estremità meno recente del segmento. 

Poiché le raccolte di generazione 2 possono occupare più segmenti, gli oggetti promossi alla generazione 2 possono essere spostati in un segmento meno recente. Gli oggetti esclusi di generazione 1 e 2 possono essere spostati in un segmento diverso, in quanto vengono promossi alla generazione 2. 

L'heap oggetti grandi non viene in genere compresso perché la copia di oggetti grandi impone un calo delle prestazioni. Tuttavia, è possibile usare la proprietà [GCSettings.LargeObjectHeapCompactionMode](xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode) per comprimere su richiesta l'heap oggetti grandi. 

Per stabilire se gli oggetti sono attivi, il Garbage Collector usa le seguenti informazioni: 

* **Radici dello stack.** Variabili dello stack fornite dal compilatore JIT e dal percorso di chiamate nello stack.

* **Handle di Garbage Collection.** Handle che puntano agli oggetti gestiti e che possono essere allocati mediante codice utente o Common Language Runtime.

* **Dati statici.** Oggetti statici nei domini applicazione che possono fare riferimento ad altri oggetti. Ogni dominio applicazione tiene traccia dei rispettivi oggetti statici.

Prima di eseguire un'operazione di Garbage Collection, tutti i thread gestiti vengono sospesi, eccetto il thread che attiva l'operazione.

Nell'illustrazione seguente viene illustrato un thread che attiva un'operazione di Garbage Collection causando la sospensione degli altri thread.

![Quando un thread attiva un'operazione di Garbage Collection](./media/fundamentals/393001.png)

Thread che attiva un'operazione di Garbage Collection

## <a name="manipulating-unmanaged-resources"></a>Modifica delle risorse non gestite

Se gli oggetti gestiti fanno riferimento a oggetti non gestiti tramite i relativi handle di file nativi, è necessario liberare in modo esplicito gli oggetti non gestiti, poiché il Garbage Collector tiene traccia della memoria solo sull'heap gestito.

È possibile che gli utenti dell'oggetto gestito non eliminino le risorse native usate dall'oggetto. Per eseguire la pulizia, è possibile rendere l'oggetto gestito finalizzabile. La finalizzazione consiste in azioni di pulizia che si eseguono quando l'oggetto non è più usato. Quando l'oggetto gestito cessa di essere usato, esegue azioni di pulizia specificate nel metodo del relativo finalizzatore.

Quando viene individuato un oggetto finalizzabile inutilizzato, il relativo finalizzatore viene inserito in una coda in modo che vengano eseguite le azioni di pulizia, mentre l'oggetto stesso viene promosso alla generazione successiva. Sarà pertanto necessario attendere l'operazione di Garbage Collection successiva eseguita in tale generazione, che non sarà necessariamente l'operazione immediatamente successiva, per stabilire se l'oggetto è stato recuperato.

## <a name="see-also"></a>Vedere anche

[Garbage Collection in .NET](gc.md)

