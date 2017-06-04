---
title: "Progettazione di propriet&#224; | Microsoft Docs"
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
  - "indicazioni per la progettazione di membri, proprietà"
  - "proprietà [.NET Framework], linee guida di progettazione"
ms.assetid: 127cbc0c-cbed-48fd-9c89-7c5d4f98f163
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Progettazione di propriet&#224;
Anche se le proprietà sono tecnicamente molto simili ai metodi, sono molto diversi in termini relativi scenari di utilizzo. Essi dovrebbero essere considerate come campi intelligenti. Hanno la sintassi per la chiamata di campi e la flessibilità dei metodi.  
  
 **✓ si** creare proprietà di sola ricezione se il chiamante non deve essere in grado di modificare il valore della proprietà.  
  
 Tenere presente che se il tipo di proprietà è un tipo di riferimento modificabile, il valore della proprietà può essere modificato anche se la proprietà è di sola.  
  
 **X non** forniscono solo set di proprietà o proprietà con setter con accessibilità più ampia rispetto al metodo Get.  
  
 Ad esempio, non utilizzare proprietà con un setter pubblico e un metodo di richiamo protetto.  
  
 Se il metodo Get della proprietà non può essere fornito, implementare la funzionalità di un metodo. È consigliabile iniziare con il nome del metodo `Set` e seguire con ciò che si avrebbero denominato della proprietà. Ad esempio, <xref:System.AppDomain> ha un metodo denominato `SetCachePath` anziché una set di proprietà di sola `CachePath`.  
  
 **✓ si** forniscono i valori predefiniti appropriati per tutte le proprietà, assicurandosi che le impostazioni predefinite non comportano una falla o codice particolarmente inefficiente.  
  
 **✓ si** consente di proprietà da impostare in qualsiasi ordine, anche se il risultato è un stato temporaneo non valido dell'oggetto.  
  
 È comune per due o più delle proprietà correlate a un punto in cui alcuni valori di una proprietà potrebbero essere non validi in base ai valori di altre proprietà sull'oggetto stesso. In questi casi, le eccezioni derivanti da stato non valido devono essere rimandate fino a quando le proprietà correlate vengono effettivamente utilizzate insieme dall'oggetto.  
  
 **✓ si** mantiene il valore precedente se un setter delle proprietà genera un'eccezione.  
  
 **X evitare** la generazione di eccezioni da metodi get di proprietà.  
  
 Metodi get di proprietà devono essere operazioni semplici e non devono avere le precondizioni. Se un metodo Get può generare un'eccezione, probabilmente deve essere riprogettata per un metodo. Si noti che questa regola non sono valide per gli indicizzatori, in cui è prevista eccezioni come risultato di convalida gli argomenti.  
  
### Progettazione di proprietà indicizzate  
 Una proprietà indicizzata è una proprietà speciale che può disporre di parametri e può essere chiamata con una sintassi speciale simile per l'indicizzazione della matrice.  
  
 Proprietà indicizzate vengono comunemente definite come indicizzatori. Gli indicizzatori devono essere utilizzati solo nelle API che forniscono l'accesso agli elementi in una raccolta logica. Ad esempio, una stringa è un insieme di caratteri e l'indicizzatore in <xref:System.String?displayProperty=fullName> è stato aggiunto per accedere ai relativi caratteri.  
  
 **✓ PROVARE** tramite gli indicizzatori per fornire l'accesso ai dati archiviati in una matrice interna.  
  
 **✓ PROVARE** fornire degli indicizzatori in tipi che rappresentano raccolte di elementi.  
  
 **X evitare** utilizzando le proprietà con più di un parametro indicizzate.  
  
 Se la progettazione richiede più parametri, verificare che la proprietà rappresenta una funzione di accesso a un insieme logico. In caso contrario, utilizzare i metodi. È consigliabile iniziare con il nome del metodo `Get` o `Set`.  
  
 **X evitare** indicizzatori con tipi di parametro diverso da <xref:System.Int32?displayProperty=fullName>, <xref:System.Int64?displayProperty=fullName>, <xref:System.String?displayProperty=fullName>, <xref:System.Object?displayProperty=fullName>, o un'enumerazione.  
  
 Se la progettazione richiede altri tipi di parametri, rivalutare attentamente se l'API rappresenta una funzione di accesso a un insieme logico. In caso contrario, utilizzare un metodo. È consigliabile iniziare con il nome del metodo `Get` o `Set`.  
  
 **✓ si** utilizzare il nome `Item` per proprietà indicizzate, a meno che non è un nome evidentemente più appropriato \(ad esempio, vedere il <xref:System.String.Chars%2A> proprietà `System.String`\).  
  
 In c\#, gli indicizzatori sono per impostazione predefinita denominato Item. Il <xref:System.Runtime.CompilerServices.IndexerNameAttribute> può essere utilizzato per personalizzare questo nome.  
  
 **X non** fornire sia un indicizzatore e metodi che sono semanticamente equivalenti.  
  
 **X non** fornire più di una famiglia di indicizzatori overload in un tipo.  
  
 Tale requisito viene applicato dal compilatore c\#.  
  
 **X non** non predefinite utilizzare proprietà indicizzate.  
  
 Tale requisito viene applicato dal compilatore c\#.  
  
### Eventi di notifica di modifica proprietà  
 Talvolta è utile fornire un evento per avvisare l'utente delle modifiche in un valore della proprietà. Ad esempio, `System.Windows.Forms.Control` Genera un `TextChanged` eventi quando il valore della relativa `Text` proprietà è stata modificata.  
  
 **✓ PROVARE** la generazione di modificare gli eventi di notifica quando vengono modificati i valori delle proprietà nelle API di alto livello \(in genere Progettazione componenti\).  
  
 Se è presente uno scenario valido per un utente di sapere quando una proprietà di un oggetto in fase di modifica, l'oggetto deve generare un evento di notifica di modifica per la proprietà.  
  
 Tuttavia, è probabilmente non vale la pena l'overhead per generare tali eventi per le API di basso livello, ad esempio tipi di base o raccolte. Ad esempio, <xref:System.Collections.Generic.List%601> non genererebbe tali eventi quando viene aggiunto un nuovo elemento all'elenco e `Count` le modifiche alle proprietà.  
  
 **✓ PROVARE** la generazione di eventi di notifica quando cambia il valore di una proprietà tramite forze esterne di modifica.  
  
 Se il valore della proprietà viene modificato mediante forze esterne \(in modo diverso da chiamando i metodi sull'oggetto\), genera gli eventi indicano allo sviluppatore che il valore viene modificato e che è stato modificato. Un buon esempio è la `Text` proprietà di un controllo casella di testo. Quando l'utente digita del testo in un `TextBox`, il valore della proprietà viene modificata automaticamente.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Indicazioni per la progettazione di membri](../../../docs/standard/design-guidelines/member.md)   
 [Linee guida](../../../docs/standard/design-guidelines/index.md)