---
title: "Schema delle impostazioni di crittografia | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
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
  - "schema di configurazione [.NET Framework], crittografia"
  - "sezioni di configurazione [.NET Framework]"
  - "impostazioni di configurazione [.NET Framework], crittografia"
  - "crittografia, mapping di nomi di algoritmi"
  - "crittografia, schema di impostazioni"
  - "elementi [.NET Framework], crittografia"
  - "impostazioni di configurazione di schema"
ms.assetid: 1f55050a-b2a3-4868-a3c0-da20826150f3
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Schema delle impostazioni di crittografia
Lo schema delle impostazioni di crittografia contiene gli elementi che consentono di specificare come eseguire il mapping dei nomi di algoritmi descrittivi sulle classi per l'implementazione degli algoritmi di crittografia.  
  
 [\<configurazione\>](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<mscorlib\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/mscorlib-element-for-cryptography-settings.md)  
  
 [\<cryptographySettings\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptographysettings-element.md)  
  
 [\<cryptoNameMapping\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptonamemapping-element.md)  
  
 [\<cryptoClasses\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclasses-element.md)  
  
 [\<cryptoClass\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclass-element.md)  
  
 [\<nameEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md)  
  
 [\<oidMap\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/oidmap-element.md)  
  
 [\<oidEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/oidentry-element.md)  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<cryptoClasses\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclasses-element.md)|Contiene un elenco delle classi di crittografia per le quali è stato eseguito il mapping su un nome descrittivo nell'elemento **\<nameEntry\>**.|  
|[\<cryptoClass\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclass-element.md)|Contiene una classe di crittografia per la quale è stato eseguito il mapping su un nome descrittivo nell'elemento **\<nameEntry\>**.|  
|[\<cryptographySettings\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptographysettings-element.md)|Contiene le impostazioni di crittografia.|  
|[\<cryptoNameMapping\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptonamemapping-element.md)|Contiene i mapping delle classi sui nomi descrittivi.|  
|[Elemento \<mscorlib\> per le impostazioni di crittografia](../../../../../docs/framework/configure-apps/file-schema/cryptography/mscorlib-element-for-cryptography-settings.md)|Contiene l'elemento **\<cryptographySettings\>**.|  
|[\<nameEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md)|Esegue il mapping del nome di una classe su un nome di algoritmo descrittivo consentendo l'uso di più nomi descrittivi per un'unica classe.|  
|[\<oidEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/oidentry-element.md)|Esegue il mapping di un identificatore di oggetto \(OID\) ASN.1 su un nome descrittivo.|  
|[\<oidMap\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/oidmap-element.md)|Contiene i mapping di un identificatore OID ASN.1 sulle classi.|  
  
## Vedere anche  
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Servizi di crittografia](../../../../../docs/standard/security/cryptographic-services.md)