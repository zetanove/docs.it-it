---
title: "Thread Local Storage: Thread-Relative Static Fields and Data Slots | Microsoft Docs"
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
  - "threading [.NET Framework], local storage"
  - "threading [.NET Framework], thread-relative static fields"
  - "local thread storage"
  - "TLS"
ms.assetid: c633a4dc-a790-4ed1-96b5-f72bd968b284
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Thread Local Storage: Thread-Relative Static Fields and Data Slots
È possibile utilizzare l'archiviazione locale del thread \(TLS\) per archiviare dati univoci per un thread e un dominio applicazione.  .NET Framework fornisce due modalità per utilizzare TLS gestito: campi statici relativi ai thread e slot di dati.  
  
-   Utilizzare i campi statici relativi ai thread \(campi `Shared` relativi ai thread in Visual Basic\) se è possibile prevedere le esigenze specifiche in fase di compilazione.  I campi statici relativi ai thread forniscono le prestazioni migliori.  Offrono inoltre il vantaggio di controllare il tipo in fase di compilazione.  
  
-   Se i requisiti effettivi possono essere individuati solo in fase di esecuzione, utilizzare gli slot di dati.  Gli slot di dati sono più lenti e scomodi da utilizzare dei campi statici relativi ai thread e i dati vengono archiviati come tipo <xref:System.Object>, pertanto è necessario eseguirne il cast al tipo corretto prima dell'utilizzo.  
  
 In C\+\+ non gestito si utilizza `TlsAlloc` per allocare gli slot dinamicamente e `__declspec(thread)` per dichiarare che una variabile deve essere allocata in una archiviazione relativa ai thread.  I campi statici relativi ai thread e gli slot di dati forniscono la versione gestita di questo comportamento.  
  
 In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] è possibile utilizzare la classe <xref:System.Threading.ThreadLocal%601?displayProperty=fullName> per creare oggetti locali di thread inizializzati in modo differito quando l'oggetto viene utilizzato per la prima volta.  Per ulteriori informazioni, vedere [Lazy Initialization](../../../docs/framework/performance/lazy-initialization.md).  
  
## Unicità dei dati in TLS gestito  
 Indipendentemente dal fatto che si utilizzino i campi statici relativi ai thread o gli slot di dati, i dati in TLS gestito sono univoci per la combinazione di thread e dominio applicazione.  
  
-   All'interno di un dominio applicazione, un thread non può modificare dati da un altro thread, anche quando entrambi utilizzano lo stesso campo o slot.  
  
-   Quando un thread accede allo stesso campo o slot dai più domini dell'applicazione, viene mantenuto un valore separato in ogni dominio applicazione.  
  
 Ad esempio, se un thread imposta il valore di un campo statico del thread, immette un altro dominio applicazione e quindi recupera il valore del campo, il valore recuperato nel secondo dominio applicazione differisce dal valore nel primo dominio applicazione.  L'impostazione di un nuovo valore per il campo nel secondo dominio applicazione non influisce sul valore del campo nel primo dominio applicazione.  
  
 Similmente, quando un thread ottiene lo stesso slot di dati denominato in due domini applicazione diversi, i dati nel primo dominio applicazione restano indipendenti dai dati nel secondo dominio applicazione.  
  
## Campi statici relativi ai thread  
 Se si è certi che i dati sono sempre univoci in una combinazione di thread e dominio applicazione, applicare l'attributo <xref:System.ThreadStaticAttribute> al campo statico.  Utilizzare il campo come qualsiasi altro campo statico.  I dati nel campo sono univoci per ogni thread che li utilizza.  
  
 I campi statici relativi ai thread garantiscono prestazioni migliori rispetto agli slot di dati e offrono il vantaggio del controllo del tipo nella fase di compilazione.  
  
 È importante notare che qualsiasi codice del costruttore di classe verrà eseguito sul primo thread nel primo contesto che accede al campo.  In tutti gli altri thread o contesti nello stesso dominio applicazione, i campi verranno inizializzati su `null` \(`Nothing` in Visual Basic\) se sono tipi di riferimento o sui valori predefiniti se sono tipi valore.  Di conseguenza non è opportuno basarsi sui costruttori delle classi per inizializzare i campi statici relativi ai thread.  Al contrario, evitare l'inizializzazione di campi statici relativi ai thread e supporre che vengano inizializzati su `null` \(`Nothing`\) o sui valori predefiniti.  
  
## Slot dei dati  
 .NET Framework fornisce slot di dati dinamici univoci per una combinazione di thread e dominio applicazione.  Esistono due tipi di slot di dati: con e senza nome.  Entrambi vengono implementati utilizzando la struttura <xref:System.LocalDataStoreSlot>.  
  
-   Per creare uno slot di dati denominato, utilizzare il metodo <xref:System.Threading.Thread.AllocateNamedDataSlot%2A?displayProperty=fullName> o <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=fullName>.  Per ottenere un riferimento a uno slot denominato esistente, passare il nome al metodo <xref:System.Threading.Thread.GetNamedDataSlot%2A>.  
  
-   Per creare uno slot di dati senza nome, utilizzare il metodo <xref:System.Threading.Thread.AllocateDataSlot%2A?displayProperty=fullName>.  
  
 Per gli slot denominati e senza nome, utilizzare i metodi <xref:System.Threading.Thread.SetData%2A?displayProperty=fullName> e <xref:System.Threading.Thread.GetData%2A?displayProperty=fullName> per impostare e recuperare le informazioni nello slot.  Si tratta di metodi statici che agiscono sempre sui dati per il thread che li sta eseguendo.  
  
 Gli slot denominati possono essere comodi, perché è possibile recuperare lo slot quando è necessario passando il nome al metodo <xref:System.Threading.Thread.GetNamedDataSlot%2A>, anziché mantenere un riferimento a uno slot senza nome.  Tuttavia, se un altro componente utilizza lo stesso nome per la memoria relativa ai thread e un thread esegue codice sia dal componente in questione che dall'altro componente, i due componenti possono danneggiare l'uno i dati dell'altro. Questo scenario presuppone che entrambi componenti siano in esecuzione nello stesso dominio applicazione e che non siano progettati per condividere gli stessi dati.  
  
## Vedere anche  
 <xref:System.ContextStaticAttribute>   
 <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=fullName>   
 <xref:System.ThreadStaticAttribute>   
 <xref:System.Runtime.Remoting.Messaging.CallContext>   
 [Threading](../../../docs/standard/threading/index.md)