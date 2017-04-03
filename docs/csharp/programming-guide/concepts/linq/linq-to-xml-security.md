---
title: Sicurezza in LINQ to XML (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: ef2c0dc9-ecf9-4c17-b24e-144184ab725f
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d4da76c120b8028c12a8c2ac58e5130d89a01e05
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-security-c"></a>Sicurezza in LINQ to XML (C#)
In questo argomento vengono descritti i problemi di sicurezza associati a LINQ to XML. Vengono inoltre fornite alcune indicazioni per ridurre l'esposizione ai rischi.  
  
## <a name="linq-to-xml-security-overview"></a>Cenni preliminari sulla sicurezza in LINQ to XML  
 LINQ to XML è progettato più per semplificare la programmazione che per applicazioni lato server con requisiti rigorosi di sicurezza. La maggior parte degli scenari XML sono costituiti dall'elaborazione di documenti XML attendibili, anziché dall'elaborazione di documenti XML non attendibili caricati in un server. LINQ to XML è ottimizzato per questi scenari.  
  
 Se è necessario elaborare dati non attendibili provenienti da origini sconosciute, è consigliabile usare un'istanza della classe <xref:System.Xml.XmlReader> configurata per filtrare gli attacchi di tipo Denial of Service XML noti.  
  
 Se è stata configurata una classe <xref:System.Xml.XmlReader> per limitare gli attacchi Denial of Service, è possibile usare il lettore per popolare l'albero LINQ to XML e trarre comunque vantaggio dai miglioramenti di LINQ to XML per la produttività nella programmazione. Diverse tecniche implicano la creazione di lettori configurati per limitare i problemi di sicurezza e quindi la creazione di istanze di un albero XML tramite il lettore configurato.  
  
 XML è intrinsecamente vulnerabile agli attacchi di tipo Denial of Service, perché i documenti non presentano vincoli in termine di dimensioni, complessità, dimensioni dei nomi degli elementi e così via. Indipendentemente dal componente usato per l'elaborazione XML, è necessario essere sempre pronti a riciclare il dominio dell'applicazione se usa una quantità eccessiva di risorse.  
  
## <a name="mitigation-of-xml-xsd-xpath-and-xslt-attacks"></a>Limitazione degli attacchi XML, XSD, XPath e XSLT  
 LINQ to XML è basato su <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter>. LINQ to XML supporta XSD e XPath tramite i metodi di estensione negli spazi dei nomi <xref:System.Xml.Schema?displayProperty=fullName> e <xref:System.Xml.XPath?displayProperty=fullName>. Usando le classi <xref:System.Xml.XmlReader>, <xref:System.Xml.XPath.XPathNavigator> e <xref:System.Xml.XmlWriter> in associazione a LINQ to XML, è possibile richiamare XSLT per trasformare gli alberi XML.  
  
 Se si opera in ambienti meno protetti, è necessario tenere conto di diversi problemi di sicurezza associati a XML e all'uso delle classi in <xref:System.Xml?displayProperty=fullName>, <xref:System.Xml.Schema?displayProperty=fullName>, <xref:System.Xml.XPath?displayProperty=fullName> e <xref:System.Xml.Xsl?displayProperty=fullName>. Di seguito sono riportati solo alcuni di questi problemi:  
  
-   XSD, XPath e XSLT sono linguaggi basati su stringa in cui è possibile specificare operazioni che richiedono quantità elevate di tempo o memoria. È responsabilità dei programmatori di applicazioni che ottengono stringhe XSD, XPath o XSLT da origini non attendibili verificare che tali stringhe non siano dannose o monitorare e limitare la possibilità che la valutazione delle stringhe comporti un consumo eccessivo delle risorse di sistema.  
  
-   Gli schemi XSD (compresi quelli inline) sono intrinsecamente vulnerabili ad attacchi di tipo Denial of Service. Non accettare schemi da origini non attendibili.  
  
-   XSD e XSLT possono includere riferimenti ad altri file, ad esempio riferimenti che generano attacchi tra zone e tra domini diversi.  
  
-   Le entità esterne nelle dichiarazioni DTD possono generare attacchi tra zone e tra domini diversi.  
  
-   Le dichiarazioni DTD sono vulnerabili ad attacchi di tipo Denial of Service  
  
-   I documenti XML particolarmente complessi possono presentare problemi di Denial of Service. È preferibile limitare la complessità dei documenti XML.  
  
-   Non accettare componenti di supporto, ad esempio oggetti <xref:System.Xml.NameTable>, <xref:System.Xml.XmlNamespaceManager> e <xref:System.Xml.XmlResolver> provenienti da assembly non attendibili.  
  
-   Leggere i dati in blocchi per limitare gli attacchi a documenti di grandi dimensioni.  
  
-   I blocchi di script nei fogli di stile XSLT possono esporre numerosi attacchi.  
  
-   Effettuare convalide accurate prima di costruire espressioni XPath dinamiche.  
  
## <a name="linq-to-xml-security-issues"></a>Problemi di sicurezza in LINQ to XML  
 I problemi di sicurezza illustrati in questo argomento non vengono presentati in un ordine specifico. Tutti i problemi sono importanti e devono essere affrontati nel modo appropriato.  
  
 Un attacco riuscito di tipo elevazione dei privilegi offre a un assembly dannoso un maggior controllo sull'ambiente. Può inoltre provocare la diffusione di dati, problemi di Denial of Service e così via.  
  
 Le applicazioni non devono diffondere dati agli utenti che non sono autorizzati a visualizzarli.  
  
 Gli attacchi di tipo Denial of Service causano il consumo di quantità eccessive di memoria o tempo CPU da parte di LINQ to XML. Sono considerati meno gravi degli attacchi di tipo elevazione dei privilegi o di quelli che comportano la diffusione di dati. Tuttavia, sono estremamente importanti negli scenari in cui un server deve elaborare documenti XML provenienti da origini non attendibili.  
  
### <a name="exceptions-and-error-messages-might-reveal-data"></a>Eccezioni e messaggi di errore possono rivelare dati  
 La descrizione di un errore può rivelare dati, ad esempio i dati che vengono trasformati, nomi file o dettagli sull'implementazione. I messaggio di errore non devono essere esposti a chiamanti non attendibili. È necessario intercettare tutti gli errori e segnalarli con messaggi di errore personalizzati.  
  
### <a name="do-not-call-codeaccesspermissionsassert-in-an-event-handler"></a>Non eseguire chiamate a CodeAccessPermissions.Assert in un gestore eventi  
 A un assembly possono essere associate autorizzazioni minori o maggiori. Gli assembly con autorizzazioni maggiori hanno un maggior controllo sul computer e sugli ambienti.  
  
 Se il codice di un assembly con autorizzazioni maggiori chiama <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> in un gestore eventi e quindi l'albero XML viene passato a un assembly dannoso con autorizzazioni limitate, l'assembly dannoso può causare la generazione di un evento. Poiché l'evento esegue codice incluso nell'assembly con autorizzazioni maggiori, l'assembly dannoso opererebbe in questo caso con privilegi elevati.  
  
 È consigliabile non eseguire mai chiamate a <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> in un gestore eventi.  
  
### <a name="dtds-are-not-secure"></a>Le dichiarazioni DTD non sono protette  
 Le entità nelle dichiarazioni DTD sono intrinsecamente non protette. È possibile che un documento XML dannoso contenente una dichiarazione DTD provochi l'uso di tutta la memoria e il tempo CPU disponibili da parte del parser, generando un attacco Denial of Service. Pertanto, in LINQ to XML l'elaborazione DTD è disattivata per impostazione predefinita. Non accettare DTD provenienti da origini non attendibili.  
  
 È ad esempio possibile che vengano accettate DTD da origini non attendibili nel caso di un'applicazione Web che consente agli utenti Web di caricare un file XML che fa riferimento a una DTD e a un file DTD. Dopo la convalida del file, una DTD dannosa potrebbe eseguire un attacco Denial of Service sul server. Un altro esempio di DTD accettate da origini non attendibili è il riferimento a una DTD su una condivisione di rete che consente anche l'accesso FTP anonimo.  
  
### <a name="avoid-excessive-buffer-allocation"></a>Evitare allocazioni eccessive di buffer  
 Gli sviluppatori di applicazioni devono essere consapevoli che origini dati di dimensioni estremamente grandi possono portare all'esaurimento delle risorse e ad attacchi Denial of Service.  
  
 Se un utente malintenzionato invia o carica un documento XML di grandi dimensioni, può causare un consumo eccessivo di risorse di sistema da parte di LINQ to XML. Ciò costituisce un attacco di tipo Denial of Service. Per evitare questo problema, è possibile impostare la proprietà <xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=fullName> e creare un lettore che è a questo punto limitato per quanto riguarda le dimensioni del documento che è in grado di caricare. Usare quindi il lettore per creare l'albero XML.  
  
 Se ad esempio è noto che le dimensioni massime previste dei documenti XML provenienti da un'origine non attendibile saranno minori di 50.000 byte, impostare <xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=fullName> su 100.000. In questo modo l'elaborazione dei documenti XML non viene ostacolata e allo stesso tempo è possibile limitare le minacce di Denial of Service che si presenterebbero se fosse possibile caricare documenti che consumano grandi quantità di memoria.  
  
### <a name="avoid-excess-entity-expansion"></a>Evitare un'eccessiva espansione delle entità  
 Un tipo noto di attacco Denial of Service associato all'utilizzo di una dichiarazione DTD si verifica quando un documento provoca un'eccessiva espansione delle entità. Per evitare questo problema, è possibile impostare la proprietà <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities%2A?displayProperty=fullName> e creare un lettore che a questo punto è limitato per quanto riguarda il numero di caratteri risultanti dall'espansione di entità. Usare quindi il lettore per creare l'albero XML.  
  
### <a name="limit-the-depth-of-the-xml-hierarchy"></a>Limitare la profondità della gerarchia XML  
 Un possibile attacco di tipo Denial of Service si verifica quando viene inviato un documento con una profondità della gerarchia eccessiva. Per evitare questo problema, è possibile eseguire il wrapping di un oggetto <xref:System.Xml.XmlReader> nella classe che conteggia la profondità degli elementi. Se la profondità supera un predeterminato livello ragionevole, è possibile terminare l'elaborazione del documento dannoso.  
  
### <a name="protect-against-untrusted-xmlreader-or-xmlwriter-implementations"></a>Proteggersi da implementazioni XmlReader o XmlWriter non attendibili  
 Gli amministratori devono verificare che tutte le implementazioni <xref:System.Xml.XmlReader> o <xref:System.Xml.XmlWriter> fornite esternamente abbiano nomi sicuri e siano state registrate nella configurazione del computer. In questo modo è possibile evitare il caricamento di malware camuffato da lettore o writer.  
  
### <a name="periodically-free-objects-that-reference-xname"></a>Liberare periodicamente gli oggetti che fanno riferimento a XName  
 Per proteggersi da determinati tipi di attacco, i programmatori di applicazioni devono liberare periodicamente tutti gli oggetti che fanno riferimento a un oggetto <xref:System.Xml.Linq.XName> nel dominio dell'applicazione.  
  
### <a name="protect-against-random-xml-names"></a>Proteggersi da nomi XML casuali  
 Le applicazioni che accettano dati da origini non attendibili dovrebbero eseguire il wrapping di un oggetto <xref:System.Xml.XmlReader> nel codice personalizzato per esaminare la possibile presenza di nomi e spazi dei nomi XML casuali. Se vengono individuati nomi e spazi dei nomi XML casuali, l'applicazione può terminare l'elaborazione del documento dannoso.  
  
 È possibile limitare il numero di nomi in un determinato spazio dei nomi (inclusi i nomi non inseriti in uno spazio dei nomi) a un livello ragionevole.  
  
### <a name="annotations-are-accessible-by-software-components-that-share-a-linq-to-xml-tree"></a>Annotazioni accessibili a componenti software che condividono un albero LINQ to XML  
 È possibile usare LINQ to XML per compilare pipeline di elaborazione in cui componenti diversi dell'applicazione caricano, convalidano, eseguono query, trasformano, aggiornano e salvano i dati XML passati tra componenti come alberi XML. In questo modo è possibile ottimizzare le prestazioni, perché l'overhead associato al caricamento e alla serializzazione di oggetti in testo XML viene eseguito solo fino alle estremità della pipeline. Gli sviluppatori devono tenere presente, tuttavia, che tutte le annotazioni e i gestori eventi creati da un componente sono accessibili ad altri componenti. Ciò può creare numerose vulnerabilità se i componenti presentano livelli di attendibilità diverse. Per compilare pipeline protette tra componenti meno attendibili, è necessario serializzare gli oggetti LINQ to XML in testo XML prima di passare i dati a un componente non attendibile.  
  
 CLR (Common Language Runtime) rende disponibile un certo grado di sicurezza. Ad esempio, un componente che non include una classe privata non può accedere alle annotazioni immesse da tale classe. Tuttavia, le annotazioni possono essere eliminate dai componenti che non sono in grado di leggerle. Questa situazione può essere sfruttata in un attacco di tipo manomissione.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
