---
title: "Elemento &lt;generatePublisherEvidence&gt; | Microsoft Docs"
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
  - "<generatePublisherEvidence> (elemento)"
  - "generatePublisherEvidence (elemento)"
ms.assetid: 7d208f50-e8d5-4a42-bc1a-1cf3590706a8
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Elemento &lt;generatePublisherEvidence&gt;
Specifica se tramite il runtime viene creata l'evidenza <xref:System.Security.Policy.Publisher> per la sicurezza dall'accesso di codice.  
  
## Sintassi  
  
```  
<generatePublisherEvidence    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se tramite il runtime viene creata l'evidenza <xref:System.Security.Policy.Publisher>.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Non crea l'evidenza <xref:System.Security.Policy.Publisher>.|  
|`true`|Crea l'evidenza <xref:System.Security.Policy.Publisher>.  Questa è l'impostazione predefinita.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] e versioni successive, questo elemento non ha effetto sui tempi di caricamento dell'assembly.  Per ulteriori informazioni, vedere la sezione relativa alla semplificazione dei criteri di sicurezza [Modifiche della sicurezza](../../../../../docs/framework/security/security-changes.md).  
  
 Common Language Runtime \(CLR\) tenta di verificare la firma Authenticode al momento del caricamento per creare l'evidenza <xref:System.Security.Policy.Publisher> per l'assembly.  Tuttavia, per impostazione predefinita la maggior parte delle applicazioni non hanno bisogno dell'evidenza <xref:System.Security.Policy.Publisher>.  I criteri di sicurezza dall'accesso di codice non si basano su <xref:System.Security.Policy.PublisherMembershipCondition>.  È opportuno evitare il costo di avvio non necessario associato alla verifica della firma dell'editore a meno che l'applicazione non venga eseguita in un computer con i criteri di sicurezza dall'accesso di codice personalizzati o non sia progettata per soddisfare le richieste per <xref:System.Security.Permissions.PublisherIdentityPermission> in un ambiente parzialmente attendibile. Le richieste per le autorizzazioni di identità vengono sempre eseguite in un ambiente totalmente attendibile.\)  
  
> [!NOTE]
>  È consigliabile che i servizi utilizzino l'elemento `<generatePublisherEvidence>` per migliorare le prestazioni di avvio.  L'utilizzo di questo elemento consente anche di evitare ritardi che possono provocare il timeout e l'annullamento dell'avvio del servizio.  
  
## File di configurazione  
 L'elemento può essere utilizzato esclusivamente nel file di configurazione dell'applicazione.  
  
## Esempio  
 Nell'esempio seguente è mostrato come utilizzare l'elemento `<generatePublisherEvidence>` per disabilitare la verifica dei criteri di sicurezza dall'accesso di codice dell'editore per un'applicazione.  
  
```  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)