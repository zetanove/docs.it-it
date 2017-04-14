---
title: "Risorse nelle applicazioni desktop | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "risorse delle applicazioni"
  - "distribuzione di applicazioni [.NET Framework], risorse"
  - "localizzazione"
  - "risorse (localizzazione)"
  - "creazione di pacchetti di risorse dell'applicazione"
  - "file di risorse"
  - "assembly satellite"
ms.assetid: 8ad495d4-2941-40cf-bf64-e82e85825890
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Risorse nelle applicazioni desktop
Quasi tutte le applicazioni destinate a un impiego professionale richiedono l'utilizzo di risorse.  Una risorsa è costituita da dati non eseguibili che vengono distribuiti con l'applicazione stessa.  Una risorsa può essere visualizzata in un'applicazione sotto forma di messaggi di errore o come parte dell'interfaccia utente.  Le risorse possono contenere dati in diversi formati, tra cui stringhe, immagini e oggetti persistenti. \(Per scrivere oggetti persistenti in un file di risorse, è necessario che gli oggetti siano serializzabili.\) L'archiviazione di dati in un file di risorse consente di modificare i dati senza ricompilare l'intera applicazione.  Inoltre consente di archiviare i dati in un'unica posizione ed elimina la necessità di basarsi sui dati specificati a livello di codice archiviati in più posizioni.  
  
 .NET Framework offre ampio supporto per la creazione e la localizzazione delle risorse nelle applicazioni desktop.  .NET Framework supporta inoltre un modello semplice per la creazione del package e la distribuzione delle risorse localizzate nella applicazioni desktop.  
  
 Per informazioni sulle risorse in ASP.NET, vedere [ASP.NET Web Page Resources Overview](../Topic/ASP.NET%20Web%20Page%20Resources%20Overview.md) nel Centro per sviluppatori di Internet Explorer.  
  
 Le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] utilizzano un modello diverso delle risorse dalle applicazioni desktop e contengono le relative risorse in un singolo file indice di risorse del pacchetto \(PRI\).  Per informazioni sulle risorse nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], vedere [Creare e recuperare le risorse nelle applicazioni di Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=241674) nel Windows Dev Center.  
  
## Creazione e localizzazione delle risorse  
 In un'applicazione non localizzata, è possibile utilizzare i file di risorse come archivio per i dati dell'applicazione, in particolare per le stringhe che possono essere altrimenti hard\-coded in più posizioni nel codice sorgente.  In genere, si creano le risorse come testo \(.txt\) o file XML \(.resx\) e si utilizza [Resgen.exe \(Resource File Generator\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) per compilarli in file binari .resources.  Questi file possono quindi essere incorporati nel file eseguibile dell'applicazione tramite un compilatore di linguaggio.  Per ulteriori informazioni sulla creazione di risorse, vedere [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md).  
  
 È anche possibile localizzare le risorse dell'applicazione per impostazioni cultura specifiche.  In tal modo è possibile compilare versioni localizzate \(tradotte\) delle applicazioni.  Quando si sviluppa un'applicazione che utilizza risorse localizzate, è possibile definire l'impostazione cultura che funge come neutrale o impostazioni cultura di fallback le cui risorse vengono utilizzate se non sono disponibili risorse appropriate.  In genere, le risorse delle impostazioni cultura neutrali vengono memorizzate nel file eseguibile dell'applicazione.  Le risorse rimanenti per le impostazioni cultura localizzate individuali vengono memorizzate in assembly satellite autonomi.  Per ulteriori informazioni, vedere [Creazione di assembly satellite](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md).  
  
## Creazione del package e distribuzione delle risorse  
 Si sviluppano risorse localizzate di applicazione in [assembly satellite](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  Un assembly satellite contiene le risorse per una singola impostazioni cultura; non contengono codice dell'applicazione.  Nel modello di distribuzione di assembly satellite, viene creata un'applicazione con l'assembly predefinito \(in genere l'assembly principale\) e un assembly satellite per tutte le impostazioni cultura supportate dall'applicazione.  Poiché gli assembly satellite non fanno parte dell'assembly principale, è possibile sostituire o aggiornare facilmente le risorse corrispondenti a impostazioni cultura specifiche senza sostituire l'assembly principale dell'applicazione.  
  
 Determinare con attenzione le risorse che costituiranno l'assembly di risorse predefinito dell'applicazione.  Poiché tale assembly fa parte dell'assembly principale, le eventuali modifiche ad esso apportate richiederanno la sostituzione dell'assembly principale.  Se non viene fornita una risorsa predefinita, quando il processo di [recupero di una risorsa di riserva](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md) proverà a cercarla verrà generata un'eccezione.  In un'applicazione progettata correttamente, l'utilizzo delle risorse non deve mai generare un'eccezione.  
  
 Per ulteriori informazioni, vedere l'articolo [Creazione del pacchetto e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  
  
## Recupero risorse  
 In fase di esecuzione, le applicazioni caricano le risorse localizzate appropriate per ciascun thread, in base alle impostazioni cultura specificate dalla proprietà <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>.  Questo valore della proprietà viene derivato come segue:  
  
-   Assegnando direttamente un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura localizzate alla proprietà <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=fullName>.  
  
-   Se le impostazioni cultura non vengono assegnate in modo esplicito, recuperando il thread predefinito delle impostazioni cultura dell'interfaccia utente dalla proprietà <xref:System.Globalization.CultureInfo.DefaultThreadCurrentUICulture%2A?displayProperty=fullName>.  
  
-   Se il thread predefinito delle impostazioni cultura dell'interfaccia utente non viene assegnato in modo esplicito, recuperando le impostazioni cultura dell'utente corrente del computer locale chiamando la funzione `GetUserDefaultUILanguage` di Windows.  
  
 Per ulteriori informazioni su come vengono impostate le impostazioni cultura correnti dell'interfaccia utente, vedere le pagine riferimento <xref:System.Globalization.CultureInfo> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>.  
  
 È quindi possibile recuperare le risorse per le impostazioni cultura correnti dell'interfaccia utente o per impostazioni cultura specifiche utilizzando la classe <xref:System.Resources.ResourceManager?displayProperty=fullName>.  Sebbene la classe <xref:System.Resources.ResourceManager> sia più utilizzata per recuperare le risorse nelle applicazioni desktop, lo spazio dei nomi <xref:System.Resources?displayProperty=fullName> contiene tipi aggiuntivi utilizzabili per recuperare le risorse.  tra cui:  
  
-   La classe <xref:System.Resources.ResourceReader>, che consente di enumerare le risorse incorporate in un assembly o archiviate in un file binario .resources autonomo.  È utile quando non si conoscono i nomi esatti delle risorse disponibili in fase di esecuzione.  
  
-   La classe <xref:System.Resources.ResXResourceReader>, che consente di recuperare le risorse da un file XML \(.resx\).  
  
-   La classe <xref:System.Resources.ResourceSet>, che consente di recuperare le risorse per impostazioni cultura specifiche senza rispettare le regole di fallback.  Le risorse possono essere archiviate in un assembly o un file binario .resources autonomo.  È inoltre possibile sviluppare un'implementazione <xref:System.Resources.IResourceReader> che consente di utilizzare la classe <xref:System.Resources.ResourceSet> per recuperare le risorse da un'altra origine.  
  
-   La classe <xref:System.Resources.ResXResourceSet>, che consente di recuperare tutti gli elementi in un file di risorse XML in memoria.  
  
## Vedere anche  
 <xref:System.Globalization.CultureInfo>   
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>   
 [Concetti di base sulle applicazioni](../../../docs/standard/application-essentials.md)   
 [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)   
 [Creazione del pacchetto e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)   
 [Creazione di assembly satellite](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md)   
 [Recupero di risorse](../../../docs/framework/resources/retrieving-resources-in-desktop-apps.md)