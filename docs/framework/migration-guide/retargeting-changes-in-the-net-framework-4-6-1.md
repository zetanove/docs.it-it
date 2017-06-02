---
title: "Modifiche di reindirizzamento in .NET Framework 4.6.1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 411ad548-30fa-43da-8716-10eccfc839e6
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# Modifiche di reindirizzamento in .NET Framework 4.6.1
In rari casi, le modifiche di reindirizzamento possono influire sulle app che vengono ricompilate per [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. A meno che non venga specificato diversamente, queste modifiche non influiscono sui file binari destinati a una versione precedente di .NET Framework ma vengono eseguiti in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].  
  
 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] include le modifiche di reindirizzamento nelle aree seguenti:  
  
-   [Windows Communication Foundation](#WCF)  
  
-   [Windows Form](#WinForms)  
  
<a name="WCF"></a>   
## Windows Communication Foundation  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=fullName><br /><br /> \(spazio dei nomi <xref:System.IdentityModel.Claims>\)|Nelle app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], se un set di attestazioni X509 viene inizializzato da un certificato con più voci DNS nel proprio campo SAN, il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A> cerca di stabilire una corrispondenza con l'argomento `claimType` con tutte le voci DNS.<br /><br /> Per le app destinate a versioni precedenti di .NET Framework, il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A> cerca di stabilire una corrispondenza con l'argomento `claimType` solo con l'ultima voce DNS.|Questa modifica interessa tutte le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Le app destinate alle versioni precedenti di .NET Framework non sono interessate.<br /><br /> Tuttavia, le app che fanno riferimento a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] possono rifiutare questo comportamento. Inoltre, è possibile per le app destinate a versioni precedenti di .NET Framework, ma che sono in esecuzione in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] per acconsentire questo comportamento. Per altre informazioni, vedere [Attenuazione: Metodo X509CertificiateClaimSet.FindClaims](../../../docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md).|Secondario|  
  
<a name="WinForms"></a>   
## Windows Form  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|metodo <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName> \(spazio dei nomi <xref:System.Windows.Forms>\)|Nelle app di Windows Form destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], un'implementazione <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=fullName> personalizzata può filtrare in modo sicuro i messaggi quando il metodo <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName> viene chiamato se l'implementazione <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=fullName>:<br /><br /> <ul><li>Esegue una o entrambe le opzioni seguenti:<br /><br /> <ul><li>Aggiunge un filtro messaggio chiamando il metodo <xref:System.Windows.Forms.Application.AddMessageFilter%2A>.</li><li>Rimuove un filtro messaggio chiamando il metodo <xref:System.Windows.Forms.Application.RemoveMessageFilter%2A>. ProcessOnStatus.</li></ul></li><li>**E** immette i messaggi chiamando il metodo <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=fullName>.</li></ul><br /> Questi tipi di implementazioni nelle app Windows Form destinate a versioni precedenti di .NET Framework in alcuni casi generano un'eccezione <xref:System.IndexOutOfRangeException> quando viene chiamato il metodo <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName>|Questa modifica interessa tutte le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Le app destinate alle versioni precedenti di .NET Framework non sono interessate.<br /><br /> Tuttavia, è possibile per le app, destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], di rifiutare questo comportamento. Inoltre, è possibile per le app destinate a versioni precedenti di .NET Framework, ma che sono in esecuzione in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] per acconsentire questo comportamento. Per altre informazioni, vedere [Attenuazione: Implementazioni IMessageFilter.PreFilterMessage personalizzate](../../../docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md).|Marginale|  
  
## Vedere anche  
 [Compatibilità delle applicazioni nella versione 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)