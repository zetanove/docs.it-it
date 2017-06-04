---
title: "Schema dei file di configurazione per .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "configurazione di applicazioni .NET Framework, schema di configurazione"
  - "app.config (file), schema"
  - "file di configurazione dell'applicazione, schema"
  - "sviluppo di applicazioni [.NET Framework], schema"
  - "schema di configurazione [.NET Framework]"
  - "impostazioni di configurazione [.NET Framework], applicazioni"
  - "tag contenitore"
  - "enterprisesec (file di configurazione)"
  - "enterprisesec.config (file)"
  - "file di configurazione del computer"
  - "machine.config (file)"
  - "impostazioni di configurazione di schema"
  - "schemi, impostazioni di configurazione"
  - "sicurezza [.NET Framework], file di configurazione"
  - "security.config (file)"
  - "XML in formato corretto"
  - "XML (tag)"
ms.assetid: 69003d39-dc8a-460c-a6be-e6d93e690b38
caps.latest.revision: 20
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 18
---
# Schema dei file di configurazione per .NET Framework
I file di configurazione sono file XML standard che è possibile usare per modificare le impostazioni e impostare criteri per le app.  Lo schema di configurazione di .NET Framework è costituito da elementi che è possibile usare nei file di configurazione per controllare il comportamento delle app.  Il sommario di questa sezione rispecchia la gerarchia dello schema per l'avvio, il runtime, la rete e altri tipi di impostazioni di configurazione.  
  
 Per informazioni sui tipi, il formato e il percorso dei file di configurazione, vedere l'articolo [Configurazione di app](../../../../docs/framework/configure-apps/index.md).  Per modificare direttamente i file di configurazione, è necessario conoscere il linguaggio XML.  
  
> [!IMPORTANT]
>  Gli attributi e i tag XML nei file di configurazione fanno distinzione tra maiuscole e minuscole.  
  
## In questa sezione  
 [Elemento \<Configuration\>](../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
 Viene descritto l'elemento `<configuration>`, ossia l'elemento di primo livello di tutti i file di configurazione.  
  
 [Elemento \<assemblyBinding\>](../../../../docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)  
 Specifica i criterio di associazione degli assembly al livello di configurazione.  
  
 [Elemento \<linkedConfiguration\>](../../../../docs/framework/configure-apps/file-schema/linkedconfiguration-element.md)  
 Specifica un file di configurazione da includere.  
  
 [Schema delle impostazioni di avvio](../../../../docs/framework/configure-apps/file-schema/startup/index.md)  
 Vengono descritti gli elementi che specificano la versione di Common Language Runtime da usare.  
  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../docs/framework/configure-apps/file-schema/runtime/index.md)  
 Vengono descritti gli elementi che configurano l'associazione degli assembly e il funzionamento dell'ambiente di esecuzione.  
  
 [Schema delle impostazioni di rete](../../../../docs/framework/configure-apps/file-schema/network/index.md)  
 Vengono descritti gli elementi che specificano la modalità di connessione di .NET Framework a Internet.  
  
 [Schema delle impostazioni di crittografia](../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)  
 Vengono descritti gli elementi che eseguono il mapping dei nomi descrittivi degli algoritmi alle classi che implementano gli algoritmi di crittografia.  
  
 [Schema delle sezioni di configurazione](../../../../docs/framework/configure-apps/file-schema/configuration-sections-schema.md)  
 Vengono descritti gli elementi che consentono di creare e usare le sezioni di configurazione per le impostazioni personalizzate.  
  
 [Schema delle impostazioni di traccia e debug](../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)  
 Vengono descritti gli elementi che specificano i listener e le opzioni di traccia.  
  
 [Schema di impostazioni del compilatore e del provider di linguaggi](../../../../docs/framework/configure-apps/file-schema/compiler/index.md)  
 Vengono descritti gli elementi che consentono di specificare la configurazione del compilatore per i provider del linguaggio disponibili.  
  
 [Schema Application Settings](../../../../docs/framework/configure-apps/file-schema/application-settings-schema.md)  
 Vengono descritti gli elementi che consentono a un'applicazione Windows Form o ASP.NET di archiviare e recuperare le impostazioni con ambito di applicazione o di utente.  
  
 [Schema delle impostazioni Web](../../../../docs/framework/configure-apps/file-schema/web/index.md)  
 Tutti gli elementi nello schema delle impostazioni Web, che include gli elementi per la configurazione del funzionamento di ASP.NET con un'applicazione host, come IIS.  Utilizzato nei file aspnet.config.  
  
## Sezioni correlate  
 [Remoting Settings Schema](http://msdn.microsoft.com/it-it/dc2d1e62-9af7-4ca1-99fd-98b93bb4db9e)  
 Vengono descritti gli elementi che configurano le applicazioni client e server che implementano i servizi remoti.  
  
 [Impostazioni di configurazione di ASP.NET](http://msdn.microsoft.com/library/b5ysx397\(v=vs.100\).aspx)  
 Vengono descritti gli elementi che controllano il comportamento delle applicazioni Web ASP.NET.  
  
 [Web Services Settings Schema](http://msdn.microsoft.com/it-it/f84d6d55-1add-4eb7-ae46-33df5833ea2e)  
 Vengono descritti gli elementi che controllano il comportamento dei servizi Web ASP.NET e dei relativi client.  
  
 [Configuring .NET Framework Apps](http://msdn.microsoft.com/it-it/d789b592-fcb5-4e3d-8ac9-e0299adaaa42)  
 Viene descritto come configurare la sicurezza, l'associazione degli assembly e i servizi remoti in .NET Framework.