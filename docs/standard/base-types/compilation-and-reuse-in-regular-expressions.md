---
title: "Compilazione e riutilizzo nelle espressioni regolari | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "espressioni regolari di .NET Framework, compilazione"
  - "espressioni regolari di .NET Framework, motori"
  - "compilazione, espressioni regolari"
  - "analisi di testo con espressioni regolari, compilazione"
  - "corrispondenza al modello con espressioni regolari, compilazione"
  - "espressioni regolari, compilazione"
  - "espressioni regolari, motori"
  - "ricerca con espressioni regolari, compilazione"
ms.assetid: 182ec76d-5a01-4d73-996c-0b0d14fcea18
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Compilazione e riutilizzo nelle espressioni regolari
È possibile ottimizzare le prestazioni delle applicazioni in cui vengono ampiamente utilizzate le espressioni regolari comprendendo il modo in cui le espressioni vengono compilate dal motore delle espressioni regolari e la relativa memorizzazione nella cache.  In questo argomento vengono illustrate la compilazione e la memorizzazione nella cache.  
  
## espressioni regolari compilate  
 In base all'impostazione predefinita, il modulo delle espressioni regolari consente di compilare un'espressione regolare in una sequenza di istruzioni interne, ovvero di codici ad alto livello diversi dal linguaggio intermedio Microsoft o da MSIL.  Quando il modulo di gestione esegue un'espressione regolare, interpreta i codici interni.  
  
 Se un oggetto <xref:System.Text.RegularExpressions.Regex> viene costruito con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, l'espressione regolare verrà compilata nel codice MSIL esplicito anziché nelle istruzioni interne di alto livello utilizzate per le espressioni regolari.  In tal modo il compilatore JIT \(Just\-In\-Time\) di .NET Framework potrà convertire l'espressione nel codice macchina nativo del computer per ottenere prestazioni migliori.  
  
 Non è tuttavia possibile scaricare il codice MSIL generato.  L'unico modo per scaricare il codice consiste nello scaricare l'intero dominio applicazione, cioè tutto il codice dell'applicazione.  Una volta compilata un'espressione regolare con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, .NET Framework non rilascia mai le risorse utilizzate dall'espressione compilata, anche se l'espressione regolare è stata creata da un oggetto <xref:System.Text.RegularExpressions.Regex> rilasciato a sua volta in un Garbage Collection.  
  
 Per evitare un utilizzo eccessivo di risorse, è necessario limitare il numero di espressioni regolari diverse compilate con l'opzione <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>.  Se è necessario che un'applicazione utilizzi un numero elevato o illimitato di espressioni regolari, è consigliabile che tali espressioni siano interpretate e non compilate.  Nel caso si abbia invece un numero ridotto di espressioni regolari utilizzate ripetutamente, sarà preferibile compilarle con <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> per ottenere prestazioni migliori.  In alternativa è possibile utilizzare espressioni regolari precompilate.  È possibile compilare tutte le espressioni in una DLL riutilizzabile mediante il metodo <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A>,  in modo che non sia necessario compilare in fase di esecuzione, pur consentendo di usufruire della velocità delle espressioni regolari compilate.  
  
## Cache delle espressioni regolari  
 Per migliorare le prestazioni, il motore delle espressioni regolari gestisce una cache a livello applicazione delle espressioni regolari compilate.  Nella cache vengono archiviati i criteri di ricerca di espressioni regolari utilizzati solo nelle chiamate al metodo statico. I criteri di ricerca di espressioni regolari forniti ai metodi di istanza non vengono memorizzati nella cache. In tal modo non è necessario riconvertire un'espressione in codice di alto livello ogni volta che la si utilizza.  
  
 Il numero massimo di espressioni regolari memorizzate nella cache è determinato dal valore della proprietà <xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=fullName> `static` \(`Shared` in Visual Basic\).  Per impostazione predefinita, il motore delle espressioni regolari memorizza nella cache fino a 15 espressioni regolari compilate.  Se il numero di espressioni regolari compilate supera la dimensione della cache, verrà eliminata l'espressione regolare utilizzata meno di recente e verrà memorizzata nella cache la nuova espressione regolare.  
  
> [!IMPORTANT]
>  La modalità di memorizzazione nella cache delle espressioni regolari in .NET Framework versione 2.0 differisce notevolmente da quella in .NET Framework versioni 1.0 e 1.1.  In .NET Framework 1.0 e 1.1 vengono memorizzate nella cache tutte le espressioni regolari, sia quelle utilizzate nelle chiamate al metodo statico che quelle utilizzate nelle chiamate al metodo di istanza.  La cache viene espansa automaticamente per archiviare le nuove espressioni regolari.  In .NET Framework 2.0 vengono memorizzate nella cache solo le espressioni regolari utilizzate nelle chiamate al metodo statico.  Per impostazione predefinita, vengono memorizzate nella cache le ultime 15 espressioni regolari, sebbene la dimensione della cache possa essere regolata impostando il valore della proprietà <xref:System.Text.RegularExpressions.Regex.CacheSize%2A>.  
  
 L'applicazione utilizzata può sfruttare le espressioni regolari precompilate in uno dei due modi seguenti:  
  
-   Utilizzando un metodo statico dell'oggetto <xref:System.Text.RegularExpressions.Regex> per definire l'espressione regolare.  Se si utilizza un criterio di ricerca di espressioni regolari già definito in un'altra chiamata al metodo statico, questo verrà recuperato dalla cache dal motore delle espressioni regolari.  In caso contrario, il motore compilerà l'espressione regolare aggiungendola nella cache.  
  
-   Riutilizzando un oggetto <xref:System.Text.RegularExpressions.Regex> esistente purché sia necessario il relativo criterio di ricerca di espressioni regolari.  
  
 A causa del sovraccarico dovuto alla creazione di istanze degli oggetti e alla compilazione di espressioni regolari, la creazione e la rapida eliminazione di numerosi oggetti <xref:System.Text.RegularExpressions.Regex> comportano un eccessivo dispendio di risorse.  Per le applicazioni che utilizzano molte espressioni regolari diverse, è possibile ottimizzare le prestazioni mediante le chiamate ai metodi `Regex` statici e aumentando eventualmente la dimensione della cache delle espressioni regolari.  
  
## Vedere anche  
 [Espressioni regolari di .NET Framework](../../../docs/standard/base-types/regular-expressions.md)