---
title: Introduzione agli eventi
description: Introduzione agli eventi
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 9b8d2a00-1584-4a5b-8994-5003d54d8e0c
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a2eb8daef0883b78769a185be7d64e43c88b1d15
ms.lasthandoff: 03/13/2017

---

# <a name="introduction-to-events"></a>Introduzione agli eventi

[Precedente](delegates-patterns.md)

Analogamente ai delegati, gli eventi sono un meccanismo di *associazione tardiva*. In effetti, gli eventi hanno alla base il supporto del linguaggio per i delegati.

Gli eventi rappresentano il modo in cui un oggetto comunica a tutti i componenti del sistema interessati che è avvenuto qualcosa. Qualsiasi altro componente può sottoscrivere l'evento e ricevere una notifica quando tale evento viene generato.

Probabilmente in altri programmi creati in passato gli eventi sono già stati usati. Molti sistemi grafici dispongono di un modello di eventi per segnalare l'interazione dell'utente. Questi eventi segnalano il movimento del mouse, la pressione di pulsanti e interazioni analoghe. Questo è uno degli scenari più comuni di uso degli eventi, ma sicuramente non l'unico.

È possibile definire gli eventi che devono essere generati per le classi. Una considerazione importante per l'uso degli eventi è che per un evento specifico potrebbe non essere registrato alcun oggetto. È necessario scrivere il codice in modo che vengano generati eventi solo se è configurato un listener.

La sottoscrizione di un evento crea anche un accoppiamento tra due oggetti, l'origine evento e il sink di evento. È necessario assicurarsi che il sink di evento annulli la sottoscrizione dall'origine evento quando non è più interessato agli eventi.

## <a name="design-goals-for-event-support"></a>Obiettivi di progettazione per il supporto degli eventi

Per quanto riguarda gli eventi, la progettazione di un linguaggio deve avere gli obiettivi seguenti.

Prima di tutto consentire il minimo accoppiamento possibile tra un'origine evento e un sink di evento. È possibile che questi due componenti non siano stati scritti dalla stessa organizzazione. È persino possibile che l'aggiornamento di questi componenti avvenga secondo pianificazioni completamente diverse.

In secondo luogo, la sottoscrizione di un evento e l'annullamento di tale sottoscrizione devono essere molto semplici.

Infine, le origini evento devono supportare più sottoscrittori di eventi, nonché la completa mancanza di sottoscrittori associati.

Come si può notare, gli obiettivi per gli eventi sono molto simili agli obiettivi per i delegati.
Ecco perché il supporto del linguaggio per gli eventi si basa sul supporto del linguaggio per i delegati.

## <a name="language-support-for-events"></a>Supporto del linguaggio per gli eventi

La sintassi per la definizione di eventi e la sottoscrizione o l'annullamento della sottoscrizione di eventi è un'estensione della sintassi per i delegati.

Per definire un evento si usa la parola chiave `event`:

```csharp
public event EventHandler<FileListArgs> Progress;
```

Il tipo di evento (`EventHandler<FileListArgs>` in questo esempio) deve essere un tipo di delegato. Quando si dichiara un evento, è necessario seguire un certo numero di convenzioni. In genere, il tipo di delegato di un evento restituisce void.
Le dichiarazioni di eventi devono essere un verbo o una frase verbale.
Usare il passato (come in questo esempio) quando l'evento segnala qualcosa che si è verificato. Usare il presente (ad esempio, `Closing`) per segnalare qualcosa che sta per verificarsi. L'uso del presente indica spesso che la classe supporta un determinato tipo di comportamento di personalizzazione. Uno degli scenari più comuni riguarda il supporto dell'annullamento. Un evento `Closing`, ad esempio, può includere un argomento che indica se l'operazione di chiusura deve continuare o meno.  Altri scenari possono consentire ai chiamanti di modificare il comportamento tramite l'aggiornamento delle proprietà degli argomenti dell'evento. È possibile generare un evento per proporre l'azione successiva che un algoritmo deve eseguire. Il gestore eventi può imporre un'azione diversa modificando le proprietà dell'argomento dell'evento.

Quando si vuole generare l'evento, è possibile chiamare i gestori eventi tramite la sintassi di chiamata dei delegati:

```csharp
Progress?.Invoke(this, new FileListArgs(file));
```

Come descritto nella sezione sui [delegati](delegates-patterns.md), l'operatore ?.
assicura in modo semplice che non venga generato un evento se questo non ha sottoscrittori.
 
Per sottoscrivere un evento si usa l'operatore `+=`:

```csharp
EventHandler<FileListArgs> onProgress = (sender, eventArgs) => 
    Console.WriteLine(eventArgs.FoundFile);
lister.Progress += OnProgress;
```

Il metodo del gestore, in genere, corrisponde al prefisso 'On' seguito dal nome dell'evento, come illustrato in precedenza.

Per annullare la sottoscrizione si usa l'operatore `-=`:

```csharp
lister.Progress -= onProgress;
```

È importante notare che per l'espressione che rappresenta il gestore eventi è stata dichiarata una variabile locale. Questo garantisce che l'annullamento della sottoscrizione rimuova il gestore.
Se invece si usa il corpo dell'espressione lambda, si tenta di rimuovere un gestore che non è mai stato associato e non viene quindi eseguita alcuna operazione.

Il prossimo articolo offre altre informazioni sui criteri tipici degli eventi, oltre a diverse varianti di questo esempio.

[Successivo](event-pattern.md)

