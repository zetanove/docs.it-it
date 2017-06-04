---
title: "Elemento &lt;supportPortability&gt; | Microsoft Docs"
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
  - "<supportPortability> (elemento)"
  - "supportPortability (elemento)"
ms.assetid: 6453ef66-19b4-41f3-b712-52d0c2abc9ca
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Elemento &lt;supportPortability&gt;
Specifica che un'applicazione può fare riferimento allo stesso assembly in due implementazioni diverse di .NET Framework, disabilitando il comportamento predefinito che tratta gli assembly come equivalenti allo scopo della portabilità dell'applicazione.  
  
## Sintassi  
  
```  
<supportPortability PKT="public_key_token" enabled="true|false"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|PKT|Attributo obbligatorio.<br /><br /> Specifica il token di chiave pubblica dell'assembly interessato, come una stringa.|  
|enabled|Attributo facoltativo.<br /><br /> Specifica se deve essere abilitato il supporto per la portabilità tra implementazioni dell'assembly .NET Framework specificato.|  
  
## Attributo enabled  
  
|Valore|Descrizione|  
|------------|-----------------|  
|true|Abilita il supporto per la portabilità tra implementazioni dell'assembly .NET Framework specificato.  Questa è l'impostazione predefinita.|  
|false|Disabilita il supporto per la portabilità tra implementazioni dell'assembly .NET Framework specificato.  Consente all'applicazione di avere riferimenti a più implementazioni dell'assembly specificato.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
|`assemblyBinding`|Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.|  
  
## Note  
 Iniziando con [!INCLUDE[net_v40_long](../../../../../includes/net-v40-long-md.md)], il supporto viene fornito automaticamente per le applicazioni che possono utilizzare una delle due implementazioni di .NET Framework, ad esempio l'implementazione di .NET Framework o di .NET Framework per Silverlight.  Le due implementazioni di un particolare assembly .NET Framework vengono considerate equivalenti dal gestore di associazione dell'assembly.  In alcuni scenari, questa funzionalità di portabilità dell'applicazione crea problemi.  In quegli scenari, l'elemento `<supportPortability>` può essere utilizzato per disabilitare la funzionalità.  
  
 Un tale scenario è un assembly che deve fare riferimento sia all'implementazione di .NET Framework sia all'implementazione di .NET Framework per Silverlight di un particolare assembly di riferimento.  Ad esempio, una finestra di progettazione XAML scritta in Windows Presentation Foundation \(WPF\) potrebbe dovere fare riferimento sia all'implementazine di Desktop WPF, per l'interfaccia utente della finestra di progettazione che al sottoinsieme di WPF incluso nell'implementazione di Silverlight.  Per impostazione predefinita, i riferimenti separati provocano un errore del compilatore, perché l'associazione di assembly vede i due assembly come equivalenti.  Questo elemento disabilita il comportamento predefinito e consente alla compilazione di riuscire.  
  
> [!IMPORTANT]
>  Affinché il compilatore passi le informazioni alla logica di associazione dell'assembly di Common Language Runtime, è necessario utilizzare l'opzione del compilatore `/appconfig` per specificare il percorso del file app.config che contiene questo elemento.  
  
## Esempio  
 Nell'esempio seguente viene abilitata un'applicazione ad avere riferimenti sia all'implementazione di .NET Framework sia all'implementazione di .NET Framework for Silverlight di qualsiasi assembly di .NET Framework presente in entrambe le implementazioni.  L'opzione del compilatore `/appconfig` deve essere utilizzata per specificare il percorso di questo file app.config.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding>  
         <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
         <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## Vedere anche  
 [\/appconfig \(opzioni del compilatore C\#\)](http://msdn.microsoft.com/library/ee523958.aspx)   
 [.NET Framework Assembly Unification Overview](http://msdn.microsoft.com/it-it/8d8cc65e-031d-463b-bde3-2c6dc2e3bc48)