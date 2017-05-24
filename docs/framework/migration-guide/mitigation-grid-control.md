---
title: 'Mitigazione: Allocazione dello spazio di controllo della griglia alle colonne a stella | Documenti di Microsoft'
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes
- .NET Framework 4.7 retargeting changes
- WPF retargeting changes
- Grid control retargeting changes
ms.assetid: 707c064d-85e9-4ea1-aefb-e42b60b88679
caps.latest.revision: 4
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9460c8b6ca8db927af4064e3567eca34c1bf5c91
ms.openlocfilehash: c7acce9d41af7e72b04b89751a7b186c9581dfea
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-grid-control39s-space-allocation-to-star-columns"></a>Mitigazione: Allocazione dello spazio di controllo della griglia alle colonne a stella

A partire dalle applicazioni destinate a .NET Framework 4.7, WPF sostituisce l'algoritmo usato dal controllo <xref:System.Windows.Controls.Grid> per allocare spazio alle colonne \*. 

## <a name="whats-changed"></a>Novità

Il nuovo algoritmo consente di risolvere diversi bug presenti nell'algoritmo precedente:

1. L'allocazione totale alle colonne può superare la larghezza della griglia. Ciò può verificarsi quando si alloca spazio a una colonna la cui quota proporzionale è minore rispetto alle dimensioni minime. L'algoritmo alloca le dimensioni minime, riducendo lo spazio disponibile per le altre colonne. Se non sono presenti colonne \* da allocare, l'allocazione totale potrebbe essere troppo grande.

1. L'allocazione totale può non raggiungere la larghezza della griglia. Questo è il doppio problema di # 1, che si verifica quando si effettua l'allocazione a una colonna la cui quota proporzionale è maggiore rispetto alle sue dimensioni massime, senza alcuna colonna \* per sfruttare la flessibilità.

1. Due colonne \* possono ricevere le allocazioni in modo non proporzionale ai loro pesi. Questa è una versione più lieve di #1/#2, che si verifica durante l'allocazione alle colonne * A, B e C (in questo ordine), dove la quota proporzionale di B viola il suo vincolo min o max. Come in precedenza, lo spazio disponibile alla colonna C si riduce e questa ottiene un'allocazione proporzionale inferiore o superiore rispetto ad A,

1. Le colonne con pesi estremamente alti (> 10^298) vengono considerate tutte come se avessero un peso di 10^298. Le differenze proporzionali tra di esse (e tra le colonne con pesi leggermente inferiori) non vengono rispettate.

1. Le colonne con pesi infiniti non vengono gestite correttamente. [In realtà non è possibile impostare un peso su infinito, ma si tratta di una limitazione artificiale. Il codice di allocazione stava tentando di gestirlo, ma in un processo non valido.]

1. Diversi problemi minori mentre si evita l'overflow, l'underflow, la perdita di precisione e altri problemi analoghi della virgola mobile.

1. Le modifiche per l'arrotondamento del layout con un DPI sufficientemente elevato non sono corrette.

Il nuovo algoritmo produce risultati che soddisfano i criteri seguenti:

Un  La larghezza effettiva assegnata a una colonna * non è mai minore della larghezza minima né maggiore della larghezza massima.

B. A ogni colonna a cui non è assegnata la larghezza minima o massima è assegnata una larghezza proporzionale al relativo peso. Per essere precisi, se si dichiara che due colonne hanno rispettivamente una larghezza x e y e se nessuna delle colonne riceve la larghezza minima o massima, le larghezze effettive v e w assegnate alle colonne hanno la stessa proporzione: v / w == x / y.

C. La larghezza totale allocata alle colonne \* proporzionali è uguale allo spazio disponibile dopo avere effettuato l'allocazione alle colonne vincolate (fisse, automatiche e colonne \* che vengono allocate alla loro larghezza min o max). Potrebbe essere pari a zero, ad esempio se la somma delle larghezze minime è superiore alla larghezza disponibile della griglia.

D. Tutte queste istruzioni devono essere interpretate in base al layout "ideale". Quando l'arrotondamento del layout è attivo, le larghezze effettive possono differire dalle larghezze ideali per un massimo di un pixel.

L'algoritmo precedente rispettava (A) ma non gli altri criteri nei casi descritti in precedenza.

Quanto detto sulle colonne e le relative larghezze in questo argomento si applica anche a righe e altezza.

## <a name="impact"></a>Impatto

Il nuovo algoritmo modifica la larghezza effettiva assegnata alle colonne \* in diversi casi:

- Quando una o più colonne \* hanno anche una larghezza minima o massima che esegue l'override dell'allocazione proporzionale per tale colonna. (La larghezza minima può derivare da una dichiarazione esplicita <xref:System.Windows.FrameworkElement.MinWidth%2A> o da un minimo implicito ottenuto dal contenuto della colonna. La larghezza massima può essere definita solo in modo esplicito da una dichiarazione <xref:System.Windows.FrameworkElement.MaxWidth%2A>.)

- Quando una o più colonne \* dichiarano un peso \* estremamente elevato, maggiore di 10^298.

- Quando i pesi \* sono diversi al punto da far sì che si verifichi un'instabilità a virgola mobile (overflow, underflow, perdita di precisione).

- Quando è abilitato l'arrotondamento del layout e il DPI effettivamente visualizzato è sufficientemente elevato.

Nei primi due casi, le larghezze generate dal nuovo algoritmo possono essere notevolmente diverse da quelle generate dal vecchio algoritmo; nell'ultimo caso, la differenza sarà di uno o due pixel al massimo.

## <a name="mitigation"></a>Attenuazione

Per impostazione predefinita, le applicazioni destinate alle versioni di .NET Framework a partire dalla 4.7 useranno il nuovo algoritmo, mentre le applicazioni destinate a .NET Framework 4.6.2 o versioni precedenti useranno il vecchio algoritmo.

Per ignorare l'impostazione predefinita, usare l'impostazione di configurazione seguente:

```xml
<runtime>
    <AppContextSwitchOverrides value="Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=true" /> 
</runtime>
```

Tramite il valore 'true' è possibile selezionare il vecchio algoritmo, mentre con 'false' è possibile selezionare il nuovo algoritmo.

## <a name="see-also"></a>Vedere anche
[Reindirizzamento delle modifiche in .NET Framework 4.7](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md)

