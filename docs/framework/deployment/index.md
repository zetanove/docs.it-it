---
title: Distribuzione di .NET Framework e delle applicazioni | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- deploying applications [.NET Framework], packaging
- deploying applications [.NET Framework]
- deploying applications [.NET Framework], features
- deploying applications [.NET Framework], distribution
- .NET Framework, deploying
- .NET Framework application deployment
ms.assetid: 238d8284-6042-4a38-a7f6-1ee8efd719da
caps.latest.revision: 56
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: fe9ab371ab8d3eee3778412e446b7aa30b42476b
ms.openlocfilehash: 46f524a8c2ee2d65d5c756a101a5c26c5919e165
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="deploying-the-net-framework-and-applications"></a>Distribuzione di .NET Framework e delle applicazioni
Questo articolo consente di iniziare a distribuire .NET Framework con l'applicazione. La maggior parte delle informazioni, sono destinate agli sviluppatori OEM e agli amministratori aziendali. È consigliabile che gli utenti che vogliono installare .NET Framework leggano [Installare .NET Framework](~/docs/framework/install/index.md).  
  
## <a name="key-deployment-resources"></a>Risorse principali di distribuzione  
 Usare i seguenti collegamenti ad altri argomenti di MSDN per informazioni specifiche sulla distribuzione e sui servizi di .NET Framework.  
  
 **Installazione e distribuzione**  
  
-   Installazione generica ed informazioni di distribuzione:  
  
    -   Opzioni del programma di installazione:  
  
        -   [Programma di installazione Web](~/docs/framework/install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)  
  
        -   [Programma di installazione offline](~/docs/framework/install/guide-for-developers.md#to-install-or-download-the-net-framework-redistributable)  
  
    -   Modalità di installazione:  
  
        -   [Installazione invisibile all'utente](../../../docs/framework/deployment/deployment-guide-for-developers.md#chaining_custom)  
  
        -   [Visualizzazione di un'interfaccia utente](../../../docs/framework/deployment/deployment-guide-for-developers.md#chaining_default)  
  
    -   [Riduzione dei riavvii del sistema durante le installazioni di .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md)  
  
    -   [Risolvere i problemi relativi alle installazioni e alle disinstallazioni bloccate di .NET Framework](~/docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)  
  
-   Distribuzione di .NET Framework in un'applicazione client (per gli sviluppatori):   
  
    -   [Uso di InstallShield](../../../docs/framework/deployment/deployment-guide-for-developers.md#installshield-deployment) in un progetto di installazione e distribuzione  
  
    -   [Uso di un'applicazione ClickOnce di Visual Studio](../../../docs/framework/deployment/deployment-guide-for-developers.md#clickonce-deployment)  
  
    -   [Creazione di un pacchetto di installazione WiX](../../../docs/framework/deployment/deployment-guide-for-developers.md#wix)  
  
    -   [Uso di un programma di installazione personalizzato](../../../docs/framework/deployment/deployment-guide-for-developers.md#chaining)  
  
    -   [Altre informazioni](../../../docs/framework/deployment/deployment-guide-for-developers.md) per sviluppatori  
  
-   Distribuzione di .NET Framework (per gli OEM e gli amministratori):  
  
    -   [Windows Assessment and Deployment Kit (ADK)](http://go.microsoft.com/fwlink/p/?LinkId=254976)  
  
    -   [Guida dell'amministratore](../../../docs/framework/deployment/guide-for-administrators.md)  
  
 **Manutenzione**  
  
-   Per informazioni generali, vedere il [blog di .NET Framework](http://go.microsoft.com/fwlink/p/?LinkId=254977)  
  
-   [Determinazione delle versioni](../../../docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)  
  
-   [Determinazione di service pack e aggiornamenti](../../../docs/framework/migration-guide/how-to-determine-which-net-framework-updates-are-installed.md)  
  
## <a name="features-that-simplify-deployment"></a>Funzionalità che semplificano la distribuzione  
 In .NET Framework sono disponibili diverse funzionalità di base che semplificano la distribuzione delle applicazioni:  
  
-   Indipendenza delle applicazioni.  
  
     Questa funzionalità fornisce l'isolamento delle applicazioni ed elimina i conflitti di DLL. Per impostazione predefinita i componenti di un'applicazione non influenzano il funzionamento di altre applicazioni.  
  
-   Componenti privati per impostazione predefinita.  
  
     Per impostazione predefinita, i componenti vengono distribuiti nella directory dell'applicazione e sono visibili solo a tale applicazione.  
  
-   Condivisione controllata del codice.  
  
     La condivisione del codice richiede che il codice venga reso disponibile per la condivisione in modo esplicito, in quanto non è condiviso per impostazione predefinita.  
  
-   Controllo delle versioni side-by-side.  
  
     È possibile creare più versioni di un componente o di un'applicazione e specificare la versione da usare. I criteri di gestione delle versioni sono attivati da Common Language Runtime.  
  
-   Distribuzione e replica XCOPY.  
  
     È possibile distribuire applicazioni e componenti autodescrittivi e indipendenti senza voci del Registro di sistema o dipendenze.  
  
-   Aggiornamenti al volo.  
  
     Gli amministratori possono aggiornare le DLL dei programmi usando host, ad esempio ASP.NET, anche su computer remoti.  
  
-   Integrazione con Windows Installer.  
  
     Durante la distribuzione di un'applicazione sono disponibili le funzioni di annuncio, pubblicazione, ripristino e installazione su richiesta.  
  
-   Distribuzione aziendale.  
  
     Questa funzionalità semplifica la distribuzione di software, anche mediante Active Directory.  
  
-   Download e memorizzazione nella cache.  
  
     I download incrementali consentono di limitare le dimensioni degli oggetti scaricati e i componenti possono essere isolati per consentirne l'uso solo da parte dell'applicazione, in modo da ridurre al minimo l'impatto della distribuzione.  
  
-   Codice parzialmente attendibile.  
  
     L'identità è basata sul codice anziché sull'utente e non viene visualizzata alcuna finestra di dialogo relativa ai certificati.  
  
## <a name="packaging-and-distributing-net-framework-applications"></a>Creazione di pacchetti e distribuzione di applicazioni .NET Framework  
 Alcuni concetti relativi alla creazione di pacchetti e alla distribuzione in .NET Framework vengono illustrati in altre sezioni della documentazione. Queste sezioni includono informazioni sulle unità autodescrittive denominate [assembly](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md), che non richiedono voci nel Registro di sistema, sugli [assembly con nome sicuro](../../../docs/framework/app-domains/strong-named-assemblies.md), che assicurano l'univocità dei nomi e prevengono lo spoofing dei nomi e sul [controllo delle versioni degli assembly](../../../docs/framework/app-domains/assembly-versioning.md), che consente di risolvere molti dei problemi associati ai conflitti di DLL. Le sezioni seguenti forniscono informazioni sulla creazione di pacchetti e sulla distribuzione di applicazioni .NET Framework.  
  
### <a name="packaging"></a>Pacchetto  
 .NET Framework consente di creare i pacchetti delle applicazioni nei seguenti modi:  
  
-   Come singolo assembly o come una raccolta di assembly.  
  
     Con questa opzione è sufficiente usare i file DLL o EXE così come sono stati compilati.  
  
-   Come file cabinet (CAB).  
  
     Con questa opzione i file vengono compressi in file CAB per ridurre il tempo necessario per la distribuzione o il download.  
  
-   Come pacchetto di Windows Installer o programmi di installazione in altri formati.  
  
     Con questa opzione vengono creati file MSI che possono essere usati con Windows Installer oppure viene creato un pacchetto dell'applicazione per l'uso con altri programmi di installazione.  
  
### <a name="distribution"></a>Distribuzione  
 .NET Framework consente di distribuire le applicazioni nei seguenti modi:  
  
-   Mediante XCOPY o FTP.  
  
     Poiché le applicazioni Common Language Runtime sono autodescrittive e non richiedono alcuna voce nel Registro di sistema, è possibile usare XCOPY o FTP per copiare semplicemente l'applicazione in una directory appropriata. L'applicazione potrà quindi essere eseguita da tale directory.  
  
-   Mediante download del codice.  
  
     Se l'applicazione viene distribuita su Internet o su una rete Intranet aziendale, è possibile effettuare il download del codice su un computer ed eseguire l'applicazione su tale computer.  
  
-   Mediante un programma di installazione come Windows Installer 2.0.  
  
     Windows Installer 2.0 consente di installare, ripristinare o rimuovere assembly .NET Framework nella Global Assembly Cache e in directory private.  
  
### <a name="installation-location"></a>Percorso di installazione  
 Per determinare dove distribuire gli assembly dell'applicazione per consentirne l'individuazione da parte del runtime, vedere [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md).  
  
 La modalità di distribuzione delle applicazioni dipende anche da alcune considerazioni sulla sicurezza. Le autorizzazioni di sicurezza vengono concesse al codice gestito in base alla posizione del codice. La distribuzione di un'applicazione o di un componente in una posizione con un livello di attendibilità basso, ad esempio Internet, comporta la limitazione delle operazioni che possono essere eseguite dall'applicazione o dal componente. Per altre informazioni sulla distribuzione e considerazioni relative alla sicurezza, vedere [Nozioni fondamentali sulla sicurezza per l'accesso al codice](../../../docs/framework/misc/code-access-security-basics.md).  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)|Descrive come Common Language Runtime determina l'assembly da usare per eseguire una richiesta di associazione.|  
|[Procedure consigliate per il caricamento di assembly](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)|Illustra come evitare problemi di identità del tipo che possono causare la generazione di eccezioni <xref:System.InvalidCastException>, <xref:System.MissingMethodException> e altri errori.|  
|[Riduzione dei riavvii del sistema durante le installazioni di .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md)|Descrive il gestore di riavvio, che impedisce automaticamente il riavvio quando possibile, e viene illustrato come le applicazioni che installano .NET Framework possano usufruirne.|  
|[Guida alla distribuzione per amministratori](../../../docs/framework/deployment/guide-for-administrators.md)|Illustra le modalità in cui un amministratore di sistema può distribuire .NET Framework e le relative dipendenze di sistema attraverso una rete usando System Center Configuration Manager (SCCM).|  
|[Guida alla distribuzione per gli sviluppatori](../../../docs/framework/deployment/deployment-guide-for-developers.md)|Illustra come gli sviluppatori possono installare .NET Framework nei computer dei rispettivi utenti con le rispettive applicazioni.|  
|[Distribuzione di applicazioni, servizi e componenti](https://docs.microsoft.com/visualstudio/deployment/deploying-applications-services-and-components)|Illustra le opzioni di distribuzione di Visual Studio, incluse le istruzioni per la pubblicazione di un'applicazione usando le tecnologie ClickOnce e Windows Installer.| 
|[Pubblicazione di applicazioni ClickOnce](/visualstudio/deployment/publishing-clickonce-applications)|Descrive come creare il pacchetto di un'applicazione Windows Forms e distribuirla con ClickOnce nei computer client di una rete.|  
|[Creazione del pacchetto e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)|Descrive il modello hub e spoke usato da .NET Framework per creare pacchetti e distribuire le risorse. Vengono illustrate le convenzioni di denominazione, i processi di fallback e le possibilità alternative di creazione di pacchetti delle risorse.|  
|[Distribuzione di una applicazione di interoperabilità](../../../docs/framework/interop/deploying-an-interop-application.md)|Illustra come fornire e installare applicazioni di interoperabilità, che in genere includono un assembly client .NET Framework, uno o più assembly di interoperabilità che rappresentano librerie dei tipi COM distinte e uno o più componenti COM registrati.|  
|[Procedura: Ottenere lo stato di avanzamento dal programma d'installazione di .NET Framework 4.5](../../../docs/framework/deployment/how-to-get-progress-from-the-dotnet-installer.md)|Descrive come avviare e rilevare automaticamente il processo di installazione di .NET Framework pur mostrando la propria visualizzazione dello stato di avanzamento dell'installazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di sviluppo](../../../docs/framework/development-guide.md)

