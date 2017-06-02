---
title: "Elemento &lt;bypassTrustedAppStrongNames&gt; | Microsoft Docs"
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
  - "<bypassTrustedAppStrongNames> (elemento)"
  - "bypassTrustedAppStrongNames (elemento)"
  - "funzionalità che consente di ignorare la verifica del nome sicuro"
  - "assembly con nome sicuro, caricamento in domini dell'applicazione trusted"
ms.assetid: 71b2ebf6-3843-41e2-ad52-ffa5cd083a40
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Elemento &lt;bypassTrustedAppStrongNames&gt;
Specifica se ignorare la convalida di nomi sicuri per gli assembly con attendibilità totale caricati in un oggetto <xref:System.AppDomain> con attendibilità totale.  
  
## Sintassi  
  
```  
<bypassTrustedAppStrongNames    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se è attivata la funzionalità che consente di ignorare la convalida di nomi sicuri per gli assembly con attendibilità totale.  Se questa funzionalità è attivata, i nomi sicuri non vengono convalidati per verificare che siano corretti quando l'assembly viene caricato.  Il valore predefinito è `true`.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`true`|Le firme con nome sicuro per gli assembly con attendibilità totale non vengono convalidate quando gli assembly vengono caricati in un oggetto <xref:System.AppDomain> con attendibilità totale.  Questa è l'impostazione predefinita.|  
|`false`|Le firme con nome sicuro per gli assembly con attendibilità totale vengono convalidate quando gli assembly vengono caricati in un oggetto <xref:System.AppDomain> con attendibilità totale.  La firma con nome sicuro viene controllata solo per verificare se è corretta; non viene confrontata con un altro nome sicuro per trovare una corrispondenza.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## Note  
 La funzionalità che consente di ignorare il nome sicuro evita il sovraccarico associato alla verifica delle firme con nome sicuro degli assembly con attendibilità totale.  
  
 Questa funzionalità si applica a tutti gli assembly firmati con nome sicuro che abbiano le caratteristiche seguenti:  
  
-   Sono completamente attendibili senza l'evidenza <xref:System.Security.Policy.StrongName> \(ad esempio, dispongono dell'evidenza della zona `MyComputer`\).  
  
-   Vengono caricati in un oggetto <xref:System.AppDomain> completamente attendibile.  
  
-   Vengono caricati da un percorso nella proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> di tale oggetto <xref:System.AppDomain>.  
  
-   Non hanno firma ritardata.  
  
> [!NOTE]
>  Se la funzionalità che consente di ignorare il nome sicuro viene disattivata per tutte le applicazioni del computer tramite una chiave del Registro di sistema, questa impostazione del file di configurazione non ha alcun effetto.  Per ulteriori informazioni, vedere [Procedura: disabilitare la funzionalità che consente di ignorare il nome sicuro](../../../../../docs/framework/app-domains/how-to-disable-the-strong-name-bypass-feature.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come specificare il comportamento che convalida la firma con nome sicuro per gli assembly con attendibilità totale.  
  
```  
<configuration>  
   <runtime>  
      <bypassTrustedAppStrongNames enabled="false"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Procedura: disabilitare la funzionalità che consente di ignorare il nome sicuro](../../../../../docs/framework/app-domains/how-to-disable-the-strong-name-bypass-feature.md)