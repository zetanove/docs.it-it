---
title: "Progettazione di eventi | Microsoft Docs"
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
  - "eventi precedenti"
  - "eventi [.NET Framework], linee guida di progettazione"
  - "indicazioni per la progettazione di membri, gli eventi"
  - "gestori eventi [.NET Framework], istruzioni di progettazione eventi"
  - "post-eventi"
  - "le firme, la gestione degli eventi"
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Progettazione di eventi
Gli eventi sono la forma più diffuso di callback \(costrutti che consentono il framework chiama codice utente\). Altri meccanismi di callback che includono membri accettando delegati, i membri virtuali e basata su interfaccia plug\-in. Dati di studi di utilizzabilità indicano che la maggior parte degli sviluppatori sono più familiarità con gli eventi che utilizzano altri meccanismi di callback. Gli eventi sono perfettamente integrati con Visual Studio e linguaggi.  
  
 È importante tenere presente che esistono due gruppi di eventi: eventi generati prima di uno stato delle modifiche del sistema, denominato eventi precedenti e gli eventi generati dopo uno stato di modifica, chiamati eventi successivi. Un esempio di un pre\-evento di `Form.Closing`, che viene generato prima della chiusura di un form. Un esempio di un post\-evento di `Form.Closed`, che viene generato dopo la chiusura di un form.  
  
 **✓ si** viene utilizzato il termine "generazione" per gli eventi anziché "fire" o "trigger".  
  
 **✓ si** utilizzare <xref:System.EventHandler%601?displayProperty=fullName> anziché creare manualmente nuovi delegati da utilizzare come gestori eventi.  
  
 **✓ PROVARE** utilizza una sottoclasse di <xref:System.EventArgs> come argomento dell'evento, a meno che non si è assolutamente certi l'evento non sarà mai necessario eseguire tutti i dati per il metodo gestione eventi, nel qual caso è possibile utilizzare il `EventArgs` digitare direttamente.  
  
 Se si include un'API con `EventArgs` direttamente, non sarà in grado di aggiungere tutti i dati devono essere trasportati senza compromettere la compatibilità con l'evento. Se si utilizza una sottoclasse, anche se inizialmente completamente vuote, sarà possibile aggiungere proprietà alla sottoclasse quando necessario.  
  
 **✓ si** utilizzare un metodo virtuale protetto per generare ciascun evento. Questa opzione è disponibile solo per gli eventi non statici su classi non sealed, non per le strutture, le classi sealed o eventi statici.  
  
 Lo scopo del metodo è fornire un modo per una classe derivata gestire l'evento utilizzando una sostituzione. Si esegue l'override è un modo più flessibile, veloce e più naturale per gestire gli eventi di classe di base nelle classi derivate. Per convenzione, il nome del metodo deve iniziare con "On" e da seguire con il nome dell'evento.  
  
 La classe derivata può scegliere di non chiamare l'implementazione di base del metodo nel relativo override. Prevedere questa possibilità non includendo qualsiasi elaborazione nel metodo che è necessario per la classe base funzionare correttamente.  
  
 **✓ si** accettano un parametro al metodo protetto che genera un evento.  
  
 Il parametro deve essere denominato `e` e deve essere digitato come la classe di argomenti di evento.  
  
 **X non** passare null come mittente quando viene generato un evento non statico.  
  
 **✓ si** passare null come mittente quando viene generato un evento statico.  
  
 **X non** passare null come parametro di dati dell'evento quando viene generato un evento.  
  
 È necessario passare `EventArgs.Empty` Se non si desidera passare i dati per il metodo di gestione di eventi. È previsto che questo parametro non deve essere null.  
  
 **✓ PROVARE** la generazione di eventi che l'utente finale può annullare. Si applica solo agli eventi precedenti.  
  
 Utilizzare <xref:System.ComponentModel.CancelEventArgs?displayProperty=fullName> o la relativa sottoclasse come argomento dell'evento per consentire all'utente di annullare gli eventi.  
  
### Progettazione di gestori eventi personalizzati  
 Vi sono casi in cui `EventHandler<T>` non può essere utilizzato, ad esempio quando è necessario che il framework lavorare con le versioni precedenti di CLR, che non supporta i Generics. In questi casi, potrebbe essere necessario progettare e sviluppare un delegato del gestore eventi personalizzato.  
  
 **✓ si** utilizzare un tipo restituito void per i gestori eventi.  
  
 Un gestore eventi può richiamare più metodi, anche su più oggetti di gestione di eventi. Se la gestione degli eventi metodi fosse consentito restituire un valore, non ci sarebbero più valori restituiti per ogni chiamata di eventi.  
  
 **✓ si** utilizzare `object` come il tipo del primo parametro del gestore eventi e denominarla `sender`.  
  
 **✓ si** utilizzare <xref:System.EventArgs?displayProperty=fullName> o la relativa sottoclasse come il tipo del secondo parametro del gestore eventi e denominarla `e`.  
  
 **X non** avere più di due parametri sui gestori eventi.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)