---
title: "Progettazione di costruttori | Microsoft Docs"
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
  - "indicazioni per la progettazione di membro, costruttori"
  - "costruttori, linee guida di progettazione"
  - "costruttori di istanza"
  - "costruttori di tipo"
  - "membri virtual"
  - "costruttori, tipi"
  - "costruttori predefiniti"
  - "costruttori statici"
ms.assetid: b4496afe-5fa7-4bb0-85ca-70b0ef21e6fc
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Progettazione di costruttori
Esistono due tipi di costruttori: digitare costruttori e i costruttori di istanza.  
  
 Costruttori di tipo sono statici e vengono eseguiti da Common Language Runtime prima che venga utilizzato il tipo. Costruttori di istanza eseguire quando viene creata un'istanza di un tipo.  
  
 Costruttori di tipo non accettano parametri. Costruttori di istanza possono. Costruttori di istanza che non accettano parametri vengono definiti costruttori predefiniti.  
  
 I costruttori sono il modo più semplice per creare istanze di un tipo. Maggior parte degli sviluppatori sarà ricerca e tenta di utilizzare un costruttore prima considerano modi alternativi per la creazione di istanze \(ad esempio i metodi factory\).  
  
 **✓ PROVARE** fornendo semplice, in teoria predefinita, i costruttori.  
  
 Un semplice costruttore con un numero molto ridotto di parametri e tutti i parametri sono primitive o enum. Tali costruttori semplici aumentano l'utilizzabilità di framework.  
  
 **✓ PROVARE** tramite un metodo factory statico anziché un costruttore se la semantica dell'operazione desiderata non corrispondenza direttamente alla costruzione di una nuova istanza, oppure se le linee guida per la progettazione costruttore costruttori risultano inappropriate.  
  
 **✓ si** utilizzare i parametri del costruttore come tasti di scelta rapida per l'impostazione delle proprietà principali.  
  
 Non vi sarà alcuna differenza semantica tra utilizzando il costruttore vuoto seguito da un set di proprietà e utilizzando un costruttore con più argomenti.  
  
 **✓ si** se vengono utilizzati i parametri del costruttore semplicemente impostare la proprietà, utilizzare lo stesso nome per i parametri del costruttore e una proprietà.  
  
 L'unica differenza tra tali parametri e le proprietà debba essere maiuscole e minuscole.  
  
 **✓ si** un lavoro minimo nel costruttore.  
  
 I costruttori non occorre eseguire la quantità di lavoro diverso da acquisizione i parametri del costruttore. Il costo di qualsiasi altra elaborazione deve essere ritardato solo quando necessario.  
  
 **✓ si** generare eccezioni dai costruttori di istanza, se appropriato.  
  
 **✓ si** dichiarare in modo esplicito il costruttore predefinito pubblico nelle classi, se tale costruttore è obbligatorio.  
  
 Se si non dichiarano alcun costruttore in modo esplicito su un tipo, molte lingue \(ad esempio c\#\) aggiungerà automaticamente un costruttore predefinito pubblico. \(Le classi astratte ottenere un costruttore protetto\).  
  
 Aggiunta di un costruttore con parametri a una classe impedisce al compilatore di aggiungere il costruttore predefinito. Questo causa spesso modifiche accidentali.  
  
 **X evitare** definendo in modo esplicito i costruttori predefiniti sulle strutture.  
  
 Creazione di matrici in questo modo più veloce, in quanto se il costruttore predefinito non è definito, non deve essere eseguito su ogni slot nella matrice. Si noti che molti compilatori, tra cui c\#, non consentano strutture possono disporre di costruttori senza parametri per questo motivo.  
  
 **X evitare** chiamare membri virtuali su un oggetto nel relativo costruttore.  
  
 La chiamata di un membro virtuale determina la sostituzione più derivata da chiamare, anche se il costruttore del tipo più derivato non è stato completamente eseguito ancora.  
  
### Linee guida di costruttore di tipo  
 **✓ si** rendere privato costruttori statici.  
  
 Un costruttore statico, denominato anche costruttore di classe, viene utilizzato per inizializzare un tipo. CLR chiama il costruttore statico prima viene creata la prima istanza del tipo o di qualsiasi membro statico su quel tipo. L'utente non ha alcun controllo su quando viene chiamato il costruttore statico. Se un costruttore statico non è privato, può essere chiamato da codice diverso da CLR. A seconda delle operazioni eseguite nel costruttore, questo può causare comportamenti imprevisti. Il compilatore c\# forza costruttori statici come privato.  
  
 **X non** generare eccezioni dai costruttori statici.  
  
 Se viene generata un'eccezione da un costruttore di tipo, il tipo non è utilizzabile nel dominio applicazione corrente.  
  
 **✓ PROVARE** inizializzare i campi statici inline anziché in modo esplicito utilizzando costruttori statici, perché il runtime è in grado di ottimizzare le prestazioni dei tipi che non dispongono di un costruttore statico definito in modo esplicito.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)