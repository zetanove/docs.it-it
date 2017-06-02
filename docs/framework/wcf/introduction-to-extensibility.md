---
title: "Introduzione all&#39;estendibilit&#224; | Microsoft Docs"
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
  - "estensibilità [WCF]"
  - "WCF [WCF], estensibilità"
  - "Windows Communication Foundation [WCF], estensibilità"
ms.assetid: ef56c251-d63c-4b3f-944f-b0c67bfb0f68
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Introduzione all&#39;estendibilit&#224;
Il modello dell'applicazione [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] è progettato per soddisfare la maggior parte dei requisiti di comunicazione di qualsiasi applicazione distribuita.  Esistono tuttavia scenari che non sono supportati dal modello di applicazione predefinito né dalle implementazioni fornite dal sistema.  Il modello di estendibilità [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] deve supportare scenari personalizzati consentendo di modificare il comportamento del sistema a ogni livello, anche al punto di sostituire l'intero modello di applicazione.  In questo argomento vengono illustrate le varie aree di estensione e vengono forniti i collegamenti alle informazioni aggiuntive relative a ogni area.  
  
## Aree da estendere  
 È possibile estendere:  
  
-   La fase di esecuzione dell'applicazione.  Estende la distribuzione e l'elaborazione di messaggi per l'applicazione.  Quest'area include anche l'estensione del sistema di sicurezza, del sistema dei metadati, del sistema della serializzazione e delle associazioni ed elementi di associazione che connettono l'applicazione al sistema di canali sottostante.  
  
-   Il canale e la fase di esecuzione del canale.  Estende il sistema che funziona al livello del messaggio, fornendo protocollo, trasporto e supporto di codifica.  
  
-   La fase di esecuzione dell'host.  Estende la relazione del dominio dell'applicazione host alla fase di esecuzione del canale e dell'applicazione.  
  
### Estensione della fase di esecuzione dell'applicazione  
 Nelle applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] viene fatta distinzione tra i messaggi destinati a un canale corrispondente e quelli destinati all'applicazione stessa.  I messaggi del canale supportano alcune funzionalità correlate al canale, ad esempio quella che consente di stabilire una conversazione protetta o una sessione affidabile.  Questi messaggi non sono disponibili nella fase di esecuzione dell'applicazione. Vengono elaborati prima che venga coinvolto il livello dell'applicazione.  
  
 I messaggi dell'applicazione contengono dati destinati a un'operazione client o di servizio creata personalmente o dal cliente.  Questi messaggi sono disponibili nel sistema di estensione al livello dell'applicazione in formato messaggio o oggetto, a seconda delle esigenze specifiche.  
  
 Tutti i messaggi passano attraverso il sistema di canali. Solo i messaggi dell'applicazione vengono passati dal sistema di canali nell'applicazione.  Per creare una nuova funzionalità a livello di canale, è necessario estendere il sistema di canali.  Per creare nuove funzionalità a livello di applicazione, è necessario estendere la fase di esecuzione del servizio o del client \(dispatcher e channel factory rispettivamente\).  [!INCLUDE[crabout](../../../includes/crabout-md.md)]ll'estensione della fase di esecuzione dell'applicazione, vedere [Estensione di ServiceHost e del livello del modello di servizi](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md).  
  
#### Estensione della protezione  
 Per creare meccanismi di sicurezza personalizzati, quali token e credenziali, è necessario estendere il sistema di sicurezza.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Estensione della protezione](../../../docs/framework/wcf/extending/extending-security.md).  
  
#### Estensione di metadati  
 Per esporre i metadati diversamente dall'impostazione predefinita, è necessario estendere il sistema dei metadati.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Estensione del sistema di metadati](../../../docs/framework/wcf/extending/extending-the-metadata-system.md).  
  
#### Estensione della serializzazione  
 Per compilare codificatori personalizzati, fornire surrogati dei dati o eseguire altre operazioni che comportano la personalizzazione di dati trasferiti, è necessario estendere il sistema di serializzazione.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Estensione di codificatori e serializzatori](../../../docs/framework/wcf/extending/extending-encoders-and-serializers.md).  
  
#### Estensione delle associazioni  
 Per associare canali del trasporto o del protocollo al livello dell'applicazione, è necessario estendere il sistema delle associazioni.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Estensione delle associazioni](../../../docs/framework/wcf/extending/extending-bindings.md).  
  
### Estensione del sistema di canali  
 Per creare canali che supportino funzionalità di trasporto o di protocollo personalizzate, vedere [Estensione del livello del canale](../../../docs/framework/wcf/extending/extending-the-channel-layer.md).  
  
### Estensione del sistema host del servizio  
 Per modificare il modello di applicazione a livello di servizio, è necessario estendere la classe <xref:System.ServiceModel.ServiceHostBase?displayProperty=fullName>.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Estensione di ServiceHost e del livello del modello di servizi](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md).  
  
 Per modificare la relazione tra il dominio dell'applicazione host e l'host del servizio, è necessario estendere la classe <xref:System.ServiceModel.Activation.ServiceHostFactory?displayProperty=fullName>.  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Estensione dell'hosting tramite ServiceHostFactory](../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md).  
  
## Vedere anche  
 [Estensione di WCF](../../../docs/framework/wcf/extending/extending-wcf.md)