---
title: "Application Settings Attributes | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "application settings [Windows Forms], attributes"
  - "attributes [Windows Forms], application settings"
  - "wrapper classes, application settings"
ms.assetid: 53caa66c-a9fb-43a5-953c-ad092590098d
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Application Settings Attributes
L'architettura delle impostazioni delle applicazioni fornisce numerosi attributi che è possibile applicare alla classe wrapper delle impostazioni delle applicazioni o alle singole proprietà.  Gli attributi vengono esaminati in fase di esecuzione dall'infrastruttura delle impostazioni delle applicazioni, spesso per l'esattezza dal provider di impostazioni, allo scopo di adattarne il funzionamento alle esigenze dichiarate del wrapper personalizzato.  
  
 Nella tabella seguente sono indicati gli attributi che è possibile applicare alla classe wrapper delle impostazioni dell'applicazione, alle singole proprietà della classe o a entrambi gli oggetti.  Per definizione, è possibile applicare un solo attributo di ambito, **UserScopedSettingAttribute** o **ApplicationScopedSettingAttribute**, a ogni singola proprietà di impostazioni.  
  
> [!NOTE]
>  Un provider di impostazioni personalizzato, derivato dalla classe <xref:System.Configuration.SettingsProvider>, è necessario solo per riconoscere i tre attributi seguenti: **ApplicationScopedSettingAttribute**, **UserScopedSettingAttribute** e **DefaultSettingValueAttribute**.  
  
|Attributo|Destinazione|Descrizione|  
|---------------|------------------|-----------------|  
|<xref:System.Configuration.SettingsProviderAttribute>|Entrambe le dimensioni|Specifica il nome breve del provider di impostazioni da utilizzare per la persistenza.<br /><br /> Se l'attributo non è indicato, viene utilizzato il provider predefinito, <xref:System.Configuration.LocalFileSettingsProvider>.|  
|<xref:System.Configuration.UserScopedSettingAttribute>|Entrambe le dimensioni|Definisce una proprietà come impostazione dell'applicazione a livello di utente.|  
|<xref:System.Configuration.ApplicationScopedSettingAttribute>|Entrambe le dimensioni|Definisce una proprietà come impostazione dell'applicazione a livello di applicazione.|  
|<xref:System.Configuration.DefaultSettingValueAttribute>|Proprietà|Specifica una stringa che può essere deserializzata dal provider nel valore predefinito specificato a livello di codice \(hard\-coded\) per la proprietà.<br /><br /> La classe <xref:System.Configuration.LocalFileSettingsProvider> non richiede tale attributo e ignorerà qualsiasi valore da esso fornito se esiste già un valore persistente.|  
|<xref:System.Configuration.SettingsDescriptionAttribute>|Proprietà|Fornisce il testo descrittivo di una singola impostazione, utilizzato essenzialmente da strumenti impiegati in fase di esecuzione e progettazione.|  
|<xref:System.Configuration.SettingsGroupNameAttribute>|Classe|Fornisce un nome esplicito per un gruppo di impostazioni.  Se tale attributo non è presente, la classe <xref:System.Configuration.ApplicationSettingsBase> utilizza il nome della classe wrapper.|  
|<xref:System.Configuration.SettingsGroupDescriptionAttribute>|Classe|Fornisce il testo descrittivo di un gruppo di impostazioni, utilizzato essenzialmente da strumenti impiegati in fase di esecuzione e progettazione.|  
|<xref:System.Configuration.SettingsManageabilityAttribute>|Entrambe le dimensioni|Consente di specificare da zero a più servizi di gestibilità da fornire al gruppo di impostazioni o alla proprietà.  I servizi disponibili sono descritti dall'enumerazione <xref:System.Configuration.SettingsManageability>.|  
|<xref:System.Configuration.SpecialSettingAttribute>|Proprietà|Indica che un'impostazione appartiene a una categoria predefinita speciale, quale una stringa di connessione, che suggerisce l'elaborazione speciale da parte del provider di impostazioni.  Le categorie predeterminate dell'attributo sono definite dall'enumerazione <xref:System.Configuration.SpecialSetting>.|  
|<xref:System.Configuration.SettingsSerializeAsAttribute>|Entrambe le dimensioni|Specifica un meccanismo di serializzazione preferito per un gruppo di impostazioni o una proprietà.  I meccanismi di serializzazione disponibili sono definiti dall'enumerazione <xref:System.Configuration.SettingsSerializeAs>.|  
|<xref:System.Configuration.NoSettingsVersionUpgradeAttribute>|Proprietà|Specifica che un provider di impostazioni deve disabilitare tutte le funzioni di aggiornamento dell'applicazione per la proprietà contrassegnata.|  
  
 *Classe* indica che l'attributo può essere applicato solo a una classe wrapper delle impostazioni dell'applicazione.  *Proprietà* indica che l'attributo può essere applicato solo alle proprietà delle impostazioni.  *Entrambe* indica che l'attributo può essere applicato a entrambi i livelli.  
  
## Vedere anche  
 <xref:System.Configuration.ApplicationSettingsBase>   
 <xref:System.Configuration.SettingsProvider>   
 [Application Settings Architecture](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)   
 [How to: Create Application Settings](http://msdn.microsoft.com/it-it/53b3af80-1c02-4e35-99c6-787663148945)