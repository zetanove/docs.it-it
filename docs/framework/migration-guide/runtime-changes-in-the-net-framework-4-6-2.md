---
title: Modifiche al runtime in .NET Framework 4.6.2 | Documenti di Microsoft
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
- runtime changes, .NET Framework
- runtime changes, .NET Framework 4.6.2
- application compatibility
ms.assetid: 23bf3a87-6fa1-4b5e-b92c-a39867a06e7f
caps.latest.revision: 16
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: da809955776b5a5cd3776898ecc4c97db74ceb0e
ms.lasthandoff: 04/18/2017

---
# <a name="runtime-changes-in-the-net-framework-462"></a>Modifiche al runtime in .NET Framework 4.6.2
In rari casi, le modifiche al runtime potrebbero incidere sulle app esistenti destinate alle versioni precedenti di .NET Framework, ma eseguite in una versione successiva del runtime di .NET Framework. Includono anche le differenze di comportamento tra le applicazioni eseguite in diversi ambienti di runtime di .NET Framework. [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] include modifiche nelle aree seguenti:  
  
-   [Base](#Core)  
  
-   [ASP.NET 2.0](#ASP)

-   [Dati](#Data)  
  
-   [Windows Communication Foundation (WCF)](#WCF)  
  
-   [Windows Presentation Foundation (WPF)](#WPF)  
  
-   [Firma XML e convalida](#XML)  
  
<a name="Core"></a>   
## <a name="core"></a>Base  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.Char.GetUnicodeCategory%2A?displayProperty=fullName><br /><br /> <xref:System.Globalization.CharUnicodeInfo.GetUnicodeCategory%2A?displayProperty=fullName>|Le categorie di caratteri in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] sono basate su Unicode versione 8.0. Le versioni di .NET Framework da 4.5 a 4.6.1 classificano i caratteri Unicode in base a Unicode versione 6.3.<br /><br /> Il confronto tra caratteri e l'ordinamento non sono interessati da questa modifica. Per altre informazioni, vedere la sezione "Stringhe e standard Unicode" nell'argomento della classe <xref:System.String>.|Le categorie di caratteri in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] potrebbero non corrispondere a quelle delle versioni precedenti di .NET Framework. Questa modifica interessa principalmente le sillabe Cherokee e i simboli delle vocali e dei toni di Tai lue semplificato.<br /><br /> Per risolvere questa modifica, esaminare codice e rimuovere o modificare la logica che dipende dalle categorie di caratteri Unicode hardcoded.|Secondario|  
|<xref:System.Security.Cryptography.RSA.ImportParameters%2A?displayProperty=fullName>, <xref:System.Security.Cryptography.RSACng.ImportParameters%2A?displayProperty=fullName>, <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey%2A?displayProperty=fullName>, <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey%2A?displayProperty=fullName>|A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questi metodi sono in grado di accedere alle chiavi con chiavi non standard per i certificati RSA. In [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti, il tentativo di accedere a tali chiavi ha generato un <xref:System.Security.Cryptography.CryptographicException>.|Se qualsiasi logica di gestione delle eccezioni si basa su un elemento <xref:System.Security.Cryptography.CryptographicException> quando vengono usate dimensioni delle chiavi non standard, questa deve essere rimossa.|Microsoft Edge|  
|<xref:System.Security.Cryptography.RSACng.VerifyHash%2A?displayProperty=fullName>|A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questo metodo restituisce `false` se la firma stessa non è formattata correttamente. Ora restituisce `false` per qualsiasi errore di verifica.<br /><br /> In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e 4.6.1, il metodo genera un'eccezione <xref:System.Security.Cryptography.CryptographicExceptio> se la firma non è formattata correttamente.|Qualsiasi codice la cui esecuzione dipende da <xref:System.Security.Cryptography.CryptographicException> deve invece essere eseguito se la convalida non va a buon fine e il metodo restituisce `false`.|Secondario|  
  
## <a name="a-nameasp--aspnet"></a><a name="ASP" /> ASP.NET

|Funzionalità|Modifica|Impatto|Ambito| 
|-------------|------------|------------|-----------|  
| <xref:System.Web.HttpRuntime.AppDomainApopPath%2A> | In .NET Framework 4.6.2, il runtime genera <xref:System.NullReferenceException> durante il recupero di un valore <xref:System.Web.HttpRuntime.AppDomainAppPath%2A> che include caratteri null. In .NET Framework 4.6.1 e versioni precedenti, viene generata un'eccezione <xref:System.ArgumentNullException>.  | È possibile eseguire le operazioni seguenti per rispondere a questa modifica: <br/> - Se l'applicazione è in esecuzione su .NET Framework 4.6.2, gestire <xref:System.NullReferenceException>. <br /> - Aggiornare a .NET Framework 4.7, che consente di ripristinare il comportamento precedente e genera un'eccezione <xref:System.ArgumentNullException>. | Microsoft Edge |

<a name="Data"></a>   
## <a name="data"></a>Dati  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Periodo di blocco del pool di connessioni per i database SQL di Azure|Il periodo di blocco del pool di connessioni è stato rimosso dalle richieste di connessione aperte ai database SQL di Azure noti.|Dopo gli errori di connessione del transiente, verranno effettuati tentativi quasi istantanei per ripetere le richieste di connessione aperte. Per altre informazioni, vedere [Mitigazione: Periodo di blocco del pool](~/docs/framework/migration-guide/mitigation-pool-blocking-period.md).|Secondario|  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=fullName> <br /> <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=fullName>|Quando si usa NetTcp con la sicurezza del trasporto e un tipo di certificato con credenziali, il protocollo SSL 3 non è più un protocollo predefinito usato per negoziare una connessione protetta.|Nella maggior parte dei casi non vi sarà alcun impatto sulle applicazioni esistenti, poiché TLS 1.0 è sempre stato incluso nell'elenco di protocolli per NetTcp. Tutti i client esistenti devono essere in grado di negoziare una connessione usando almeno TLS1.0.<br /><br /> Se è necessario il protocollo Ssl3, è possibile usare uno dei meccanismi di configurazione seguenti per aggiungerlo all'elenco dei protocolli negoziati:<br /><br /> - La proprietà <xref:System.ServiceModel.TcpTransportSecurity?displayProperty=fullName><br />- La proprietà <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=fullName><br />- La sezione [\<transport>](~/docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md) di [\<netTcpBinding>](~/docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)<br />- La sezione [\<sslStreamSecurity>](~/docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md) di [\<customBinding>](~/docs/framework/configure-apps/file-schema/wcf/custombinding.md)|Microsoft Edge|  
  
<a name="WPF"></a>   
## <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|La proprietà `IsEnabled` dell'elemento padre di un controllo <xref:System.Windows.Controls.TextBlock>|A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], la modifica della proprietà `IsEnabled` dell'elemento padre di un controllo <xref:System.Windows.Controls.TextBlock> ha effetto su tutti i controlli figlio (ad esempio collegamenti ipertestuali e pulsanti) del controllo <xref:System.Windows.Controls.TextBlock>.<br /><br /> In [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti di .NET Framework, i controlli all'interno di <xref:System.Windows.Controls.TextBlock> non sempre riflettono lo stato della proprietà `IsEnabled` dell'elemento padre <xref:System.Windows.Controls.TextBlock>.|Questa modifica è conforme al comportamento previsto per i controlli all'interno di un controllo <xref:System.Windows.Controls.TextBlock>.|Secondario|  
|Scorrimento orizzontale, virtualizzazione e <xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset%2A?displayProperty=fullName>|È stato modificato il comportamento dell'operazione di scorrimento di un elemento <xref:System.Windows.Controls.ItemsControl> che esegue la propria virtualizzazione in direzione ortogonale alla direzione di scorrimento principale.|La modifica produce un'esperienza più prevedibile e intuitiva per l'utente finale, ma può influire su qualsiasi applicazione che dipende dal valore esatto di <xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset%2A?displayProperty=fullName> dopo una operazione di scorrimento orizzontale. Per altre informazioni, vedere [Mitigazione: Scorrimento orizzontale e virtualizzazione](~/docs/framework/migration-guide/mitigation-horizontal-scrolling-and-virtualization.md).|Secondario|  
|Controllo ortografico WPF (classe <xref:System.Windows.Controls.SpellCheck?displayProperty=fullName>)|In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] sono stati segnalati tre problemi nel controllo ortografico di WPF durante l'esecuzione di [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]:<br /><br /> - In [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], il correttore ortografico genera talvolta un'eccezione <xref:System.Runtime.InteropServices.COMException> quando si richiamano i metodi [ISpellChecker](https://msdn.microsoft.com/library/windows/desktop/hh869767\(v=vs.85\).aspx) o [ISpellCheckerFactory](https://msdn.microsoft.com/library/windows/desktop/hh869770\(v=vs.85\).aspx). In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], queste eccezioni sono state eliminate.<br />- In [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], il correttore ortografico identifica in modo errato gli errori di ortografia di parole composte, ad esempio "Hausnummer" in tedesco. In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], il correttore ortografico gestisce correttamente le parole composte.<br />- In [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], il correttore ortografico genera un'eccezione <xref:System.UnauthorizedAccessException> quando un'applicazione viene avviata tramite "Esegui come utente diverso". In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questo scenario non è supportato e il controllo ortografico viene disabilitato automaticamente.|Queste modifiche consentono di migliorare l'affidabilità del correttore ortografico.  Essi non dovrebbero incidere negativamente su un'applicazione, a meno che il relativo codice non dipenda da un'eccezione generata.|Microsoft Edge|  
| Metodo [DataGridCellsPanel.BringIndexIntoView](xref:System.Windows.Controls.DataGridCellsPanel.BringIndexInfoView(System.Int32)) | In .NET Framework 4.6.2, il metodo **BringIndexIntoView** viene eseguito in modo asincrono quando è abilitata la virtualizzazione delle colonne la cui larghezza tuttavia non è stata determinata. Tuttavia, se le colonne vengono rimosse prima che venga completata l'operazione asincrona, può verificarsi un evento [ArgumentOutOfRangeException](xref:System.ArgumentOutOfRangeException).<br/></br>A partire da .NET Framework 4.7, l'eccezione non viene più generata in questo scenario. | È possibile eseguire una delle operazioni seguenti per impedire che si verifichi l'eccezione: <br/> - Eseguire l'aggiornamento a .NET Framework 4.7. <br/> 1 Installare la patch più recente per la manutenzione di .NET Framework 4.6.2. <br/> - Evitare di rimuovere colonne fino al completamento della risposta asincrona al metodo [DataGrid.ScrollIntoView](xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)). | Microsoft Edge | 
  
<a name="XML"></a>   
## <a name="signed-xml-verification-requirements"></a>Requisiti di verifica XML firmati  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=fullName> e <xref:System.Security.Cryptography.Xml.EncryptedXml?displayProperty=fullName>|Il caricamento delle risorse esterne è disabilitato e le destinazioni ambigue degli ID vengono considerate non valide.|Viene generata un'eccezione in diversi casi, tra cui:<br /><br /> - Identificazione di un elemento da un attributo ID e definizione di un secondo elemento con lo stesso identificatore<br />- Definizione di un identificatore che non è un valore `NCName` valido.<br />- Riferimento a URI esterni.<br /><br /> <xref:System.Security.Cryptography.Xml.SignedXml.CheckSignature%2A?displayProperty=fullName> restituisce sempre `false` per i documenti:<br /><br /> - Che usano la trasformazione dei riferimenti di XPath.<br />- Che usano la trasformazione dei riferimenti di XSLT.<br /><br /> Gli sviluppatori devono esaminare l'uso di <xref:System.Security.Cryptography.Xml.XmlDsigXPathTransform?displayProperty=fullName> e <xref:System.Security.Cryptography.Xml.XmlDsigXsltTransform> nonché dei tipi derivati da <xref:System.Security.Cryptography.Xml.Transform?displayProperty=fullName>, poiché un destinatario del documento potrebbe non essere in grado di elaborarlo.<br /><br /> Per altre informazioni, vedere [Dopo aver applicato l'aggiornamento di sicurezza 3141780, le applicazioni .NET Framework riscontrano errori di eccezione o errori imprevisti durante l'elaborazione di file che contengono SignedXml](https://support.microsoft.com/en-us/kb/3148821).|Secondario|  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità delle applicazioni nella versione 4.6.2](~/docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-2.md)
