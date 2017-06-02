---
title: "Elemento &lt;assemblyBinding&gt; per &lt;configuration&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "Elemento <assemblyBinding>"
  - "assemblyBinding (elemento)"
ms.assetid: 6cc55983-b894-449b-8e26-b258e53939cd
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Elemento &lt;assemblyBinding&gt; per &lt;configuration&gt;
Specifica i criterio di associazione degli assembly al livello di configurazione.  
  
## Sintassi  
  
```  
<assemblyBinding    
   xmlns="urn:schemas-microsoft-com:asm.v1">  
</assemblyBinding>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`xmlns`|Attributo obbligatorio.<br /><br /> Specifica lo spazio dei nomi XML necessario per l'associazione degli assembly.  Utilizzare la stringa "urn:schemas\-microsoft\-com:asm.v1" come valore.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<linkedConfiguration\>](../../../../docs/framework/configure-apps/file-schema/linkedconfiguration-element.md)|Specifica un file di configurazione da includere.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<Configuration\>](../../../../docs/framework/configure-apps/file-schema/configuration-element.md)|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
  
## Note  
 L'[Elemento \<linkedConfiguration\>](../../../../docs/framework/configure-apps/file-schema/linkedconfiguration-element.md) semplifica la gestione degli assembly del componente consentendo ai file di configurazione dell'applicazione di includere file di configurazione degli assembly contenuti in percorsi conosciuti, anziché duplicare le impostazioni di configurazione degli assembly.  
  
> [!NOTE]
>  L'elemento `<linkedConfiguration>` non è supportato per le applicazioni con manifesti di Windows affiancati.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come includere un file di configurazione nel disco rigido locale.  
  
```  
<configuration>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
      <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml"/>  
   </assemblyBinding>  
</configuration>  
```  
  
## Vedere anche  
 [Schema dei file di configurazione](../../../../docs/framework/configure-apps/file-schema/index.md)