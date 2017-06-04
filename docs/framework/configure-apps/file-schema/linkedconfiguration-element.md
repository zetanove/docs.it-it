---
title: "Elemento &lt;linkedConfiguration&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding/linkedConfiguration"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#linkedConfiguration"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<linkedConfiguration> (elemento)"
  - "file di configurazione [.NET Framework], file di configurazione collegati"
  - "inclusione di file di configurazione"
  - "file di configurazione collegati"
  - "linkedConfiguration (elemento)"
ms.assetid: 8eb34f3b-427e-4288-a7ff-c73f489deb45
caps.latest.revision: 6
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 6
---
# Elemento &lt;linkedConfiguration&gt;
Specifica un file di configurazione da includere.  
  
## Sintassi  
  
```  
<linkedConfiguration  
   href="URL of linked configuration file"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`href`|URL del file di configurazione da includere.  L'unico formato supportato per l'attributo `href` è "file:\/\/".  Sono supportati i file locali e i file UNC.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[Elemento \<assemblyBinding\>](../../../../docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)|Specifica i criterio di associazione degli assembly al livello di configurazione.|  
  
## Note  
 L'elemento `<linkedConfiguration>` semplifica la gestione degli assembly del componente.  Se una o più applicazioni utilizzano un assembly il cui file di configurazione è contenuto in un percorso noto, i file di configurazione delle applicazioni che utilizzano l'assembly possono utilizzare l'elemento `<linkedConfiguration>` per includere il file di configurazione dell'assembly, anziché direttamente le informazioni di configurazione.  Quando viene eseguita la gestione dell'assembly del componente, è sufficiente aggiornare il file di configurazione comune per fornire informazioni di configurazione aggiornate a tutte le applicazioni in cui viene utilizzato l'assembly.  
  
> [!NOTE]
>  L'elemento `<linkedConfiguration>` non è supportato per le applicazioni con manifesti di Windows affiancati.  
  
 L'utilizzo dei file di configurazione collegati è controllato dalle regole riportate di seguito.  
  
-   Le impostazioni contenute nei file di configurazione inclusi hanno effetto solo sui criteri di associazione del caricatore e vengono utilizzate solo dal caricatore.  Nei file di configurazione inclusi possono essere contenute impostazioni diverse dai criteri di associazione, ma tali impostazioni non producono alcun effetto.  
  
-   L'unico formato supportato per l'attributo `href` è "file:\/\/".  Sono supportati i file locali e i file UNC.  
  
-   Non esistono limiti per il numero delle configurazioni collegate per file di configurazione.  
  
-   Tutti i file di configurazione collegati vengono uniti per formare un file, analogamente al comportamento della direttiva `#include` in C\/C\+\+.  
  
-   L'elemento `<linkedConfiguration>` è supportato solo dai file di configurazione dell'applicazione. Viene ignorato in Machine.config.  
  
-   I riferimenti circolari vengono rilevati e terminati,  ovvero se gli elementi `<linkedConfiguration>` di una serie di file di configurazione formano un ciclo, il ciclo viene rilevato e arrestato.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come includere un file di configurazione dal disco rigido locale.  
  
```  
<configuration>  
   <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
      <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml"/>  
   </assemblyBinding>  
</configuration>  
```  
  
## Vedere anche  
 [Elemento \<assemblyBinding\>](../../../../docs/framework/configure-apps/file-schema/assemblybinding-element-for-configuration.md)   
 [Schema dei file di configurazione](../../../../docs/framework/configure-apps/file-schema/index.md)