---
title: Risorse nelle applicazioni desktop | Documentazione Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deploying applications [.NET Framework], resources
- application resources
- resource files
- satellite assemblies
- localization
- packaging application resources
- localizing resources
ms.assetid: 8ad495d4-2941-40cf-bf64-e82e85825890
caps.latest.revision: 19
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: 3bbfaf3272444fbd2127f01ae4d5c9ca0db7bd39
ms.lasthandoff: 04/08/2017

---
# <a name="resources-in-desktop-apps"></a>Risorse nelle applicazioni desktop
L'utilizzo di risorse è richiesto in quasi tutte le applicazioni destinate a un impiego professionale. Una risorsa è costituita da dati non eseguibili che vengono distribuiti in modo logico con un'applicazione. Una risorsa può essere visualizzata in un'applicazione sotto forma di messaggi di errore o come parte dell'interfaccia utente. Le risorse possono contenere dati in diversi formati, tra cui stringhe, immagini e oggetti persistenti. Per scrivere oggetti persistenti in un file di risorse, è necessario che gli oggetti siano serializzabili. L'archiviazione dei dati in un file di risorse consente di modificare i dati senza ricompilare l'intera applicazione. Inoltre permette di archiviare i dati in un'unica posizione e non è più necessario basarsi sui dati specificati a livello di codice archiviati in più posizioni.  
  
 .NET Framework offre ampio supporto per la creazione e la localizzazione delle risorse nelle applicazioni desktop. .NET Framework supporta inoltre un modello semplice per la creazione del pacchetto e la distribuzione delle risorse localizzate nella applicazioni desktop.  
  
 Per informazioni sulle risorse in ASP.NET, vedere [Cenni preliminari sulle risorse delle pagine Web ASP.NET](http://msdn.microsoft.com/library/0936b3b2-9e6e-4abe-9c06-364efef9dbbd) nel Centro per sviluppatori Internet Explorer.  
  
 Nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] viene utilizzato un modello di risorse diverso dalle applicazioni desktop e le relative risorse vengono archiviate in un singolo file indice di risorse del pacchetto (PRI). Per informazioni sulle risorse nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], vedere [Creazione e recupero di risorse nelle applicazioni Windows Store](http://go.microsoft.com/fwlink/p/?LinkId=241674) nel Centro per sviluppatori Windows.  
  
## <a name="creating-and-localizing-resources"></a>Creazione e localizzazione di risorse  
 In un'applicazione non localizzata, è possibile utilizzare i file di risorse come repository per i dati dell'applicazione, in particolare per le stringhe che altrimenti possono essere hard-coded in più posizioni nel codice sorgente. In genere, le risorse vengono create come testo, con estensione txt o come o file XML (RESX) e si utilizza [Resgen.exe (Resource File Generator)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) per compilarle in file binari con estensione resources. Questi file possono quindi essere incorporati nel file eseguibile dell'applicazione tramite un compilatore di linguaggio. Per altre informazioni sulla creazione di file di risorse, vedere [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md).  
  
 È anche possibile localizzare le risorse dell'applicazione per impostazioni cultura specifiche. In questo modo è possibile compilare versioni localizzate (tradotte) delle applicazioni. Quando si sviluppa un'applicazione in cui vengono utilizzate risorse localizzate, è possibile definire delle impostazioni cultura che fungono da impostazioni cultura non associate ad alcun paese o di fallback le cui risorse vengono utilizzate se non ve ne sono di appropriate. In genere, le risorse delle impostazioni cultura non associate ad alcun paese vengono archiviate nel file eseguibile dell'applicazione. Le risorse rimanenti per le singole impostazioni cultura localizzate vengono archiviate in assembly satellite autonomi. Per altre informazioni, vedere [Creazione di assembly satellite](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md).  
  
## <a name="packaging-and-deploying-resources"></a>Creazione del pacchetto e distribuzione delle risorse  
 Si sviluppano risorse di applicazioni localizzate in [assembly satellite](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md). In un assembly satellite sono contenute le risorse di singole impostazioni cultura e non il codice dell'applicazione. Nel modello di distribuzione dell'assembly satellite si crea un'applicazione con un assembly predefinito (in genere l'assembly principale) e un assembly satellite per tutte le impostazioni cultura supportate dall'applicazione. Poiché gli assembly satellite non fanno parte dell'assembly principale, è possibile sostituire o aggiornare facilmente le risorse corrispondenti a impostazioni cultura specifiche senza sostituire l'assembly principale dell'applicazione.  
  
 Determinare con attenzione le risorse che costituiranno l'assembly di risorse predefinito dell'applicazione. Poiché tale assembly fa parte dell'assembly principale, le eventuali modifiche apportate richiederanno la sostituzione dell'assembly principale. Se non viene fornita una risorsa predefinita, quando il [processo di recupero di una risorsa](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md) di riserva proverà a cercarla verrà generata un'eccezione. In un'applicazione progettata correttamente, l'utilizzo delle risorse non deve mai generare un'eccezione.  
  
 Per ulteriori informazioni, leggere l'articolo [Creazione del package e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  
  
## <a name="retrieving-resources"></a>Recupero di risorse  
 In fase di esecuzione, le applicazioni caricano le risorse localizzate appropriate per ciascun thread, in base alle impostazioni cultura specificate dalla proprietà <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>. Questo valore della proprietà viene derivato come segue:  
  
-   Assegnando direttamente un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni cultura localizzate alla proprietà <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=fullName>.  
  
-   Se le impostazioni cultura non vengono assegnate in modo esplicito, recuperando il thread predefinito delle impostazioni cultura dell'interfaccia utente dalla proprietà <xref:System.Globalization.CultureInfo.DefaultThreadCurrentUICulture%2A?displayProperty=fullName>.  
  
-   Se le impostazioni cultura dell'interfaccia utente di un thread predefinito non vengono assegnate in modo esplicito, recuperando le impostazioni cultura per l'utente corrente del computer locale chiamando la funzione `GetUserDefaultUILanguage` di Windows.  
  
 Per ulteriori informazioni su come vengono impostate le impostazioni cultura correnti dell'interfaccia utente, vedere le pagine di riferimento <xref:System.Globalization.CultureInfo> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>.  
  
 È quindi possibile recuperare le risorse per le impostazioni cultura correnti dell'interfaccia utente o per impostazioni cultura specifiche utilizzando la classe <xref:System.Resources.ResourceManager?displayProperty=fullName>. Sebbene la classe <xref:System.Resources.ResourceManager> sia maggiormente utilizzata per recuperare le risorse nelle applicazioni desktop, nello spazio dei nomi <xref:System.Resources?displayProperty=fullName> sono contenuti tipi aggiuntivi utilizzabili per recuperare le risorse. Sono inclusi:  
  
-   La classe <xref:System.Resources.ResourceReader>, che consente di enumerare le risorse incorporate in un assembly o archiviate in un file binario autonomo con estensione resources. È utile quando non si conoscono i nomi esatti delle risorse disponibili in fase di esecuzione.  
  
-   La classe <xref:System.Resources.ResXResourceReader> che consente di recuperare le risorse da un file XML (con estensione resx).  
  
-   La classe <xref:System.Resources.ResourceSet> che consente di recuperare le risorse di impostazioni cultura specifiche senza rispettare le regole di fallback. Le risorse possono essere archiviate in un assembly o un file binario autonomo con estensione resources. È inoltre possibile sviluppare un'implementazione <xref:System.Resources.IResourceReader> che consente di utilizzare la classe <xref:System.Resources.ResourceSet> per recuperare le risorse da un'altra origine.  
  
-   La classe <xref:System.Resources.ResXResourceSet> che consente di recuperare tutti gli elementi in un file di risorse XML in memoria.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Globalization.CultureInfo>   
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>   
 [Concetti di base sulle applicazioni](../../../docs/standard/application-essentials.md)   
 [Creazione dei file di risorsa](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)   
 [Creazione del package e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)   
 [Creazione di assembly satellite](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md)   
 [Recupero di risorse](../../../docs/framework/resources/retrieving-resources-in-desktop-apps.md)
