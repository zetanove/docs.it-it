---
title: "Livelli di attendibilit&#224; di sicurezza nell&#39;accesso alle risorse  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb5be924-317d-4d69-b33a-3d18ecfb9d6e
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Livelli di attendibilit&#224; di sicurezza nell&#39;accesso alle risorse 
Questo argomento descrive le restrizioni di accesso ai tipi di risorse esposti dallo spazio dei nomi <xref:System.Transactions>.  
  
 Nello spazio dei nomi <xref:System.Transactions> esistono tre livelli principali di attendibilità.I livelli di attendibilità sono definiti in base ai tipi di risorse esposti dallo spazio dei nomi <xref:System.Transactions> e in base al livello di attendibilità necessario ad accedere a tali risorse.Le risorse a cui lo spazio dei nomi <xref:System.Transactions> consente di accedere sono la memoria di sistema, le risorse a livello di processo condivise e le risorse a livello di sistema.I livelli sono:  
  
-   **AllowPartiallyTrustedCallers** \(APTCA\), per le applicazioni che utilizzano transazioni all'interno di un solo dominio applicazione.  
  
-   **DistributedTransactionPermission** \(DTP\), per le applicazioni che utilizzano transazioni distribuite.  
  
-   Per le risorse durevoli, le applicazioni di gestione della configurazione e le applicazioni di interoperabilità legacy.  
  
> [!NOTE]
>  Evitare di utilizzare contesti rappresentati per chiamare le interfacce di integrazione.  
  
## Livelli di attendibilità  
  
### AllowPartiallyTrustedCallers \(attendibilità parziale\)  
 L'assembly <xref:System.Transactions> può essere chiamato da codice parzialmente attendibile in quanto è stato contrassegnato con l'attributo **AllowPartiallyTrustedCallers**.Questo attributo sostanzialmente rimuove il flag implicito <xref:System.Security.Permissions.SecurityAction> dal set di autorizzazioni **FullTrust** che altrimenti viene assegnato automaticamente a ogni metodo accessibile pubblicamente di ogni tipo.Tuttavia, alcuni tipi e membri richiedono comunque autorizzazioni di livello superiore.  
  
 L'attributo APTCA consente alle applicazioni di utilizzare transazioni in un contesto di attendibilità parziale all'interno di un solo dominio applicazione.Ciò consente di utilizzare le transazioni per cui non è stata eseguita l'escalation nonché le integrazioni volatili allo scopo di eseguire la gestione degli errori.Si consideri ad esempio un'applicazione che utilizza una tabella hash transazionale.I dati possono essere aggiunti e rimossi dalla tabella hash mediante un'unica transazione.Se in seguito viene eseguito il rollback della transazione, tutte le modifiche apportate alla tabella hash tramite tale transazione possono essere annullate.  
  
### DistributedTransactionPermission  
 Quando viene eseguita l'escalation di una transazione dello spazio dei nomi <xref:System.Transactions> in modo che venga gestita mediante il gestore MSDTC, lo spazio dei nomi <xref:System.Transactions> richiede l'autorizzazione <xref:System.Transactions.DistributedTransactionPermission> per creare la transazione distribuita.Ciò significa che il codice che ha causato l'escalation della transazione \(ad esempio tramite la serializzazione o l'aggiunta di integrazioni durevoli\) deve disporre dell'autorizzazione DTP.Non è necessario che il codice che ha creato la transazione dello spazio dei nomi <xref:System.Transactions> disponga di questa autorizzazione.  
  
### FullTrust \(attendibilità totale\)  
 Questo livello di autorizzazione viene utilizzato per applicare restrizioni alle applicazioni che modificano risorse durevoli.In caso di errore, l'applicazione deve essere in grado di interagire con la gestione transazioni per eseguire il ripristino allo scopo di determinare il risultato finale della transazione e quindi aggiornare i dati definitivi.Questo tipo di applicazione è detto gestore di risorse durevole.Un classico esempio di questo tipo di applicazione è SQL.  
  
 Per consentire il ripristino, questo tipo di applicazione è in grado di utilizzare le risorse di sistema in modo definitivo.Ciò è dovuto al fatto che il gestore delle transazioni recuperabili deve ricordare le transazioni di cui è stato eseguito il commit finché non è in grado di confermare che tutti i gestori di risorse durevoli integrati nella transazione siano stati informati in merito al risultato.Pertanto, questo tipo di applicazione richiede attendibilità totale e deve essere eseguito solo se dispone del livello di attendibilità FullTrust.  
  
 Per ulteriori informazioni sulle integrazioni durevoli e sul ripristino, vedere gli argomenti [Integrazione di risorse come partecipanti a una transazione ](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md) e [Esecuzione del ripristino ](../../../../docs/framework/data/transactions/performing-recovery.md).  
  
 L'autorizzazione FullTrust deve essere concessa anche alle applicazioni che eseguono operazioni di interoperabilità legacy con COM\+.  
  
 Di seguito viene fornito un elenco di tipi e membri che non possono essere chiamati da codice parzialmente attendibile in quanto contrassegnati con l'attributo di sicurezza dichiarativa **FullTrust**.  
  
 `PermissionSetAttribute(SecurityAction.LinkDemand, Name := "FullTrust")`  
  
-   <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=fullName>  
  
-   <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A>  
  
-   <xref:System.Transactions.TransactionInterop>  
  
-   <xref:System.Transactions.TransactionManager.DistributedTransactionStarted>  
  
-   <xref:System.Transactions.HostCurrentTransactionCallback>  
  
-   <xref:System.Transactions.TransactionManager.Reenlist%2A>  
  
-   <xref:System.Transactions.TransactionManager.RecoveryComplete%2A>  
  
-   <xref:System.Transactions.TransactionScope.%23ctor%28System.Transactions.TransactionScopeOption%2CSystem.Transactions.TransactionOptions%2CSystem.Transactions.EnterpriseServicesInteropOption%29>  
  
 Solo il chiamante immediato è tenuto a possedere il set di autorizzazioni **FullTrust** per poter utilizzare i tipi o i metodi appena elencati.