---
title: "Elemento &lt;loadFromRemoteSources&gt; | Microsoft Docs"
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
  - "loadFromRemoteSources (elemento)"
  - "<loadFromRemoteSources> (elemento)"
ms.assetid: 006d1280-2ac3-4db6-a984-a3d4e275046a
caps.latest.revision: 31
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 31
---
# Elemento &lt;loadFromRemoteSources&gt;
Specifica se concedere attendibilità totale agli assembly provenienti da origini remote.  
  
> [!NOTE]
>  Se si viene indirizzati a questo argomento a causa di un messaggio di errore nell'elenco errori del progetto Visual Studio o di un errore di compilazione, vedere [Procedura: utilizzare un assembly dal Web in Visual Studio](http://msdn.microsoft.com/it-it/d8635b63-89a0-41aa-90f4-f351b2111070).  
  
## Sintassi  
  
```  
<loadFromRemoteSources    
   enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`enabled`|Attributo obbligatorio.<br /><br /> Specifica se concedere l'attendibilità totale a un assembly caricato da origini remote.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|`false`|Non concedere attendibilità totale alle applicazioni provenienti da origini remote.  Questa è l'impostazione predefinita.|  
|`true`|Concedere l'attendibilità totale alle applicazioni provenienti da origini remote.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sulle opzioni di inizializzazione in fase di esecuzione.|  
  
## Note  
 In .NET Framework 3.5 e versioni precedenti, un assembly caricato da un percorso remoto viene caricato come parzialmente attendibile con un set di autorizzazioni che dipende dalla zona in cui è stato caricato.  Ad esempio, se si caricano gli assembly da un sito web, vengono caricati nell'area Internet e dispongono del set di autorizzazioni previsto per Internet.  In altre parole, viene eseguito in una sandbox di Internet.  Se si tenta di eseguire tale assembly in [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)] e in versioni precedenti, viene generata un'eccezione. È necessario creare in modo esplicito una sandbox per l'assembly \(vedere [How to: Run Partially Trusted Code in a Sandbox](../../../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)\), o eseguirlo in attendibilità totale.  
  
 L'elemento `<loadFromRemoteSources>` consente di specificare che gli assembly che sarebbero eseguiti con attendibilità parziale nelle versioni precedenti di .NET Framework sono eseguiti con attendibilità totale in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)].  Per impostazione predefinita, gli assembly remoti non vengono eseguiti in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] e versioni successive.  Per eseguire un assembly remoto, è necessario eseguirlo come completamente attendibile o creare una sandbox <xref:System.AppDomain> in cui eseguirlo.  
  
> [!NOTE]
>  In [!INCLUDE[net_v45](../../../../../includes/net-v45-md.md)], gli assembly nelle condivisioni di rete locale vengono eseguiti con attendibilità totale per impostazione predefinita; non è necessario abilitare l'elemento `<loadFromRemoteSources>`.  
  
> [!NOTE]
>  Se un'applicazione è stata copiata dal Web, questa viene contrassegnata da Windows come applicazione web, anche se si trova nel computer locale.  È possibile modificare tale designazione modificando le proprietà del file. In alternativa, è possibile utilizzare l'elemento `<loadFromRemoteSources>` per concedere all'assembly l'attendibilità totale.  In alternativa, è possibile utilizzare il metodo <xref:System.Reflection.Assembly.UnsafeLoadFrom%2A> per caricare un assembly locale del sistema operativo contrassegnato come caricato dal web.  
  
 L'attributo `enabled` di questo elemento è efficace solo quando i criteri di sicurezza dall'accesso di codice \(CAS, Code Access Security\) sono disabilitati.  Tali criteri sono disabilitati per impostazione predefinita in [!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)] e versioni successive.  Se si imposta `enabled` su `true`, alle applicazioni remote viene concessa l'attendibilità totale.  
  
 Se l'attributo `enabled` di `<loadFromRemoteSources>` non viene impostato su `true`, nelle condizioni seguenti viene generata un'eccezione:  
  
-   Il dominio corrente presenta un comportamento di sandboxing diverso dal comportamento che presenta in [!INCLUDE[net_v35_short](../../../../../includes/net-v35-short-md.md)].  In questa situazione è necessario che i criteri CAS siano disabilitati e che il dominio corrente non sia stato creato mediante sandbox.  
  
-   L'assembly caricato non proviene dalla zona `MyComputer`.  
  
> [!NOTE]
>  Quando si prova a caricare un file da cartelle collegate in un computer che funziona da host, si potrebbe ricevere un'eccezione <xref:System.IO.FileLoadException> in un'applicazione per computer virtuale Windows.  Questo errore può inoltre verificarsi quando si tenta di caricare un file da una cartella collegata a [Servizi desktop remoto](http://go.microsoft.com/fwlink/?LinkId=182775) \(servizi terminal\).  Per evitare l'eccezione, impostare `enabled` su `true`.  
  
 L'impostazione dell'elemento `<loadFromRemoteSources>` su `true` evita la generazione di questa eccezione.  Consente di specificare che non si utilizza Common Language Runtime per garantire la sicurezza creando gli assembly caricati mediante sandbox e che a tali assembly è possibile concedere l'esecuzione con attendibilità totale.  
  
> [!IMPORTANT]
>  Se l'assembly non deve essere eseguito con attendibilità totale, non impostare questo elemento di configurazione.  Creare invece mediante sandbox un oggetto <xref:System.AppDomain> in cui caricare l'assembly.  
  
## File di configurazione  
 Questo elemento viene utilizzato in genere nel file di configurazione dell'applicazione, ma può essere utilizzato in altri file di configurazione a seconda del contesto.  Per ulteriori informazioni, vedere l'articolo [Utilizzare più impliciti dei criteri di sicurezza per l'accesso di codice: loadFromRemoteSources](http://go.microsoft.com/fwlink/p/?LinkId=266839) nel blog di sicurezza di .NET.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come concedere l'attendibilità totale alle applicazioni provenienti da origini remote.  
  
```  
<configuration>  
   <runtime>  
      <loadFromRemoteSources enabled="true"/>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [Utilizzi più impliciti dei criteri di sicurezza per l'accesso di codice: loadFromRemoteSources](http://go.microsoft.com/fwlink/p/?LinkId=266839)   
 [How to: Run Partially Trusted Code in a Sandbox](../../../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)   
 [Schema delle impostazioni dell'ambiente di esecuzione](../../../../../docs/framework/configure-apps/file-schema/runtime/index.md)   
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)