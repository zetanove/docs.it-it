---
title: "Progettazione di enum | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "indicazioni per la progettazione di tipo, le enumerazioni"
  - "enumerazioni semplici"
  - "enumerazioni [.NET Framework], linee guida di progettazione"
  - "classe libreria linee guida di progettazione [.NET Framework], enumerazioni"
  - "enumerazioni Flags"
ms.assetid: dd53c952-9d9a-4736-86ff-9540e815d545
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Progettazione di enum
Le enumerazioni sono un tipo speciale di tipo di valore. Esistono due tipi di enumerazioni: enumerazioni di flag e le enumerazioni semplici.  
  
 Enumerazioni semplici rappresentano piccoli set chiuso di scelte. Un esempio comune di enum semplice è un set di colori.  
  
 Enumerazioni di flag sono progettate per supportare le operazioni bit per bit sui valori enum. Un esempio comune di enumerazione flag è un elenco di opzioni.  
  
 **✓ si** usare un enum per tipizzare fortemente parametri, proprietà e restituiscono valori che rappresentano i set di valori.  
  
 **✓ si** preferire l'utilizzo di un tipo enum anziché costanti statiche.  
  
 **X non** utilizzare un'enumerazione per gli insiemi aperti \(ad esempio, la versione del sistema operativo, i nomi degli amici, e così via\).  
  
 **X non** forniscono valori enum riservato che servono per utilizzi futuri.  
  
 È possibile aggiungere sempre semplicemente i valori per l'enumerazione esistente in una fase successiva. Vedere [aggiunta di valori per le enumerazioni](#add_value) per ulteriori informazioni sull'aggiunta di valori per le enumerazioni. Valori riservati è sufficiente eseguire il set di valori reali e tendono a produrre errori dell'utente.  
  
 **X evitare** esporre pubblicamente le enumerazioni con un solo valore.  
  
 Una pratica comune per garantire un'estendibilità futura delle API C consiste nell'aggiungere parametri riservati per le firme del metodo. Tali parametri riservati possono essere espresso come le enumerazioni con un valore predefinito singolo. Questo non deve essere eseguito in API gestite. Metodi \(overload\) consente di aggiungere parametri nelle versioni future.  
  
 **X non** includere valori sentinel nelle enumerazioni.  
  
 Sebbene talvolta utili agli sviluppatori di framework, valori sentinel possono generare confusione per gli utenti di framework. Vengono utilizzati per tenere traccia dello stato di essere uno dei valori di enumerazione piuttosto che dal set rappresentato dal tipo enum.  
  
 **✓ si** fornire un valore pari a zero sulle enumerazioni semplici.  
  
 Si consiglia di chiamare il valore come "None". Se tale valore non è appropriato per questa enumerazione specifica, il valore predefinito più comune per l'enumerazione deve essere assegnato il valore sottostante pari a zero.  
  
 **✓ PROVARE** utilizzando <xref:System.Int32> \(impostazione predefinita nella maggior parte dei linguaggi di programmazione\) con il tipo sottostante di un'enumerazione, a meno che una delle operazioni seguenti è vera:  
  
-   L'enumerazione è un'enumerazione flags e disporre di più di 32 flag oppure prevede che più in futuro.  
  
-   Il tipo sottostante deve essere diverso da quello <xref:System.Int32> per semplificare l'interoperabilità con codice non gestito, che prevede le enumerazioni di dimensioni diverse.  
  
-   Un tipo sottostante più piccolo comporta risparmi notevoli in uno spazio. Se si prevede di enum deve essere utilizzato principalmente come argomento per il flusso di controllo, la dimensione è poco rilevante. Il risparmio potrebbe essere significativo se:  
  
    -   Si prevede di enum deve essere utilizzato come un campo in una struttura molto spesso un'istanza o una classe.  
  
    -   Si prevede che gli utenti di creare matrici di grandi dimensioni o le raccolte delle istanze di enum.  
  
    -   Si prevede un numero elevato di istanze dell'enumerazione da serializzare.  
  
 Per informazioni sull'utilizzo in memoria, tenere presente che gli oggetti gestiti sono sempre `DWORD`\-allineati, pertanto è necessario in modo efficace più enumerazioni o altre strutture di piccole dimensioni in un'istanza di tipo pack un'enumerazione con più piccola per fare la differenza, poiché la dimensione totale dell'istanza sarà sempre essere arrotondato per eccesso un `DWORD`.  
  
 **✓ si** denominare le enumerazioni di flag con nomi plurali o frasi e le enumerazioni semplici con singolare o frasi.  
  
 **X non** estendere <xref:System.Enum?displayProperty=fullName> direttamente.  
  
 <xref:System.Enum?displayProperty=fullName> un tipo speciale utilizzato da CLR per creare enumerazioni definite dall'utente. La maggior parte dei linguaggi di programmazione fornisce un elemento di programmazione che consente di accedere a questa funzionalità. Ad esempio, in c\# di `enum` parola chiave viene utilizzata per definire un'enumerazione.  
  
<a name="design"></a>   
### Enumerazioni di Flag progettazione  
 **✓ si** si applicano le <xref:System.FlagsAttribute?displayProperty=fullName> per le enumerazioni di flag. Non si applica questo attributo per le enumerazioni semplici.  
  
 **✓ si** utilizzare potenze di due per i valori di enumerazione flag possono essere liberamente combinati mediante un'operazione OR bit per bit.  
  
 **✓ PROVARE** fornendo i valori di enumerazione speciali per comunemente utilizzato le combinazioni di flag.  
  
 Operazioni bit per bit sono un concetto avanzato e non devono essere richiesta per eseguire semplici operazioni.<xref:System.IO.FileAccess> è un esempio di tale valore speciale.  
  
 **X evitare** creazione enumerazioni di flag in alcune combinazioni di valori non sono validi.  
  
 **X evitare** utilizzando flag valori enum pari a zero, a meno che il valore rappresenta "tutti i flag sono cancellati" ed è denominato in modo appropriato, come stabilito dalla linea guida successiva.  
  
 **✓ si** nome il valore zero delle enumerazioni di flag `None`. Per un'enumerazione di flag, il valore deve sempre indicare "tutti i flag vengono cancellati."  
  
<a name="add_value"></a>   
### Aggiunta di valore alle enumerazioni  
 È molto comune per rilevare che è necessario aggiungere i valori enum dopo aver spedito già. È un potenziale problema di compatibilità dell'applicazione quando viene restituito il valore appena aggiunto da un'API esistente, poiché il nuovo valore potrebbero non gestire correttamente le applicazioni scritte in modo inadeguato.  
  
 **✓ PROVARE** aggiunta di valori per le enumerazioni, nonostante un rischio per la compatibilità di piccole dimensioni.  
  
 Se si dispone di dati reali sull'incompatibilità delle applicazioni causati da aggiunte a un'enumerazione, è consigliabile aggiungere una nuova API che restituisce i valori vecchi e nuovi e deprecare l'API precedente, che deve continuare la restituzione solo i valori precedenti. Ciò garantisce che le applicazioni esistenti sono compatibili.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di tipo](../../../docs/standard/design-guidelines/type.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)