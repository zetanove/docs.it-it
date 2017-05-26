---
title: Reindirizzamento delle modifiche in .NET Framework 4.6.2 | Microsoft Docs
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes, .NET Framework
- retargeting changes, .NET Framework 4.6.2
- application compatibility
ms.assetid: 76dc6849-8210-4e41-8731-20828c98b282
caps.latest.revision: 26
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 229ccf3fa4ff1029334641da350cfd040e4b286e
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="retargeting-changes-in-the-net-framework-462"></a>Reindirizzamento delle modifiche in .NET Framework 4.6.2
In rari casi, le modifiche di reindirizzamento possono influire sulle app che vengono ricompilate per [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]. Non influiscono sui file binari destinati a una versione precedente di .NET Framework ma vengono eseguiti nella versione 4.6.2. [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] include le modifiche di reindirizzamento nelle aree seguenti:  
  
-   [Base](#Core)  
  
-   [Windows Communication Foundation (WCF)](#WCF)  
  
-   [Windows Form](#WinForms)  
  
 La colonna Ambito nelle tabelle seguenti contiene il significato di ogni modifica:  
  
-   Principale Una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice. Si noti che le modifiche di reindirizzamento non rientrano in questa categoria.  
  
-   Secondaria. Una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.  
  
-   Bordo. Una modifica che influisce sulle app in scenari molto specifici e non comuni.  
  
-   Trasparente. Una modifica che non ha effetti evidenti sullo sviluppatore o sull'utente dell'app. L'app non dovrebbe richiedere variazioni a causa di questa modifica.  
  
<a name="Core"></a>   
## <a name="core"></a>Base  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Supporto del percorso lungo|A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], sono supportati i percorsi lunghi (di un massimo di 32 mila caratteri) e la limitazione sulle lunghezze di percorso da 260 caratteri (o `MAX_PATH`) è stata eliminata.|Per le applicazioni che usano [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], i percorsi di codice che in precedenza generavano <xref:System.IO.PathTooLongException> non possono più generare un'eccezione. Per altre informazioni, vedere [Mitigazione: Supporto del percorso lungo](~/docs/framework/migration-guide/mitigation-long-path-support.md).|Secondario|  
|Normalizzazione del percorso|A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], è cambiato il modo in cui vengono normalizzati i percorsi per rinviare al sistema operativo e per fornire un accesso migliore ai percorsi del dispositivo DOS.|Le modifiche consentono di accedere ai percorsi validi del dispositivo che in precedenza non erano supportati. Per altre informazioni, vedere [Mitigazione: Normalizzazione del percorso](~/docs/framework/migration-guide/mitigation-path-normalization.md).|Secondario|  
|<xref:System.IO.Path.GetDirectoryName%2A?displayProperty=fullName> e <xref:System.IO.Path.GetPathRoot%2A?displayProperty=fullName>|A partire dalle applicazioni dedicate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], sono state apportate alcune modifiche per supportare i percorsi in precedenza non supportati (entrambi in termini di lunghezza e il formato). In particolare, i controlli per la sintassi del separatore dell'unità appropriata (due punti) sono stati resi più corretti.|Queste modifiche bloccano alcuni percorsi URI che questi due metodi supportavano in precedenza. Per altre informazioni, vedere [Mitigazione: Verifica della presenza dei due punti nel percorso](~/docs/framework/migration-guide/mitigation-path-colon-checks.md).|Microsoft Edge|  
|Costruttore <xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29?displayProperty=fullName>|A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], la proprietà <xref:System.Security.Claims.ClaimsIdentity.Actor%2A> creata da una chiamata al metodo <xref:System.Security.Claims.ClaimsIdentity.%23ctor%28System.Security.Principal.IIdentity%29?displayProperty=fullName> è una nuova istanza di <xref:System.Security.Claims.ClaimsIdentity>. Nelle versioni precedenti di .NET Framework, <xref:System.Security.Claims.ClaimsIdentity.Actor%2A> è un riferimento esistente.|In alcuni casi, il confronto tra la proprietà <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=fullName> con la proprietà <xref:System.Security.Claims.ClaimsIdentity.Actor%2A?displayProperty=fullName> di <xref:System.Security.Principal.IIdentity> del costruttore restituisce risultati diversi.<br /><br /> Per altre informazioni, vedere [Mitigazione: Costruttore ClaimsIdentity](~/docs/framework/migration-guide/mitigation-claimsidentity-constructor.md).|Microsoft Edge|  
|<xref:System.Security.Cryptography.AesCryptoServiceProvider.CreateDecryptor%2A?displayProperty=fullName>|A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], il componente di decrittografia <xref:System.Security.Cryptography.AesCryptoServiceProvider> fornisce una trasformazione riutilizzabile.   Dopo una chiamata a <xref:System.Security.Cryptography.ICryptoTransform.TransformFinalBlock%2A>, la trasformazione viene reinizializzata e può essere riutilizzata.<br /><br /> Per le applicazioni destinate a versioni precedenti di .NET Framework, il tentativo di riusare il componente di decrittografia chiamando <xref:System.Security.Cryptography.ICryptoTransform.TransformBlock%2A> dopo una chiamata a <xref:System.Security.Cryptography.ICryptoTransform.TransformFinalBlock%2A> genera un'eccezione <xref:System.Security.Cryptography.CryptographicException> o produce dati danneggiati.|L'impatto dovrebbe essere minimo, poiché si tratta del comportamento previsto.<br /><br /> Le applicazioni che dipendono dal comportamento precedente la possono rifiutare esplicitamente aggiungendo l'impostazione di configurazione seguente alla sezione [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'applicazione:<br /><br /> `<runtime>    <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.AesCryptoServiceProvider.DontCorrectlyResetDecryptor=true"/> </runtime>`<br /><br /> Le applicazioni destinate a versioni precedenti di .NET Framework ma in esecuzione su una versione uguale o successiva a .NET Framework [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] possono optare per questo comportamento aggiungendo l'impostazione di configurazione seguente alla sezione [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'applicazione:<br /><br /> `<runtime>    <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.AesCryptoServiceProvider.DontCorrectlyResetDecryptor=false"/> </runtime>`|Secondario|  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Supporto della sicurezza del trasporto WCF per i certificati archiviati usando CNG|A partire dalle app destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], la sicurezza del trasporto WCF supporta i certificati archiviati usando la libreria di crittografia di Windows (CNG). Questo supporto è limitato ai certificati con una chiave pubblica che ha un esponente di lunghezza non superiore a 32 bit. Quando un'applicazione ha come destinazione [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questa funzionalità è attivata per impostazione predefinita.<br /><br /> Nelle versioni precedenti di .NET Framework, il tentativo di usare i certificati X509 con un provider di archiviazione chiavi CSG genera un'eccezione.|Le applicazioni destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti, ma in esecuzione su [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], possono abilitare il supporto per i certificati CNG aggiungendo la riga seguente alla sezione runtime del file app.config o web.config.<br /><br /> `<AppContextSwitchOverrides     value="Switch.System.ServiceModel.DisableCngCertificates=false" />`<br /><br /> L'operazione può essere eseguita anche con il codice seguente:<br /><br /> `private const string DisableCngCertificates = @"Switch.System.ServiceModel.DisableCngCertificate"; AppContext.SetSwitch(disableCngCertificates, false);`<br /><br /> `Const DisableCngCertificates As String = "Switch.System.ServiceModel.DisableCngCertificates" AppContext.SetSwitch(disableCngCertificates, False)`<br /><br /> Si noti che, grazie a questa modifica, i codici di gestione delle eccezioni che dipendono dal tentativo di avviare una comunicazione protetta con un certificato CNG di esito negativo non verranno più eseguiti.|Secondario|  
  
<a name="WinForms"></a>   
## <a name="windows-forms"></a>Windows Form  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=fullName>, `System.ComponentModel.EventDescriptor.Equals` e `System.ComponentModel.PropertyDescriptor.Equals`|A partire dalle applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], l'implementazione del metodo della classe base <xref:System.ComponentModel.MemberDescriptor.Equals%2A> è stata modificata.|Poiché il test di uguaglianza ora produce il risultato previsto, questa modifica dovrebbe avere un impatto minimo.<br /><br /> Tuttavia, le applicazioni destinate a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] e che dipendono dal precedente comportamento possono rifiutare esplicitamente questa modifica. Analogamente, le applicazioni destinate alle versioni precedenti di .NET Framework ma che vengono eseguite in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] possono acconsentire esplicitamente a questa modifica. Per altre informazioni, vedere [Mitigazione: MemberDescriptor.Equals](~/docs/framework/migration-guide/mitigation-memberdescriptor-equals.md).|Microsoft Edge|  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità delle applicazioni nella versione 4.6.2](~/docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-2.md)
