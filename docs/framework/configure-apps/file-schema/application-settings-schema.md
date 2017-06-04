---
title: "Schema Application Settings | Microsoft Docs"
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
  - "impostazioni di applicazioni, schema [Windows Form]"
  - "schema di configurazione [.NET Framework], impostazioni di applicazioni"
  - "schema (impostazioni di applicazioni)"
  - "Windows Form, schema impostazioni di applicazioni"
ms.assetid: 5797fcff-6081-4e8c-bebf-63d9c70cf14b
caps.latest.revision: 3
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 3
---
# Schema Application Settings
Questo schema consente a un'applicazione Windows Form o ASP.NET di memorizzare e recuperare le impostazioni con ambito di applicazione o di utente.  In questo contesto, per impostazione si intende un qualsiasi elemento di informazione che può essere specifico per l'applicazione o per l'utente corrente, ad esempio un qualsiasi elemento di una stringa di connessione al database relativo alla dimensione preferita della finestra predefinita dell'utente.  
  
 Per impostazione predefinita, Application Settings in un'applicazione Windows Form utilizza la classe <xref:System.Configuration.LocalFileSettingsProvider>, che utilizza il sistema di configurazione .NET per memorizzare le impostazioni in un file di configurazione XML.  Per ulteriori informazioni sui file utilizzati da Application Settings, vedere [Application Settings Architecture](../../../../docs/framework/winforms/advanced/application-settings-architecture.md).  
  
 Application Settings definisce i seguenti elementi all'interno dei file di configurazione utilizzati.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|Elemento `<applicationSettings>`|Contiene tutti i tag `<setting>` specifici per l'applicazione.|  
|Elemento `<userSettings>`|Contiene tutti i tag `<setting>` specifici per l'utente corrente.|  
|Elemento `<setting>`|Definisce un'impostazione.  Figlio di `<applicationSettings>` o `<userSettings>`.|  
|Elemento `<value>`|Definisce il valore di un'impostazione.  Figlio di `<setting>`.|  
  
## Elemento \<applicationSettings\>  
 Questo elemento contiene tutti i tag \<setting\> specifici per un'istanza dell'applicazione su un computer client.  Non definisce alcun attributo.  
  
## Elemento \<userSettings\>  
 Questo elemento contiene tutti i tag \<setting\> specifici per l'utente che sta attualmente utilizzando l'applicazione.  Non definisce alcun attributo.  
  
## Elemento \<setting\>  
 Questo elemento definisce un'impostazione  Gli attributi di cui dispone sono riportati di seguito.  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`name`|Obbligatorio.  ID univoco dell'impostazione.  Le impostazioni create mediante Visual Studio vengono salvate con il nome `ProjectName``.Properties.Settings`.|  
|`serializedAs`|Obbligatorio.  Formato da utilizzare per la serializzazione del valore in testo.  I valori validi sono:<br /><br /> -   `string`:  il valore viene serializzato come stringa mediante <xref:System.ComponentModel.TypeConverter>.<br />-   `xml`.  il valore viene serializzato mediante la serializzazione XML.<br />-   `binary`:  il valore viene serializzato come valore binario con testo codificato mediante la serializzazione binaria.<br />-   `custom`:  il fornitore possiede una conoscenza intrinseca di questa impostazione e quindi eseguirà la relativa serializzazione e deserializzazione.<br />-   Per utilizzare la serializzazione binaria o personalizzata, è necessario definire una propria classe settings e utilizzare <xref:System.Configuration.SettingsSerializeAsAttribute> per specificare la serializzazione binaria o personalizzata.|  
  
## Elemento \<value\>  
 Questo elemento contiene il valore di un'impostazione.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato un file Application Settings che definisce due impostazioni con ambito di applicazione e due impostazioni con ambito di utente.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
    <configSections>  
        <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >  
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
        </sectionGroup>  
        <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >  
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />  
        </sectionGroup>  
    </configSections>  
    <applicationSettings>  
        <WindowsApplication1.Properties.Settings>  
            <setting name="Cursor" serializeAs="String">  
                <value>Default</value>  
            </setting>  
            <setting name="DoubleBuffering" serializeAs="String">  
                <value>False</value>  
            </setting>  
        </WindowsApplication1.Properties.Settings>  
    </applicationSettings>  
    <userSettings>  
        <WindowsApplication1.Properties.Settings>  
            <setting name="FormTitle" serializeAs="String">  
                <value>Form1</value>  
            </setting>  
            <setting name="FormSize" serializeAs="String">  
                <value>595, 536</value>  
            </setting>  
        </WindowsApplication1.Properties.Settings>  
    </userSettings>  
</configuration>  
```  
  
## Vedere anche  
 [Cenni preliminari sulle impostazioni delle applicazioni](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [Application Settings Architecture](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)