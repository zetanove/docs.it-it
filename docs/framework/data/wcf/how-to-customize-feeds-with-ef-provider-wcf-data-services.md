---
title: "Procedura: personalizzare feed con il provider di Entity Framework (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, personalizzazione"
  - "WCF Data Services, personalizzazione di feed"
ms.assetid: fd16272e-36f2-415e-850e-8a81f2b17525
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: personalizzare feed con il provider di Entity Framework (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente di personalizzare la serializzazione Atom in una risposta del servizio dati in modo che venga eseguito il mapping delle proprietà di un'entità agli elementi inutilizzati definiti nel protocollo AtomPub.  In questo argomento viene illustrato come definire attributi di mapping per i tipi di entità in un modello di dati definito in un file con estensione edmx tramite il provider di Entity Framework.  Per altre informazioni, vedere [Personalizzazione di feed](../../../../docs/framework/data/wcf/feed-customization-wcf-data-services.md).  
  
 In questo argomento si modificherà manualmente il file con estensione edmx generato dallo strumento contenente il modello di dati.  Il file deve essere modificato manualmente in quanto le estensioni al modello di dati non sono supportate da Entity Designer.  Per altre informazioni sul file con estensione edmx generato dagli strumenti di Entity Data Model, vedere [.edmx File Overview](http://msdn.microsoft.com/it-it/f4c8e7ce-1db6-417e-9759-15f8b55155d4).  Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
### Per modificare manualmente il file Northwind.edmx per aggiungere attributi di personalizzazione dei feed  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file `Northwind.edmx`, quindi scegliere **Apri con**.  
  
2.  Nella finestra di dialogo **Apri con \- Northwind.edmx** selezionare **Editor XML**, quindi scegliere **OK**.  
  
3.  Individuare l'elemento `ConceptualModels` e sostituire il tipo di entità `Customers` esistente con l'elemento seguente che contiene gli attributi per il mapping della personalizzazione dei feed:  
  
     [!code-xml[Astoria Custom Feeds#EdmFeedCustomers](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria custom feeds/xml/northwind.csdl#edmfeedcustomers)]  
  
4.  Salvare le modifiche e chiudere il file Northwind.edmx.  
  
5.  \(Facoltativo\) Fare clic con il pulsante destro del mouse sul file Northwind.edmx, quindi scegliere **Esegui strumento personalizzato**.  
  
     Il file del livello di oggetti verrà rigenerato, poiché potrebbe essere necessario.  
  
6.  Ricompilare il progetto.  
  
## Esempio  
 Nell'esempio precedente per l'URI `http://myservice/` `Northwind.svc/Customers('ALFKI')` viene restituito il risultato seguente.  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria custom feeds/xml/edmfeedresult.xml#edmfeedresult)]  
  
## Vedere anche  
 [Provider di Entity Framework](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md)