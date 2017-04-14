---
title: "Apprendimento tramite le procedure dettagliate | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8ae2965-6a49-4155-89b0-7fab2c488ab1
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Apprendimento tramite le procedure dettagliate
Nella documentazione di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sono disponibili diverse procedure dettagliate.  In questo argomento vengono discussi alcuni problemi generali relativi alle procedure, inclusa la risoluzione dei problemi, e vengono forniti i collegamenti a diverse procedure dettagliate di base per acquisire familiarità con [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
> [!NOTE]
>  Nelle procedure dettagliate disponibili in questa sezione della Guida introduttiva viene esposto il codice di base che supporta la tecnologia [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  In pratica, si useranno i progetti di [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] e Windows Form per implementare le applicazioni [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Nella documentazione di [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] vengono forniti esempi e procedure dettagliate a questo scopo.  
  
## Procedure dettagliate della Guida introduttiva  
 In questa sezione sono disponibili diverse procedure dettagliate  basate sul database di esempio Northwind, in cui vengono presentate passo passo e con minime complessità le funzionalità di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 Di seguito è riportato l'ordine di esecuzione tipico che si consiglia di seguire:  
  
|Obiettivo|Visual Basic|C\#|  
|---------------|------------------|---------|  
|Creare una classe di entità ed eseguire una semplice query.|[Procedura dettagliata: modello a oggetti e query semplici \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-visual-basic.md)|[Procedura dettagliata: modello a oggetti e query semplici \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-simple-object-model-and-query-csharp.md)|  
|Aggiungere una seconda classe ed eseguire una query più complessa.<br /><br /> Richiede il completamento della procedura dettagliata precedente.|[Procedura dettagliata: esecuzione di query tra relazioni \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-visual-basic.md)|[Procedura dettagliata: query tra relazioni \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-csharp.md)|  
|Aggiungere, modificare ed eliminare elementi nel database.|[Procedura dettagliata: modifica dei dati \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-visual-basic.md)|[Procedura dettagliata: modifica dei dati \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-manipulating-data-csharp.md)|  
|Usare stored procedure.|[Procedura dettagliata: utilizzo delle sole stored procedure \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-visual-basic.md)|[Procedura dettagliata: utilizzo delle sole stored procedure \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-csharp.md)|  
  
## Generale  
 Le informazioni seguenti riguardano queste procedure dettagliate in generale:  
  
-   Ambiente: in ogni procedura dettagliata di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene usato [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] come ambiente di sviluppo integrato \(IDE\).  
  
-   Motori SQL: queste procedure dettagliate sono scritte per essere implementate tramite SQL Server Express.  Se non si dispone di SQL Server Express, è possibile scaricarlo gratuitamente.  Per altre informazioni, vedere [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  
  
    > [!NOTE]
    >  Nelle procedure dettagliate di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene usato un nome file come stringa di connessione.  La possibilità di specificare semplicemente un nome file è un aspetto pratico di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per gli utenti di SQL Server Express.  Prestare sempre attenzione ai problemi di sicurezza.  Per altre informazioni, vedere [Sicurezza in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/security-in-linq-to-sql.md).  
  
-   Per le procedure dettagliate di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è in genere richiesto il database di esempio Northwind.  Per altre informazioni, vedere [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  
  
-   Le finestre di dialogo e i comandi di menu visualizzati nelle procedure dettagliate potrebbero non corrispondere a quelli descritti nella Guida, in quanto dipendono dalle impostazioni o dall'edizione di [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] in uso.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
-   Per le procedure dettagliate che riguardano scenari a più livelli è necessario che il computer configurato come server sia diverso dal computer di sviluppo. Inoltre è necessario disporre delle autorizzazioni appropriate per accedere al server.  
  
-   Il nome della classe che in genere rappresenta la tabella Orders nel database di esempio Northwind è `[Order]`.  L'uso di caratteri di escape è obbligatorio, poiché `Order` è una parola chiave in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)].  
  
## Risoluzione dei problemi  
 Possono verificarsi errori di runtime in quanto non si dispone di sufficienti autorizzazioni per accedere ai database usati in queste procedure dettagliate.  Vedere i passaggi seguenti per risolvere il più comune di questi problemi.  
  
### Problemi di accesso  
 L'applicazione potrebbe tentare di accedere al database usando credenziali di accesso non accettate.  
  
##### Per verificare o modificare l'accesso al database  
  
1.  In Windows fare clic sul menu **Start**, scegliere **Tutti i programmi**, quindi **Microsoft SQL Server 2005**, **Strumenti di configurazione** e infine **Gestione configurazione SQL Server**.  
  
2.  Nel riquadro sinistro di **Gestione configurazione SQL Server** fare clic su **Servizi di SQL Server 2005**.  
  
3.  Nel riquadro destro fare clic con il pulsante destro del mouse su **SQL Server \(SQLEXPRESS\)**, quindi scegliere **Proprietà**.  
  
4.  Fare clic sulla scheda **Accesso** e verificare come viene effettuato l'accesso al server.  
  
     Nella maggior parte dei casi **Sistema locale** consente di accedere al server.  
  
     Se si apporta una modifica, fare clic su **Riavvia** per riavviare il servizio.  
  
### Protocolli  
 A volte i protocolli possono non essere impostati correttamente per l'accesso dell'applicazione al database.  Ad esempio, il protocollo **Named Pipes**, necessario per le procedure dettagliate in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], non è abilitato per impostazione predefinita.  
  
##### Per abilitare il protocollo Named Pipes  
  
1.  Nel riquadro sinistro di **Gestione configurazione SQL Server** espandere il nodo **Configurazione di rete SQL Server 2005**, quindi fare clic su **Protocolli per SQLEXPRESS**.  
  
2.  Nel riquadro destro verificare che il protocollo **Named Pipes** sia abilitato.  In caso contrario fare clic con il pulsante destro del mouse su **Named pipes**, quindi scegliere **Abilita**.  
  
     Sarà necessario arrestare e riavviare il servizio.  Eseguire i passaggi illustrati nel blocco successivo.  
  
### Arresto e riavvio del servizio  
 È necessario arrestare e riavviare i servizi per rendere effettive le modifiche.  
  
##### Per arrestare e riavviare il servizio  
  
1.  Nel riquadro sinistro di **Gestione configurazione SQL Server** fare clic su **Servizi di SQL Server 2005**.  
  
2.  Nel riquadro destro fare clic con il pulsante destro del mouse su **SQL Server \(SQLEXPRESS\)**, quindi scegliere **Interrompi**.  
  
3.  Fare clic con il pulsante destro del mouse su **SQL Server \(SQLEXPRESS\)**, quindi scegliere **Riavvia**.  
  
## Vedere anche  
 [Introduzione](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)