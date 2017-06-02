---
title: "Risoluzione di risorse esterne | Microsoft Docs"
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
ms.assetid: ad3fa320-4b8f-4e5c-b549-01157591007a
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Risoluzione di risorse esterne
La proprietà **XmlResolver** di **XmlDocument** viene usata dalla classe **XmlDocument** per individuare le risorse non inline nei dati XML, quali DTD, entità e schemi esterni.  Questi elementi possono trovarsi in una rete o in un'unità locale ed essere identificati tramite un URI \(Uniform Resource Identifier\) .  Questo consente a **XmlDocument** di risolvere i nodi **EntityReference** presenti nel documento e convalidare il documento in base allo schema o alla DTD esterna.  
  
## XmlDocument completamente attendibile  
 La proprietà **XmlResolver** influisce sulla funzionalità del metodo **XmlDocument.Load**.  Nella tabella seguente viene illustrato il funzionamento della proprietà **XmlDocument.XmlResolver** quando l'oggetto **XmlDocument** è completamente attendibile.  Vengono inoltre indicati i metodi **XmlDocument.Load** quando l'input di Load è **TextReader**, **String**, **Stream** o **URI**.  Il contenuto della tabella non si applica al metodo **Load** se **XmlDocument** viene caricato da un **XmlReader**.  
  
|XmlResolver, proprietà|Funzione|Note|  
|----------------------------|--------------|----------|  
|La proprietà è impostata su una classe **XmlResolver** creata in precedenza e con proprietà già impostate dall'utente.|**XmlDocument** consente di usare l'**XmlResolver** assegnato per risolvere nomi di file e riferimenti a risorse esterne, quali DTD, entità e schemi.<br /><br /> **XmlResolver** viene usato anche quando si risolvono risorse esterne necessarie per l'aggiunta o la modifica di nodi in **XmlDocument**.|L'**XmlResolver** assegnato a **XmlDocument** è il sistema di risoluzione usato quando è necessario individuare e risolvere risorse esterne.|  
|La proprietà è impostata su **null** \(**Nothing** in Microsoft Visual Basic .NET\).|Non sono supportate le funzionalità che richiedono una risorsa esterna, ad esempio l'individuazione di uno schema o una DTD esterna.  Le entità esterne non verranno risolte e non è supportata la modifica delle funzioni, come l'inserimento di nodi di entità che richiedono la risoluzione.|**XmlDocument** consente di caricare i file come anonimi e non tenta di risolvere altre risorse.|  
|La proprietà non viene impostata, ma rimane nello stato predefinito.|Verrà creata un'istanza di un **XmlUrlResolver** con credenziali NULL e verrà usata dal documento **XmlDocument** nella risoluzione dei nomi di file, nell'individuazione delle DTD, delle entità e degli schemi esterni. Le credenziali **null** verranno usate per la modifica dei nodi.||  
  
 Viene inoltre indicato il metodo **XmlDocument.Load** quando l'input di **Load** è **XmlReader** e **XmlDocument** è completamente attendibile.  
  
|XmlResolver, proprietà|Funzione|Note|  
|----------------------------|--------------|----------|  
|La classe **XmlResolver** usata da **XmlDocument** è la stessa usata da **XmlReader**.|**XmlDocument** usa l'**XmlResolver** assegnato a **XmlReader**.<br /><br /> Non è possibile impostare la proprietà **XmlDocument.Resolver**, indipendentemente dal livello di attendibilità di **XmlDocument**, poiché ottiene un **XmlResolver** da **XmlReader**.  Non è possibile eseguire l'override delle impostazioni **XmlResolver** di **XmlReader** impostando la proprietà **XmlResolver** di **XmlDocument**.|**XmlReader** può essere l'**XmlTextReader**, **XmlValidatingReader** o un lettore personalizzato.  Se il lettore usato supporta la risoluzione di entità, le entità esterne vengono risolte.  I riferimenti alle entità non vengono risolti se il lettore passato non li supporta.|  
  
## XmlDocument semi\-trusted  
 Nella tabella seguente viene illustrato il funzionamento della proprietà **XmlDocument.XmlResolver** quando l'oggetto è semi\-trusted.  Il contenuto della tabella si applica ai metodi **XmlDocument.Load** quando l'input di Load è **TextReader**, **String**, **Stream** o **URI**.  Il contenuto della tabella non si applica al metodo **Load** se **XmlDocument** viene caricato da un **XmlReader**.  
  
|XmlResolver, proprietà|Funzione|Note|  
|----------------------------|--------------|----------|  
|Nello scenario semi\-trusted è possibile impostare la proprietà **XmlResolver** solo su null.|Verrà creata un'istanza di un **XmlUrlResolver** con credenziali **null** e verrà usata dal documento **XmlDocument** nella risoluzione dei nomi di file, nell'individuazione delle DTD, delle entità e degli schemi esterni. Le credenziali **null** verranno usate per la modifica dei nodi.|Il comportamento è identico a quello che si verifica quando la proprietà **XmlResolver** non viene impostata, bensì lasciata nello stato predefinito.<br /><br /> **XmlDocument** consente di usare autorizzazioni anonime per tutte le azioni.|  
|La proprietà è impostata su **null** \(**Nothing** in Microsoft Visual Basic .NET\).|Non è supportata alcuna funzionalità che richiede una risorsa esterna, ad esempio l'individuazione di uno schema esterno o di una DTD.  Le entità esterne non verranno risolte e non saranno supportate le funzionalità di modifica, quali l'inserimento di nodi di entità che richiedono la risoluzione.|Quando la proprietà è **null**, il comportamento è identico, indipendentemente dal fatto che **XmlDocument** sia completamente attendibile o semi\-trusted.|  
|La proprietà non viene impostata, ma rimane nello stato predefinito.|Verrà creata un'istanza di un **XmlUrlResolver** con credenziali **null** e verrà usata dal documento **XmlDocument** nella risoluzione dei nomi di file, nell'individuazione delle DTD, delle entità e degli schemi esterni. Le credenziali **null** verranno usate per la modifica dei nodi.|**XmlDocument** consente di usare autorizzazioni anonime per tutte le azioni.|  
  
 Il contenuto della tabella si applica al metodo **XmlDocument.Load** quando l'input di **Load** è **XmlReader** e **XmlDocument** è semi\-trusted.  
  
|XmlResolver, proprietà|Funzione|Note|  
|----------------------------|--------------|----------|  
|La classe **XmlResolver** usata dall'**XmlDocument** è la stessa usata dall'**XmlReader**.|**XmlDocument** usa l'**XmlResolver** assegnato a **XmlReader**.<br /><br /> Non è possibile impostare la proprietà **XmlDocument.Resolver**, indipendentemente dal livello di attendibilità di **XmlDocument**, poiché ottiene un **XmlResolver** da **XmlReader**.  Non è possibile eseguire l'override delle impostazioni **XmlResolver** di **XmlReader** impostando la proprietà **XmlResolver** di **XmlDocument**.|**XmlReader** può essere **XmlTextReader**, un tipo <xref:System.Xml.XmlReader> di convalida o un lettore personalizzato.  Se il lettore usato supporta la risoluzione di entità, le entità esterne vengono risolte.  I riferimenti alle entità non vengono risolti se il lettore passato non li supporta.|  
  
 Impostando XmlResolver in modo che contenga le credenziali corrette sarà possibile accedere alle risorse esterne.  
  
> [!NOTE]
>  Non vi è modo di recuperare la proprietà **XmlResolver**.  In questo modo è possibile impedire all'utente di riutilizzare un **XmlResolver** sul quale sono state impostate le credenziali.  Inoltre, se viene usato **XmlTextReader** o un tipo <xref:System.Xml.XmlReader> di convalida per caricare **XmlDocument** e quest'ultimo ha un sistema di risoluzione impostato, i sistemi di risoluzione di questi lettori non vengono memorizzati nella cache da **XmlDocument** dopo la fase **Load**, in quanto anche tale operazione presenta un rischio per la sicurezza.  
  
 Per altre informazioni, vedere la sezione Note della pagina di riferimento <xref:System.Xml.XmlResolver>.  
  
## Vedere anche  
 [Modello DOM \(Document Object Model\) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)