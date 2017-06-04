---
title: "Interoperabilit&#224; con transazioni COM+ ed Enterprise Services  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d0fd0d26-fe86-443b-b208-4d57d39fa4aa
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Interoperabilit&#224; con transazioni COM+ ed Enterprise Services 
Lo spazio dei nomi <xref:System.Transactions> supporta l'interoperabilità fra gli oggetti di transazione creati mediante questo spazio dei nomi e le transazioni create tramite COM\+.  
  
 L'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption> consente di specificare il livello di interoperabilità con COM\+ quando si crea una nuova istanza della classe <xref:System.Transactions.TransactionScope>.  
  
 Per impostazione predefinita, quando il codice dell'applicazione verifica la proprietà statica <xref:System.Transactions.Transaction.Current%2A>, lo spazio dei nomi <xref:System.Transactions> tenta di individuare una transazione non corrente, oppure un oggetto <xref:System.Transactions.TransactionScope> in cui la proprietà <xref:System.Transactions.Transaction.Current%2A> sia **null**.Se tale ricerca ha esito negativo, lo spazio dei nomi <xref:System.Transactions> tenta di individuare una transazione nel contesto COM\+.Si noti che anche se lo spazio dei nomi <xref:System.Transactions> rileva una transazione nel contesto COM\+, predilige comunque le transazioni native dello spazio dei nomi <xref:System.Transactions>.  
  
## Livelli di interoperabilità  
 L'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption> definisce i livelli di interoperabilità seguenti: <xref:System.Transactions.EnterpriseServicesInteropOption>, <xref:System.Transactions.EnterpriseServicesInteropOption> e <xref:System.Transactions.EnterpriseServicesInteropOption>.  
  
 La classe <xref:System.Transactions.TransactionScope> contiene costruttori che accettano come parametro l'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption>.  
  
 L'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> consente di non impostare alcuna interoperabilità fra i contesti <xref:System.EnterpriseServices> e gli ambiti di transazione.Dopo aver creato un oggetto <xref:System.Transactions.TransactionScope> con l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption>, le modifiche apportate alla proprietà <xref:System.Transactions.Transaction.Current%2A> non vengono riflesse nel contesto COM\+.Analogamente, le modifiche apportate alla transazione nel contesto COM\+ non vengono riflesse sulla proprietà <xref:System.Transactions.Transaction.Current%2A>.Si tratta della modalità di esecuzione più veloce per <xref:System.Transactions> poiché non esiste alcuna sincronizzazione aggiuntiva richiesta.<xref:System.Transactions.EnterpriseServicesInteropOption> è il valore predefinito utilizzato da <xref:System.Transactions.TransactionScope> con tutti i costruttori che non accettano <xref:System.Transactions.EnterpriseServicesInteropOption> come parametro.  
  
 Se si desidera combinare le transazioni dello spazio dei nomi <xref:System.EnterpriseServices> con la transazione di ambiente, è necessario utilizzare l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> o l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption>.Entrambi questi valori si basano sulla funzionalità Services without Components, e pertanto devono essere utilizzati in Windows XP Service Pack 2 o Windows Server 2003.  
  
 L'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> impone che la transazione di ambiente dello spazio dei nomi <xref:System.Transactions> corrisponda sempre a quella dello spazio dei nomi <xref:System.EnterpriseServices>.Ciò comporta la creazione di un nuovo contesto transazionale <xref:System.EnterpriseServices> e l'impostazione della transazione corrente dell'ambito <xref:System.Transactions.TransactionScope> come transazione corrente di tale contesto.Ne consegue che la transazione associata alla proprietà <xref:System.Transactions.Transaction.Current%2A> è completamente sincronizzata con la transazione associata alla proprietà <xref:System.EnterpriseServices.ContextUtil.Transaction%2A>.Poiché può essere necessario creare nuovi contesti COM\+, questo valore comporta una riduzione delle prestazioni.  
  
 L'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> specifica i requisiti seguenti:  
  
-   Quando si verifica la proprietà <xref:System.Transactions.Transaction.Current%2A>, lo spazio dei nomi <xref:System.Transactions> deve supportare le transazioni nel contesto COM\+ se rileva di essere in esecuzione in un contesto diverso da quello predefinito.Si noti che il contesto predefinito non può contenere alcuna transazione.In tal caso, pertanto, anche se è stata scelta l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption>, il sistema restituisce come <xref:System.Transactions.Transaction.Current%2A> la transazione memorizzata nell'archivio locale di thread utilizzato dallo spazio dei nomi <xref:System.Transactions>.  
  
-   Se si crea un nuovo oggetto <xref:System.Transactions.TransactionScope> e tale creazione si verifica in un contesto diverso da quello predefinito, la transazione corrente dell'oggetto <xref:System.Transactions.TransactionScope> deve essere riflessa in COM\+.In questo caso, il funzionamento dell'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> è analogo a quello dell'opzione <xref:System.Transactions.EnterpriseServicesInteropOption>, nel senso che viene creato un nuovo contesto COM\+.  
  
 Inoltre, quando si imposta la proprietà <xref:System.Transactions.Transaction.Current%2A>, sia nella modalità <xref:System.Transactions.EnterpriseServicesInteropOption> sia nella modalità <xref:System.Transactions.EnterpriseServicesInteropOption>, l'impostazione di <xref:System.Transactions.Transaction.Current%2A> non può essere eseguita in modo diretto.Se si tenta di impostare in modo diretto la proprietà <xref:System.Transactions.Transaction.Current%2A> il sistema genera un'eccezione <xref:System.InvalidOperationException>, a meno che tale impostazione venga eseguita tramite la creazione di un ambito <xref:System.Transactions.TransactionScope>.Il valore dell'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption> viene ereditato dai nuovi ambiti di transazione che non specificano in modo esplicito il valore da utilizzare.Ad esempio, se si crea un nuovo oggetto <xref:System.Transactions.TransactionScope> con l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> e quindi si crea un secondo oggetto <xref:System.Transactions.TransactionScope> senza specificare alcuna opzione dell'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption>, l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> viene impostata automaticamente anche per il secondo oggetto <xref:System.Transactions.TransactionScope>.  
  
 In breve, quando si crea un nuovo ambito di transazione, si applicano le regole seguenti:  
  
1.  Viene eseguita la verifica della proprietà <xref:System.Transactions.Transaction.Current%2A> per stabilire se esiste una transazione.Questa verifica comporta quanto segue:  
  
    -   Viene eseguita una verifica per stabilire se esiste un ambito.  
  
    -   Se esiste un ambito, viene eseguita una verifica del valore dell'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption> passato al momento della creazione iniziale dell'ambito.  
  
    -   Se l'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption> è impostata su <xref:System.Transactions.EnterpriseServicesInteropOption>, la transazione COM\+ \(ovvero la transazione dello spazio dei nomi <xref:System.EnterpriseServices>\) ha la precedenza sulla transazione dello spazio dei nomi <xref:System.Transactions> contenuta nell'archivio locale dei thread gestiti.  
  
         Se il valore è impostato su <xref:System.Transactions.EnterpriseServicesInteropOption>, la transazione dello spazio dei nomi <xref:System.Transactions> contenuta nell'archivio locale dei thread gestiti ha la precedenza.  
  
         Se il valore è <xref:System.Transactions.EnterpriseServicesInteropOption>, esiste una sola transazione ed è una transazione COM\+.  
  
2.  Viene eseguita una verifica del valore dell'enumerazione <xref:System.Transactions.TransactionScopeOption> passato dal costruttore dell'ambito <xref:System.Transactions.TransactionScope>.Ciò determina se occorre creare una nuova transazione.  
  
3.  Se occorre creare una nuova transazione, i valori dell'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption> comportano quanto segue:  
  
    -   <xref:System.Transactions.EnterpriseServicesInteropOption>: viene creata una transazione associata a un contesto COM\+.  
  
    -   <xref:System.Transactions.EnterpriseServicesInteropOption>: viene creata una transazione dello spazio dei nomi <xref:System.Transactions>.  
  
    -   <xref:System.Transactions.EnterpriseServicesInteropOption>: se esiste un contesto COM\+, viene creata una transazione che quindi viene associata a tale contesto.  
  
 Nella tabella seguente vengono riportati il contesto di ES \(Enterprise Services\) e un ambito transazionale che richiede una transazione che utilizza l'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption>.  
  
|Contesto di ES|None|Automatic|Full|  
|--------------------|----------|---------------|----------|  
|Contesto predefinito|Contesto predefinito|Contesto predefinito|Crea nuovo <br />contesto di transazione|  
|Contesto non predefinito|Preservazione del contesto client|Creazione di un nuovo contesto transazionale|Creazione di un nuovo contesto transazionale|  
  
 Nella tabella seguente viene riportata la transazione di ambiente in funzione del contesto <xref:System.EnterpriseServices> e un ambito transazionale che richiede una transazione che utilizza l'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption>.  
  
|Contesto di ES|Nessuno|Automatic|Full|  
|--------------------|-------------|---------------|----------|  
|Contesto predefinito|ST|ST|ES|  
|Contesto non predefinito|ST|ES|ES|  
  
 Nella tabella precedente:  
  
-   ST indica che la transazione di ambiente dell'ambito è gestita dallo spazio dei nomi <xref:System.Transactions>, indipendentemente dall'eventuale presenza di una transazione del contesto <xref:System.EnterpriseServices>.  
  
-   ES indica che la transazione di ambiente dell'ambito corrisponde alla transazione del contesto <xref:System.EnterpriseServices>.