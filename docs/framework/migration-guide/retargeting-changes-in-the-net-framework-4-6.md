---
title: "Modifiche di reindirizzamento in .NET Framework 4.6 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa849255-f90f-4bf1-b0ff-b173c12110d7
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Modifiche di reindirizzamento in .NET Framework 4.6
In rari casi, le modifiche di reindirizzamento possono influire sulle app che vengono ricompilate per [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. A meno che non venga specificato diversamente, queste modifiche non influiscono sui file binari destinati a una versione precedente di .NET Framework ma vengono eseguiti in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)].  
  
 [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] include le modifiche di reindirizzamento nelle aree seguenti:  
  
-   [ASP.NET](#ASP)  
  
-   [Servizi di rete](#Net)  
  
-   [Windows Communications Foundation \(WCF\)](#WCF)  
  
-   [Windows Form](#WinForms)  
  
-   [Windows Presentation Foundation \(WPF\)](#WPF)  
  
-   [XML](#XML)  
  
<a name="ASP"></a>   
## ASP.NET  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|<xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName> con un valore `tagKey` di <xref:System.Web.UI.HtmlTextWriterTag?displayProperty=fullName>|In conformità con lo standard HTML, il metodo <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName> ora esegue il rendering di <xref:System.Web.UI.HtmlTextWriterTag?displayProperty=fullName> come tag non di chiusura in una risposta HTML.|Il tag BR ora produce un'interruzione di riga. Precedentemente, ha prodotto due interruzioni di riga.<br /><br /> Le app che dipendono dal tag `<BR>` per produrre due interruzioni di riga possono ripristinare il comportamento precedente aggiungendo una chiamata aggiuntiva al metodo <xref:System.Web.UI.HtmlTextWriter.RenderBeginTag%28System.Web.UI.HtmlTextWriterTag%29?displayProperty=fullName> con l'argomento <xref:System.Web.UI.HtmlTextWriterTag?displayProperty=fullName>.|Secondario|  
  
<a name="Net"></a>   
## Servizi di rete  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|<xref:System.Net.ServicePointManager?displayProperty=fullName> e <xref:System.Net.Security.SslStream?displayProperty=fullName>|A partire dalle app destinate a .NET Framework 4.6, le classi <xref:System.Net.ServicePointManager?displayProperty=fullName> e <xref:System.Net.Security.SslStream?displayProperty=fullName> possono usare uno dei protocolli seguenti: Tls1.0, Tls1.1 o Tls 1.2.<br /><br /> Le app per una versione precedente di NET Framework, anche se vengono eseguite su NET Framework 4.6, non sono interessate.|Questa modifica influisce su qualsiasi app destinata a .NET Framework 4.6 che usa SSL per comunicare con un server HTTPS o un server socket tramite uno qualsiasi dei tipi seguenti: <xref:System.Net.Http.HttpClient>, <xref:System.Net.HttpWebRequest>, <xref:System.Net.FtpWebRequest>, <xref:System.Net.Mail.SmtpClient> e <xref:System.Net.Security.SslStream>.  Per altre informazioni, vedere [Attenuazione: Protocolli TLS](../../../docs/framework/migration-guide/mitigation-tls-protocols.md).|Secondario|  
  
<a name="WCF"></a>   
## Windows Communications Foundation \(WCF\)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|<xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%2A?displayProperty=fullName>|L'implementazione dell'oggetto <xref:System.IdentityModel.Policy.AuthorizationContext> restituito da una chiamata al metodo <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext%28System.Collections.Generic.IList%7BSystem.IdentityModel.Policy.IAuthorizationPolicy%7D%29> con un argomento `null``authorizationPolicies` è cambiata in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)].|In rari casi, le app WCF che usano l'autenticazione personalizzata possono riscontrare differenze di comportamento. Se è necessario il comportamento precedente, vedere [Attenuazione: AuthorizationContext predefinito](../../../docs/framework/migration-guide/mitigation-default-authorizationcontext.md).|Secondario|  
  
<a name="WinForms"></a>   
## Windows Form  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=fullName>|A partire dalle app destinare a .NET Framework 4.6, il metodo <xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=fullName> converte correttamente le icone con i frame PNG in oggetti <xref:System.Drawing.Bitmap>.<br /><br /> Nelle app destinate a .NET Framework 4.5.2 e alle versioni precedenti, il metodo <xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=fullName> genera un'eccezione <xref:System.ArgumentOutOfRangeException> se l'oggetto <xref:System.Drawing.Icon> presenta frame PNG.|Questa modifica influisce sulle app che vengono ricompilate per essere destinate a .NET Framework 4.6 e che implementano una gestione speciale per l'eccezione <xref:System.ArgumentOutOfRangeException> generata se un oggetto <xref:System.Drawing.Icon> presenta frame PNG. Se questo comportamento è indesiderato, un'opzione di configurazione ripristina il comportamento precedente. Per altre informazioni, vedere [Attenuazione: Frame PNG in oggetti icona](../../../docs/framework/migration-guide/mitigation-png-frames-in-icon-objects.md).|Secondario|  
  
<a name="WPF"></a>   
## Windows Presentation Foundation \(WPF\)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Arrotondamento del layout a DPI elevati|Il modo in cui i margini vengono arrotondati e i bordi e lo sfondo al loro interno vengono modificati.|Il layout dei controlli WPF può cambiare leggermente. Per altre informazioni, vedere [Attenuazione: Layout WPF](../../../docs/framework/migration-guide/mitigation-wpf-layout.md).|Secondario|  
  
<a name="XML"></a>   
## XML  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|------------------|--------------|-------------|------------|  
|Convalida dello schema XSD|A partire da .NET Framework 4.6 la convalida dello schema XSD rileva la violazione di vincoli univoci se viene usata una chiave composta e una chiave è vuota.|Vedere [Attenuazione: Convalida di XML Schema](../../../docs/framework/migration-guide/mitigation-xml-schema-validation.md)|Secondario|  
|<xref:System.Xml.XmlWriter>|Per le app destinate a .NET Framework 4.5.2 o a versioni precedenti, se si scrive una coppia di surrogati non valida usando la gestione dei fallback delle eccezioni, non viene sempre generata un'eccezione.<br /><br /> Per le app destinate a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], se si tenta di scrivere una coppia di surrogati non valida, viene generata un'eccezione <xref:System.ArgumentException>.|Per le app che vengono ricompilate per essere destinate a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], se vengono scritte coppie di surrogati non valide, verrà generata un'eccezione anche nei casi in cui prima non veniva generata.|Marginale|