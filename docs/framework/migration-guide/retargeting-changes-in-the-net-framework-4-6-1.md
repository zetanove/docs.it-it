---
title: Modifiche di reindirizzamento in .NET Framework 4.6.1 | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes, .NET Framework
- retargeting changes, .NET Framework 4.6.1
- application compatibility
ms.assetid: 411ad548-30fa-43da-8716-10eccfc839e6
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0adc4a6cae566b6a15c5fa492620abb74b47335b
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="retargeting-changes-in-the-net-framework-461"></a>Modifiche di reindirizzamento in .NET Framework 4.6.1
In rari casi, le modifiche di reindirizzamento possono influire sulle app che vengono ricompilate per [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. A meno che non venga specificato diversamente, queste modifiche non influiscono sui file binari destinati a una versione precedente di .NET Framework ma vengono eseguiti in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].  
  
 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] include le modifiche di reindirizzamento nelle aree seguenti:  
  
-   [Base](#Core)  
  
-   [Contratti di codice](#Contracts)  
  
-   [Windows Communication Foundation](#WCF)  
  
-   [Windows Form](#WinForms)  
  
<a name="Core"></a>   
## <a name="core"></a>Base  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.IO.Compression.ZipFile.CreateFromDirectory%2A?displayProperty=fullName>|Per le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni successive, il carattere separatore di percorsi è stato modificato da una barra rovesciata ("\\") a una barra ("/") nella proprietà <xref:System.IO.Compression.ZipArchiveEntry.FullName%2A> degli oggetti <xref:System.IO.Compression.ZipArchiveEntry> creati da overload del metodo <xref:System.IO.Compression.ZipFile.CreateFromDirectory%2A?displayProperty=fullName>.|Questa modifica garantisce la conformità dell'implementazione .NET alla sezione 4.4.17.1 della [specifica relativa al formato di file ZIP](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT) e consente agli archivi con estensione ZIP di essere decompressi anche in sistemi non Windows.<br /><br /> Le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni successive, tuttavia, possono rifiutare questo comportamento. Per altre informazioni, vedere [Mitigation: ZipArchiveEntry.FullName Path Separator](../../../docs/framework/migration-guide/mitigation-ziparchiveentry-fullname-path-separator.md) (Mitigazione: Separatore di percorsi ZipArchiveEntry.FullName).|Microsoft Edge|  
  
<a name="Contracts"></a>   
## <a name="code-contracts"></a>Contratti di codice  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.Diagnostics.Contracts.Contract.Invariant%2A?displayProperty=fullName> e <xref:System.Diagnostics.Contracts.Contract.Requires%2A?displayProperty=fullName> e chiamate a <xref:System.String.IsNullOrEmpty%2A?displayProperty=fullName>|Per le app destinate a .NET Framework 4.6.1, il rewriter emette l'avviso del compilatore CC1036: "Detected call to method 'System.String.IsNullOrWhiteSpace(System.String)' without [Pure] in method..." ("Rilevata chiamata al metodo 'System.String.IsNullOrWhiteSpace(System.String)' senza [Pure] nel metodo...").|Si tratta di un avviso del compilatore, non di un errore del compilatore.<br /><br /> Questo comportamento è stato affrontato nel [problema GitHub n. 339](https://github.com/Microsoft/CodeContracts/issues/339). Per eliminare questo avviso, è possibile scaricare e compilare una versione aggiornata del codice sorgente per gli strumenti contratti di codice da [GitHub](https://github.com/Microsoft/CodeContracts/blob/master/README.md). Le informazioni per il download sono disponibili in fondo alla pagina.|Secondario|  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation"></a>Windows Communication Foundation  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=fullName><br /><br /> (spazio dei nomi <xref:System.IdentityModel.Claims>)|Nelle app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], se un set di attestazioni X509 viene inizializzato da un certificato con più voci DNS nel relativo campo SAN, il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A> tenta di far corrispondere l'argomento `claimType` a tutte le voci DNS.<br /><br /> Per le app destinate a versioni precedenti di .NET Framework, il metodo <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A> tenta di far corrispondere l'argomento `claimType` solo all'ultima voce DNS.|Questa modifica interessa tutte le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Le app destinate alle versioni precedenti di .NET Framework non sono interessate.<br /><br /> Le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], tuttavia, possono rifiutare questo comportamento. Possono invece accettare questo comportamento le app destinate a versioni precedenti di .NET Framework ma in esecuzione su [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Per altre informazioni, vedere [Mitigazione: Metodo X509CertificateClaimSet.FindClaims](../../../docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md).|Secondario|  
  
<a name="WinForms"></a>   
## <a name="windows-forms"></a>Windows Form  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Metodo <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName> (spazio dei nomi <xref:System.Windows.Forms>)|Nelle app di Windows Form destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], un'implementazione <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=fullName> personalizzata può filtrare in modo sicuro i messaggi quando viene chiamato il metodo <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName> se l'implementazione <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage%2A?displayProperty=fullName>:<br /><br /> <ul><li>Esegue una o entrambe le opzioni seguenti:<br /><br /> <ul><li>Aggiunge un filtro messaggio chiamando il metodo <xref:System.Windows.Forms.Application.AddMessageFilter%2A>.</li><li>Rimuove un filtro messaggio chiamando il metodo <xref:System.Windows.Forms.Application.RemoveMessageFilter%2A>. ProcessOnStatus.</li></ul></li><li>**E** immette i messaggi chiamando il metodo <xref:System.Windows.Forms.Application.DoEvents%2A?displayProperty=fullName>.</li></ul><br /> Nelle app Windows Form destinate a versioni precedenti di .NET Framework, questo tipo di implementazioni genera in alcuni casi un'eccezione <xref:System.IndexOutOfRangeException> quando viene chiamato il metodo <xref:System.Windows.Forms.Application.FilterMessage%2A?displayProperty=fullName>|Questa modifica interessa tutte le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Le app destinate alle versioni precedenti di .NET Framework non sono interessate.<br /><br /> Le app destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], tuttavia, possono rifiutare questo comportamento. Possono invece accettare questo comportamento le app destinate a versioni precedenti di .NET Framework ma in esecuzione su [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Per altre informazioni, vedere [Mitigazione: Implementazioni IMessageFilter.PreFilterMessage personalizzate](../../../docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md).|Microsoft Edge|  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità delle applicazioni nella versione 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)
