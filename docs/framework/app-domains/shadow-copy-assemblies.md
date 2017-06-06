---
title: Creazione di copie shadow di assembly | Microsoft Docs
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
- assemblies [.NET Framework], shadow copying
- application domains, shadow copying assemblies
- shadow copying assemblies
ms.assetid: de8b8759-fca7-4260-896b-5a4973157672
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: e451c7f15026b06db98d1922e06183a06e42d982
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="shadow-copying-assemblies"></a>Creazione di copie replicate di assembly
La creazione di copie shadow consente di aggiornare gli assembly usati in un dominio applicazione senza scaricare quest'ultimo. Ciò è particolarmente utile per le applicazioni che devono essere disponibili in modo continuo, ad esempio siti ASP.NET.  
  
> [!IMPORTANT]
>  La copia shadow non è supportata nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].  
  
 Common Language Runtime blocca un file di assembly quando l'assembly è caricato, in modo che non sia possibile aggiornare il file finché l'assembly non sarà stato scaricato. L'unico modo per scaricare un assembly da un dominio applicazione consiste nello scaricare il dominio applicazione; pertanto, in circostanze normali, non è possibile aggiornare un assembly su disco fino a quando tutti i domini applicazione che lo usano non saranno stati scaricati.  
  
 Quando un dominio applicazione è configurato per la copia shadow di file, gli assembly dal percorso dell'applicazione vengono copiati in un'altra posizione e caricati da tale posizione. La copia è bloccata, ma il file di assembly originale è sbloccato e può essere aggiornato.  
  
> [!IMPORTANT]
>  Gli unici assembly che possono essere replicati mediante copia shadow sono quelli memorizzati nella directory dell'applicazione o nelle relative sottodirectory, specificato dalle proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> e <xref:System.AppDomainSetup.PrivateBinPath%2A> quando viene configurato il dominio applicazione. Gli assembly memorizzati nella Global Assembly Cache non vengono replicati mediante copia shadow.  
  
 In questo articolo sono contenute le sezioni seguenti:  
  
-   [Abilitazione e uso della creazione di copie shadow](#EnablingAndUsing): illustra l'uso di base e le opzioni disponibili per la copia shadow.  
  
-   [Prestazioni di avvio](#StartupPerformance): illustra le modifiche che vengono apportate alla copia shadow in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] per migliorare le prestazioni di avvio e come ripristinare il funzionamento delle versioni precedenti.  
  
-   [Metodi obsoleti](#ObsoleteMethods): illustra le modifiche apportate ai metodi e alle proprietà che controllano la creazione di copie shadow in [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)].  
  
<a name="EnablingAndUsing"></a>   
## <a name="enabling-and-using-shadow-copying"></a>Abilitazione e uso della creazione di copie shadow  
 È possibile usare le proprietà della classe <xref:System.AppDomainSetup> come indicato di seguito per configurare un dominio applicazione per la creazione di copie shadow:  
  
-   Abilitare la creazione di copie shadow impostando la proprietà <xref:System.AppDomainSetup.ShadowCopyFiles%2A> sul valore della stringa `"true"`.  
  
     Per impostazione predefinita, tutti gli assembly nel percorso dell'applicazione verranno copiati in una Download Cache prima che vengano caricati. Si tratta della stessa cache gestita da Common Language Runtime per archiviare i file scaricati da altri computer ed eliminare automaticamente i file quando non sono più necessari.  
  
-   Facoltativamente, impostare un percorso personalizzato per i file di copia shadow usando la proprietà <xref:System.AppDomainSetup.CachePath%2A> e la proprietà <xref:System.AppDomainSetup.ApplicationName%2A>.  
  
     Il percorso di base della posizione è costituito dalla concatenazione della proprietà <xref:System.AppDomainSetup.ApplicationName%2A> alla proprietà <xref:System.AppDomainSetup.CachePath%2A> come sottodirectory. Gli assembly vengono replicati nelle sottodirectory di questo percorso, non nel percorso di base.  
  
    > [!NOTE]
    >  Se la proprietà <xref:System.AppDomainSetup.ApplicationName%2A> non è impostata, la proprietà <xref:System.AppDomainSetup.CachePath%2A> viene ignorata e viene usata la Download Cache. Non viene generata alcuna eccezione.  
  
     Se si specifica un percorso personalizzato, si è responsabili della pulizia delle directory e dei file copiati quando non sono più necessari, perché non vengono eliminati automaticamente.  
  
     Esistono diversi motivi per cui è consigliabile impostare un percorso personalizzato per i file della copia shadow, ad esempio se l'applicazione genera un numero elevato di copie. La Download Cache è limitata dalle dimensioni, non dalla durata, pertanto è possibile che Common Language Runtime proverà a eliminare un file che è ancora in uso. Un altro motivo per impostare un percorso personalizzato è quando gli utenti che eseguono l'applicazione non hanno accesso in scrittura al percorso di directory che Common Language Runtime usa per la Download Cache.  
  
-   Facoltativamente, limitare gli assembly che vengono replicati usando la proprietà <xref:System.AppDomainSetup.ShadowCopyDirectories%2A>.  
  
     Quando si abilita la creazione di copie shadow per un dominio applicazione, l'impostazione predefinita consiste nel copiare tutti gli assembly nel percorso dell'applicazione, ovvero nelle directory specificate dalle proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> e <xref:System.AppDomainSetup.PrivateBinPath%2A>. È possibile limitare la copia alle directory selezionate creando una stringa che contiene solo le directory per cui si vogliono creare copie shadow e assegnando la stringa alla proprietà <xref:System.AppDomainSetup.ShadowCopyDirectories%2A>. Separare le directory con punti e virgola. Gli unici assembly che vengono replicati sono quelli nelle directory selezionate.  
  
    > [!NOTE]
    >  Se non si assegna una stringa alla proprietà <xref:System.AppDomainSetup.ShadowCopyDirectories%2A>  o se si imposta questa proprietà su `null`, tutti gli assembly nelle directory specificate dalle proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> e <xref:System.AppDomainSetup.PrivateBinPath%2A> vengono replicati come copie shadow.  
  
    > [!IMPORTANT]
    >  I percorsi delle directory non devono contenere punti e virgola, perché il punto e virgola è il carattere delimitatore. Non esiste alcun carattere di escape per i punti e virgola.  
  
<a name="StartupPerformance"></a>   
## <a name="startup-performance"></a>Prestazioni di avvio  
 All'avvio di un dominio applicazione che usa la creazione di copie shadow, si verifica un ritardo mentre gli assembly nella directory dell'applicazione vengono copiati nella directory di copia shadow o verificati, se si trovano già in tale posizione. Prima di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], tutti gli assembly sono stati copiati in una directory temporanea. Ogni assembly è stato aperto per verificare il nome dell'assembly e il nome sicuro è stato convalidato. Ogni assembly è stato controllato per verificare se è stato aggiornato più di recente rispetto alla copia nella directory della copia shadow. In tal caso, è stato copiato nella directory della copia shadow. Infine, le copie temporanee vengono rimosse.  
  
 A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], il comportamento di avvio predefinito consiste nel confrontare direttamente la data e l' ora del file di ciascun assembly nella directory dell'applicazione con la data e l'ora della copia nella directory della copia shadow. Se l'assembly è stato aggiornato, viene copiato usando la stessa procedura adottata nelle versioni precedenti di .NET Framework. In caso contrario, viene caricata la copia nella directory della copia shadow.  
  
 Il miglioramento delle prestazioni risultante è maggiore per le applicazioni in cui gli assembly non vengono modificati di frequente e le modifiche vengono apportate in genere in un piccolo subset di assembly. Se la maggior parte degli assembly in un'applicazione viene modificata frequentemente, il nuovo comportamento predefinito potrebbe causare una regressione delle prestazioni. È possibile ripristinare il comportamento di avvio delle versioni precedenti di .NET Framework aggiungendo l'[\<elemento shadowCopyVerifyByTimestamp>](../../../docs/framework/configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md) al file di configurazione con `enabled="false"`.  
  
<a name="ObsoleteMethods"></a>   
## <a name="obsolete-methods"></a>Metodi obsoleti  
 La classe <xref:System.AppDomain> include diversi metodi, ad esempio <xref:System.AppDomain.SetShadowCopyFiles%2A> e <xref:System.AppDomain.ClearShadowCopyPath%2A>, che possono essere usati per controllare la creazione di copie shadow in un dominio applicazione, ma che sono stati contrassegnati come obsoleti in .NET Framework versione 2.0. Il modo consigliato per configurare un dominio applicazione per la creazione di copie shadow consiste nell'usare le proprietà della classe <xref:System.AppDomainSetup>.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.AppDomainSetup.ShadowCopyFiles%2A?displayProperty=fullName>   
 <xref:System.AppDomainSetup.CachePath%2A?displayProperty=fullName>   
 <xref:System.AppDomainSetup.ApplicationName%2A?displayProperty=fullName>   
 <xref:System.AppDomainSetup.ShadowCopyDirectories%2A?displayProperty=fullName>   
 [\<Elemento shadowCopyVerifyByTimestamp>](../../../docs/framework/configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md)
