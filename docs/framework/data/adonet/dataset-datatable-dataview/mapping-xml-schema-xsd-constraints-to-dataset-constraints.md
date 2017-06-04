---
title: "Mapping dei vincoli di XML Schema (XSD) ai vincoli del DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d0d1a4b-9104-434f-ac04-6c01ab5716b5
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Mapping dei vincoli di XML Schema (XSD) ai vincoli del DataSet
Lo schema XSD \(XML Schema Definition Language\) consente di specificare vincoli sugli elementi e sugli attributi in esso definiti.  Quando si esegue il mapping di un XML Schema a uno schema relazionale in un oggetto <xref:System.Data.DataSet>, viene eseguito il mapping dei vincoli di XML Schema ai vincoli relazionali appropriati nelle tabelle e nelle colonne del **DataSet**.  
  
 Contenuto della sezione viene illustrato il mapping dei seguenti vincoli di XML Schema:  
  
-   Il vincolo di univocità specificato mediante l'elemento **unique**.  
  
-   Il vincolo key specificato mediante l'elemento **key**.  
  
-   Il vincolo keyref specificato mediante l'elemento **keyref**.  
  
 Usando un vincolo su un elemento o su un attributo, si specificano determinate restrizioni relative ai valori dell'elemento in qualsiasi istanza del documento.  Ad esempio, l'applicazione di un vincolo key a un elemento figlio **CustomerID** di un elemento **Customer** nello schema indica che i valori dell'elemento figlio **CustomerID** devono essere univoci in qualsiasi istanza del documento e che i valori null non sono consentiti.  
  
 È anche possibile specificare vincoli tra elementi e attributi in un documento, in modo da stabilire una relazione all'interno del documento.  I vincoli key e keyref vengono usati nello schema per specificare i vincoli all'interno del documento, creando quindi una relazione tra gli elementi e gli attributi del documento.  
  
 Il processo di mapping consente di convertire tali vincoli dello schema in vincoli appropriati per le tabelle create all'interno del **DataSet**.  
  
## In questa sezione  
 [Mappare i vincoli univoci di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-unique-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Vengono descritti gli elementi di XML Schema usati per creare vincoli univoci in un **DataSet**.  
  
 [Mappare i vincoli key di XML Schema \(XSD\) ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-key-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Vengono descritti gli elementi di XML Schema usati per creare vincoli key \(vincoli univoci in cui non sono consentiti valori null\) in un **DataSet**.  
  
 [Mappare i vincoli di XML Schema \(XSD\) keyref ai vincoli del DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-keyref-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Vengono descritti gli elementi di XML Schema usati per creare vincoli keyref \(di chiave esterna\) in un **DataSet**.  
  
## Sezioni correlate  
 [Derivazione della struttura relazionale di un DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Viene descritta la struttura relazionale, o schema, di un **DataSet** creata da uno schema XSD \(XML Schema Definition Language\).  
  
 [Generazione delle relazioni del DataSet da XML Schema \(XSD\)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)  
 Vengono descritti gli elementi di XML Schema usati per creare relazioni tra le colonne delle tabelle in un **DataSet**.  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)