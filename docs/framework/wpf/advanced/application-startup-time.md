---
title: "Tempo di avvio delle applicazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "avvio dell'applicazione [WPF]"
  - "prestazioni [WPF], ora di avvio"
  - "schermata iniziale [WPF], ora di avvio"
  - "ora di avvio [WPF]"
  - "WPF, ora di avvio"
ms.assetid: f0ec58d8-626f-4d8a-9873-c20f95e08b96
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Tempo di avvio delle applicazioni
Il tempo necessario per l'avvio di un'applicazione WPF può variare molto.  In questo argomento vengono descritte le varie tecniche che consentono di ridurre il tempo di avvio percepito ed effettivo per un'applicazione WPF \(Windows Presentation Foundation\).  
  
## Informazioni sull'avvio a freddo e l'avvio a caldo  
 L'avvio a freddo avviene quando l'applicazione viene avviata per la prima volta dopo un riavvio del sistema o quando la si avvia, la si chiude e la si avvia di nuovo dopo molto tempo.  All'avvio di un'applicazione, se le pagine necessarie \(codice, dati statici, Registro di sistema e così via\) non sono presenti nell'elenco di standby del gestore della memoria di Windows, si verificano errori di pagina.  Per portare le pagine in memoria è necessario l'accesso al disco.  
  
 L'avvio a caldo si verifica quando la maggior parte delle pagine relative ai componenti CLR \(Common Language Runtime\) principali è già caricata in memoria, quindi il tempo di accesso al disco è minimo.  Si spiega in questo modo perché un'applicazione gestita venga avviata più velocemente quando viene eseguita per la seconda volta.  
  
## Implementare una schermata iniziale  
 Nei casi di ritardo significativo e inevitabile tra l'avvio dell'applicazione e la visualizzazione della prima interfaccia utente, è possibile ottimizzare il tempo di avvio percepito utilizzando una *schermata iniziale*.  In questo modo viene visualizzata un'immagine quasi immediatamente dopo l'avvio dell'applicazione da parte dell'utente.  Quando l'applicazione è pronta per la visualizzazione della prima interfaccia utente, viene applicata la dissolvenza alla schermata iniziale.  A partire da [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)] è possibile utilizzare la classe <xref:System.Windows.SplashScreen> per implementare una schermata iniziale.  Per ulteriori informazioni, vedere [Aggiunta di una schermata iniziale in un'applicazione WPF](../../../../docs/framework/wpf/app-development/how-to-add-a-splash-screen-to-a-wpf-application.md).  
  
 È inoltre possibile implementare la schermata iniziale preferita tramite grafica Win32 nativa.  Visualizzare l'implementazione prima che venga chiamato il metodo <xref:System.Windows.Application.Run%2A>.  
  
## Analizzare il codice di avvio  
 Individuare la motivazione della lentezza dell'avvio a freddo.  L'I\/O del disco potrebbe essere una causa, ma non sempre.  In genere è consigliabile ridurre al minimo il ricorso a risorse esterne, ad esempio rete, servizi Web o disco.  
  
 Prima di testare, verificare che nessuna applicazione o nessun servizio in esecuzione utilizzi codice gestito o codice WPF.  
  
 Avviare l'applicazione WPF immediatamente dopo un riavvio e calcolare il tempo necessario per la visualizzazione.  Se tutti gli avvii successivi dell'applicazione \(avvio a caldo\) sono molto più veloci, è possibile che il problema dell'avvio a freddo sia imputabile all'I\/O.  
  
 Se il problema dell'avvio a freddo dell'applicazione non è correlato all'I\/O, è probabile che all'avvio dell'applicazione l'inizializzazione o i calcoli richiedano molto tempo, che si attenda il completamento di un evento o che siano necessarie molte operazioni di compilazione JIT.  Nelle sezioni seguenti vengono illustrate in maggiore dettaglio alcune di queste situazioni.  
  
## Ottimizzare il caricamento dei moduli  
 Per stabilire i moduli caricati nell'applicazione, utilizzare strumenti quali Process Explorer \(Procexp.exe\) e Tlist.exe.  Il comando `Tlist <pid>` mostra tutti i moduli caricati da un processo.  
  
 Se ad esempio non ci si connette al Web ma si vede che System.Web.dll è caricato, esiste un modulo nell'applicazione che fa riferimento a questo assembly.  Verificare se il riferimento sia effettivamente necessario.  
  
 Se nell'applicazione sono presenti più moduli, unirli in un unico modulo.  Questo approccio richiede meno sovraccarico da caricamento di assembly CLR.  Un minor numero di assembly significa inoltre minori requisiti di gestione dello stato per CLR.  
  
## Rinviare le operazioni di inizializzazione  
 Prendere in considerazione la possibilità eseguire il codice di inizializzazione dopo il rendering della finestra dell'applicazione principale.  
  
 Tenere presente che l'inizializzazione può essere eseguita all'interno di un costruttore di classi e se il codice di inizializzazione fa riferimento ad altre classi può provocare un effetto a cascata in base al quale molti costruttori di classi vengono eseguiti.  
  
## Evitare la configurazione dell'applicazione  
 Prendere in considerazione la possibilità di evitare la configurazione dell'applicazione.  Se ad esempio un'applicazione necessita di requisiti di configurazione semplici e di tempi di avvio prestabiliti, le voci del Registro di sistema o un semplice file INI possono costituire un'alternativa di avvio più veloce.  
  
## Utilizzare GAC  
 Se un assembly non è installato nella Global Assembly Cache \(GAC\), i ritardi sono provocati dalla verifica hash di assembly con nome sicuro e dalla convalida dell'immagine Ngen se un'immagine nativa per tale assembly è disponibile nel computer.  La verifica del nome sicuro viene ignorata per tutti gli assembly installati nella GAC.  Per ulteriori informazioni, vedere [Gacutil.exe \(strumento Global Assembly Cache\)](../../../../docs/framework/tools/gacutil-exe-gac-tool.md).  
  
## Utilizzare Ngen.exe  
 Prendere in considerazione l'utilizzo del generatore di immagini native \(Ngen.exe\) nell'applicazione.  L'utilizzo di Ngen.exe significa trovare un compromesso tra utilizzo della CPU e maggiore accesso al disco perché l'immagine nativa generata da Ngen.exe occupa probabilmente uno spazio maggiore dell'immagine MSIL.  
  
 Per migliorare il tempo di avvio a caldo, è consigliabile utilizzare sempre Ngen.exe nell'applicazione in quanto ciò evita l'utilizzo della CPU per la compilazione JIT del codice dell'applicazione.  
  
 In alcuni scenari di avvio a freddo l'utilizzo di Ngen.exe può rivelarsi utile  perché non è necessario che il compilatore JIT \(mscorjit.dll\) venga caricato.  
  
 La compresenza di moduli Ngen e JIT può sortire un effetto peggiore  perché mscorjit.dll deve essere caricato e quando il compilatore JIT opera sul codice si rende necessario l'accesso a molte pagine nelle immagini Ngen quando il compilatore JIT legge i metadati degli assembly.  
  
### Ngen e ClickOnce  
 Anche il modo in cui si intende distribuire l'applicazione può incidere sui tempi di caricamento.  La distribuzione dell'applicazione [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] non supporta Ngen.  Se si decide di utilizzare Ngen.exe per l'applicazione, sarà necessario utilizzare un altro meccanismo di distribuzione, ad esempio Windows Installer.  
  
 Per ulteriori informazioni, vedere [Ngen.exe \(generatore di immagini native\)](../../../../docs/framework/tools/ngen-exe-native-image-generator.md).  
  
### Riassegnazione e conflitti di indirizzi di DLL  
 Se si utilizza Ngen.exe, tenere presente che la riassegnazione può verificarsi quando le immagini native vengono caricate in memoria.  Se una DLL non viene caricata all'indirizzo di base preferito perché la serie di indirizzi è già allocata, il caricatore di Windows la caricherà a un altro indirizzo e questa operazione può richiedere molto tempo.  
  
 È possibile utilizzare lo strumento Virtual Address Dump \(Vadump.exe\) per verificare l'esistenza di moduli in cui tutte le pagine sono private.  In tal caso è possibile che il modulo sia stato riassegnato a un indirizzo diverso  e le relative pagine non possono essere condivise.  
  
 Per ulteriori informazioni su come impostare l'indirizzo di base, vedere [Ngen.exe \(generatore di immagini native\)](../../../../docs/framework/tools/ngen-exe-native-image-generator.md).  
  
## Ottimizzare Authenticode  
 La verifica Authenticode va ad aggiungersi al tempo necessario per l'avvio.  Gli assembly con firma Authenticode devono essere verificati con l'autorità di certificazione.  Questa verifica può richiedere tempo perché possono essere necessarie più connessioni alla rete per scaricare gli elenchi di revoche di certificati correnti.  La verifica accerta inoltre la presenza di una catena completa di certificati validi sul percorso a una radice disponibile nell'elenco locale.  Ciò può equivalere a vari secondi di ritardo mentre l'assembly viene caricato.  
  
 Prendere in considerazione la possibilità di installare il certificato CA nel computer client o di evitare l'utilizzo di Authenticode quando possibile.  Se è certo che l'evidenza dell'autore non è indispensabile per l'applicazione, la verifica della firma non è necessaria.  
  
 A partire da [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] è disponibile un'opzione di configurazione che consente di ignorare la verifica Authenticode.  A tale scopo aggiungere al file app.exe.config l'impostazione seguente:  
  
```  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>   
    </runtime>  
</configuration>  
```  
  
 Per ulteriori informazioni, vedere [Elemento \<generatePublisherEvidence\>](../../../../docs/framework/configure-apps/file-schema/runtime/generatepublisherevidence-element.md).  
  
## Confrontare le prestazioni in Windows Vista  
 In Windows Vista il gestore della memoria dispone di una tecnologia denominata SuperFetch.  SuperFetch analizza modelli di utilizzo della memoria nel corso del tempo per determinare il contenuto di memoria ottimale per un utente specifico.  Funziona di continuo per gestire sempre il contenuto.  
  
 Si tratta di un approccio diverso dalla tecnica di prelettura utilizzata in Windows XP, in base alla quale i dati vengono precaricati in memoria senza analisi dei modelli di utilizzo.  Con il passare del tempo se l'utente utilizza spesso l'applicazione WPF in Windows Vista è possibile che il tempo di avvio a freddo dell'applicazione migliori.  
  
## Utilizzare i domini applicazioni in modo efficiente  
 Se possibile, caricare gli assembly in un'area del codice indipendente dal dominio per avere la certezza che l'immagine nativa, se presente, venga utilizzata in tutti i domini applicazioni creati nell'applicazione.  
  
 Per ottenere prestazioni migliori, applicare comunicazioni efficienti tra domini riducendo le chiamate tra domini.  Se possibile utilizzare chiamate senza argomenti o con gli argomenti di tipo primitivo.  
  
## Utilizzare l'attributo NeutralResourcesLanguage  
 Utilizzare l'attributo <xref:System.Resources.NeutralResourcesLanguageAttribute> per specificare impostazioni cultura non associate ad alcun paese per <xref:System.Resources.ResourceManager>.  In questo modo si evitano ricerche infruttuose negli assembly.  
  
## Utilizzare la classe BinaryFormatter per la serializzazione  
 Se è necessario utilizzare la serializzazione, servirsi della classe <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> anziché della classe <xref:System.Xml.Serialization.XmlSerializer>.  La classe <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> è implementata nella libreria di classi base \(BCL, Base Class Library\) nell'assembly mscorlib.dll.  <xref:System.Xml.Serialization.XmlSerializer> viene implementato nell'assembly System.Xml.dll, che potrebbe essere una DLL aggiuntiva da caricare.  
  
 Se è necessario utilizzare la classe <xref:System.Xml.Serialization.XmlSerializer>, si possono ottenere prestazioni migliori se si esegue una pregenerazione dell'assembly di serializzazione.  
  
## Configurare ClickOnce per verificare gli aggiornamenti dopo l'avvio  
 Se nell'applicazione viene utilizzato [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)], evitare l'accesso alla rete all'avvio configurando [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] in modo che la ricerca degli aggiornamenti nel sito di distribuzione avvenga dopo l'avvio dell'applicazione.  
  
 Se si utilizza il modello di applicazione XBAP \(XAML Browser Application\), ricordare che in [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] il controllo del sito di distribuzione alla ricerca di aggiornamenti avviene anche se XBAP è già nella cache di [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)].  Per ulteriori informazioni, vedere [Sicurezza e distribuzione di ClickOnce](../Topic/ClickOnce%20Security%20and%20Deployment.md).  
  
## Configurare l'avvio automatico del servizio PresentationFontCache  
 La prima applicazione WPF a essere eseguita dopo un riavvio è il servizio PresentationFontCache.  Questo servizio consente di memorizzare nella cache i tipi di caratteri del sistema, di migliorare l'accesso ai tipi di carattere e le prestazioni complessive.  L'avvio del servizio comporta un sovraccarico e, in alcuni ambienti controllati, è consigliabile considerare la possibilità di configurare il servizio in modo che venga avviato automaticamente al riavvio del sistema.  
  
## Impostare l'associazione dati a livello di codice  
 Anziché utilizzare XAML per impostare <xref:System.Windows.FrameworkElement.DataContext%2A> in modo dichiarativo per la finestra principale, impostarlo a livello di codice nel metodo <xref:System.Windows.Application.OnActivated%2A>.  
  
## Vedere anche  
 <xref:System.Windows.SplashScreen>   
 <xref:System.AppDomain>   
 <xref:System.Resources.NeutralResourcesLanguageAttribute>   
 <xref:System.Resources.ResourceManager>   
 [Aggiunta di una schermata iniziale in un'applicazione WPF](../../../../docs/framework/wpf/app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)   
 [Ngen.exe \(generatore di immagini native\)](../../../../docs/framework/tools/ngen-exe-native-image-generator.md)   
 [Elemento \<generatePublisherEvidence\>](../../../../docs/framework/configure-apps/file-schema/runtime/generatepublisherevidence-element.md)