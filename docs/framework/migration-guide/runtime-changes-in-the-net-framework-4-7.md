---
title: Modifiche al runtime in .NET Framework 4.7 | Microsoft Docs
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- runtime changes,.NET Framework
- runtime changes,.NET Framework 4.7
- application compatibility
ms.assetid: 268eb334-7906-4e0b-a1e3-c74b745de2a5
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 321ec8f8293afad0f3da7fb6f907f45d404394cc
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="runtime-changes-in-the-net-framework-47"></a>Modifiche al runtime in .NET Framework 4.7

In rari casi, le modifiche al runtime potrebbero incidere sulle app esistenti destinate alle versioni precedenti di .NET Framework, ma eseguite in una versione successiva del runtime di .NET Framework. Includono anche le differenze di comportamento tra le applicazioni eseguite in diversi ambienti di runtime di .NET Framework. .NET Framework 4.6.2 include modifiche nelle aree seguenti:

- [Windows Presentation Foundation (WPF)](#WPF)

La colonna Ambito nelle tabelle seguenti contiene il significato di ogni modifica:

- Principale Una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice. Si noti che le modifiche di reindirizzamento non rientrano in questa categoria.

- Secondaria. Una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.

- Bordo. Una modifica che influisce sulle app in scenari molto specifici e non comuni.

- Trasparente. Una modifica che non ha effetti evidenti sullo sviluppatore o sull'utente dell'app. L'app non dovrebbe richiedere variazioni a causa di questa modifica.

## <a name="a-namewpf--windows-presentation-foundation-wpf"></a><a name="WPF" /> Windows Presentation Foundation (WPF)

assetId:///M:System.Windows.Controls.DataGridCellsPanel.BringIndexIntoView(System.Int32)?qualifyHint=False&autoUpgrade=True

| Funzionalità | Modifica | Impatto | Ambito |
|---|---|---|---|
| Metodo <xref:System.Windows.Controls.DataGridCellsPanel.BringIndexIntoView%2A> | In .NET Framework 4.6.2, il metodo <xref:System.Windows.Controls.DataGridCellsPanel.BringIndexIntoView%2A> viene eseguito in modo asincrono quando è abilitata la virtualizzazione delle colonne la cui larghezza tuttavia non è stata determinata. Se le colonne vengono rimosse prima che venga completata l'operazione asincrona, può verificarsi un'eccezione <xref:System.ArgumentOutOfRangeException>.<br/></br>A partire da .NET Framework 4.7, l'eccezione non viene più generata in questo scenario. | Questa modifica migliora l'affidabilità del metodo. | Microsoft Edge | 
|Sfondo <xref:System.Windows.Controls.Ribbon.RibbonGroup> | In .NET Framework 4.6.2 e nelle versioni precedenti, lo sfondo <xref:System.Windows.Controls.Ribbon.RibbonGroup> su build localizzate è stato disegnato con un pennello trasparente e questo ha determinato un'esperienza dell'interfaccia utente di basso livello. In .NET Framework 4.7, WPF aggiorna le risorse localizzate per il controllo <xref:System.Windows.Controls.Ribbon.RibbonGroup>, in modo da garantire che sia selezionato il pennello corretto. | Per sfruttare i vantaggi del nuovo comportamento, eseguire l'aggiornamento a .NET Framework 4.7. | Microsoft Edge |
| Controllo ortografico WPF | A partire da .NET Framework 4.6.1, il controllo ortografico nelle applicazioni WPF genera talvolta un'eccezione <xref:System.ObjectDisposedException> durante la chiusura dell'applicazione. <br/><br/>In .NET Framework 4.7, l'eccezione viene gestita correttamente dal runtime, in modo da garantire che le applicazioni non vengano più compromesse. Notare che le eccezioni first-chance occasionali continueranno a essere osservate nelle applicazioni in esecuzione in un debugger.  | Per sfruttare i vantaggi del nuovo comportamento, eseguire l'aggiornamento a .NET Framework 4.7.   | Microsoft Edge |

## <a name="see-also"></a>Vedere anche

[Compatibilità delle applicazioni in .NET Framework 4.7](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-7.md)


