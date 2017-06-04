---
title: "Estensione del sistema di metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "estensione di metadati [WCF]"
ms.assetid: 8c6b3b00-61b8-4589-8fa5-546cc33719bf
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Estensione del sistema di metadati
Il sistema dei metadati di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è un gruppo di classi e interfacce che rappresentano i metadati necessari per implementare applicazioni basate sul servizio.Modificare o estendere le classi o implementare e configurare le interfacce per esportare e importare metadati personalizzati quali estensioni WSDL \(Web Services Description Language\) o asserzioni di WS\-PolicyAttachment personalizzate.  
  
## In questa sezione  
 [Esportazione di metadati personalizzati per un'estensione WCF](../../../../docs/framework/wcf/extending/exporting-custom-metadata-for-a-wcf-extension.md)  
 Viene descritto come implementare e utilizzare l'interfaccia <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> per incorporare asserzioni di criteri personalizzate nei documenti WSDL.  
  
 [Importazione di metadati personalizzati per un'estensione WCF](../../../../docs/framework/wcf/extending/importing-custom-metadata-for-a-wcf-extension.md)  
 Viene descritto come implementare e utilizzare l'interfaccia <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName> per leggere e rispondere ad asserzioni di criteri personalizzate in documenti WSDL.  
  
 [Pubblicazione e recupero di metadati su un'associazione personalizzata](../../../../docs/framework/wcf/extending/publishing-and-retrieving-metadata-over-a-custom-binding.md)  
 Viene descritto come scambiare metadati su associazioni personalizzate.