---
title: "Modifiche al runtime in .NET Framework 4.5.2 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 94ac01ea-8b12-44d2-b12b-5220a5d14d87
caps.latest.revision: 5
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 5
---
# Modifiche al runtime in .NET Framework 4.5.2
In rari casi, le modifiche al runtime potrebbero incidere sulle app esistenti destinate alle versioni precedenti di .NET Framework ma eseguite nel runtime di .NET Framework 4.5.2. Sono incluse le modifiche apportate nelle seguenti aree:  
  
-   [ASP.NET](#ASP_NET)  
  
-   [Entity Framework](#EF)  
  
<a name="ASP_NET"></a>   
## Modifiche al runtime ASP.NET  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Attributo `enableViewStateMac` dell'[elemento pages](http://msdn.microsoft.com/it-it/4123bb66-3fe4-4d62-b70e-33758656b458)|ASP.NET non consente più agli sviluppatori di specificare:<br /><br /> `<pages enableViewStateMac="false" />`<br /><br /> oppure:<br /><br /> `<@Page EnableViewStateMac="false" %>`|L'algoritmo Message Authentication Code \(MAC\) dello stato di visualizzazione viene ora applicato per tutte le richieste con stato di visualizzazione incorporato. Riguarda solo le app che impostano in modo esplicito la proprietà <xref:System.Web.UI.Page.EnableViewStateMac%2A> su `false`.<br /><br /> Per altre informazioni, vedere [Risoluzione degli errori relativi allo stato di visualizzazione del codice MAC \(Message Authentication Code\)](http://support.microsoft.com/kb/2915218).|Principale|  
  
<a name="EF"></a>   
## Modifiche al runtime di Entity Framework  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Relazioni su un elemento QueryView|Entity Framework non genera più un'eccezione <xref:System.StackOverflowException> quando un'app esegue una query che coinvolge un elemento QueryView con una proprietà di navigazione 0..1 che tenta di includere le entità correlate nella query, ad esempio chiamando `.Include(e=>e.RelatedNavProp)`.|Questa modifica riguarda solo il codice che usa elementi QueryView con relazioni 1\-0..1 in caso di esecuzione di query che chiamano `.Include`. Migliora l'affidabilità e dovrebbe essere trasparente a quasi tutte le app. Se tuttavia questa modifica causa un comportamento imprevisto, è possibile disabilitarla aggiungendo la voce seguente alla sezione `<appSettings>` del file di configurazione dell'app:<br /><br /> `<add key="EntityFramework_SimplifyUserSpecifiedViews"  value="false" />`|Microsoft Edge|  
  
## Vedere anche  
 [Reindirizzamento delle modifiche](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-5-2.md)   
 [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Compatibilità delle applicazioni nella versione 4.5.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-1.md)