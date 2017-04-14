---
title: "Distribuzione di un servizio WCF ospitato in Internet Information Services (IIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04ebd329-3fbd-44c3-b3ab-1de3517e27d7
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# Distribuzione di un servizio WCF ospitato in Internet Information Services (IIS)
Lo sviluppo e la distribuzione di un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] ospitato in Internet Information Services \(IIS\) sono costituiti dalle attività seguenti:  
  
-   Verificare che IIS, ASP.NET, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e il componente di attivazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] siano installati e registrati correttamente.  
  
-   Creare una nuova applicazione IIS o riusare un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] esistente.  
  
-   Creare un file con estensione svc per il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Distribuire l'implementazione del servizio nell'applicazione IIS.  
  
-   Configurare il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Per una procedura dettagliata sulla creazione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitato in IIS, vedere [Procedura: ospitare un servizio WCF in IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md).  
  
## Verificare che IIS, ASP.NET e WCF siano installati e registrati correttamente.  
 Affinché i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS funzionino correttamente, è necessario che siano installati [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], IIS e ASP.NET. Le procedure per installare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(come parte di [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)]\), ASP.NET e IIS variano a seconda della versione del sistema operativo utilizzata.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'installazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e di [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)], vedere [Microsoft .NET Framework 4 \(programma di installazione Web\)](http://go.microsoft.com/fwlink/?LinkId=201185). Le istruzioni per l'installazione di IIS sono disponibili nella pagina sull'[installazione di IIS](http://go.microsoft.com/fwlink/?LinkId=201188).  
  
 Il processo di installazione per [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] registra automaticamente [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in IIS, se IIS già è presente sul computer. Se IIS viene installato dopo [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)], è richiesto un passaggio aggiuntivo per registrare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in IIS e [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]. A tal fine, è possibile procedere come segue, a seconda del sistema operativo:  
  
-   [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)], Windows 7 e [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]: usare lo strumento [Strumento di registrazione ServiceModel \(ServiceModelReg.exe\)](../../../../docs/framework/wcf/servicemodelreg-exe.md) per registrare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in IIS. Per usare questo strumento, digitare **ServiceModelReg.exe \/i \/x** al prompt dei comandi di Visual Studio. Per aprire il prompt dei comandi, fare clic sul pulsante Start, selezionare **Tutti i programmi**, **Microsoft Visual Studio 2012**, **Visual Studio Tools**, quindi **Prompt dei comandi di Visual Studio**.  
  
-   [!INCLUDE[wv](../../../../includes/wv-md.md)]: installare il sottocomponente Componenti di attivazione di Windows Communication Foundation di [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)]. A tale scopo, scegliere **Installazione applicazioni** nel Pannello di controllo e quindi **Installazione componenti di Windows**. Verrà avviata l'**Aggiunta guidata componenti di Windows**.  
  
-   Windows 7:  
  
 È necessario infine verificare che ASP.NET sia configurato per utilizzare .NET Framework 4. Per effettuare questa operazione, eseguire lo strumento ASPNET\_Regiis con l'opzione \-i.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Strumento di registrazione di IIS per ASP.NET](http://go.microsoft.com/fwlink/?LinkId=201186)  
  
## Creare una nuova applicazione IIS o riutilizzare un'applicazione ASP.NET esistente  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS devono risiedere all'interno di un'applicazione IIS. È possibile creare una nuova applicazione IIS per ospitare esclusivamente servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. In alternativa, è possibile distribuire un servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in un'applicazione esistente che ospita già contenuto [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)], ad esempio pagine ASPX e servizi Web ASP.NET \(ASMX\).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] queste opzioni, vedere le sezioni "Hosting di WCF affiancato ad ASP.NET" e "Hosting dei servizi WCF in modalità di compatibilità ASP.NET" in [Servizi WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md).  
  
 Si noti che in [!INCLUDE[iis601](../../../../includes/iis601-md.md)] e versioni successive un'applicazione di programmazione isolata e orientata a oggetti viene riavviata periodicamente. Il valore predefinito è 1740 minuti. Il valore massimo supportato è 71.582 minuti. Il riavvio può essere disabilitato.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] questa proprietà, vedere [PeriodicRestartTime](http://go.microsoft.com/fwlink/?LinkId=109968).  
  
## Creare un file con estensione svc per il servizio WCF  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS sono rappresentati come file di dati speciali \(file con estensione svc\) nell'applicazione IIS. Questo modello è simile al modo in cui le pagine ASMX sono rappresentate all'interno di un'applicazione IIS come file con estensione asmx. Un file con estensione svc contiene una direttiva di elaborazione specifica per [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \([@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)\) che consente all'infrastruttura host [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di attivare servizi ospitati in risposta ai messaggi in arrivo. La sintassi più comune per un file con estensione svc viene illustrata nell'istruzione seguente:  
  
```  
<% @ServiceHost Service="MyNamespace.MyServiceImplementationTypeName" %>  
```  
  
 È costituita dalla direttiva [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) e da un solo attributo, `Service`. Il valore dell'attributo `Service` è il nome del tipo Common Language Runtime \(CLR\) dell'implementazione del servizio. L'utilizzo di questa direttiva equivale fondamentalmente alla creazione di un host del servizio tramite il seguente codice:  
  
```  
new ServiceHost( typeof( MyNamespace.MyServiceImplementationTypeName ) );  
```  
  
 È inoltre possibile una configurazione di hosting aggiuntiva, ad esempio la creazione di un elenco di indirizzi di base per il servizio. È anche possibile utilizzare un <xref:System.ServiceModel.Activation.ServiceHostFactory> personalizzato per estendere la direttiva per l'utilizzo con soluzioni di hosting personalizzate. Le applicazioni IIS che ospitano servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non sono responsabili della gestione della creazione e della durata delle istanze <xref:System.ServiceModel.ServiceHost>. L'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] gestita crea dinamicamente l'istanza <xref:System.ServiceModel.ServiceHost> necessaria quando viene ricevuta la prima richiesta per il file con estensione svc. L'istanza non viene rilasciata finché non viene chiusa in modo esplicito dal codice o finché l'applicazione non viene riciclata.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla sintassi per i file con estensione svc, vedere [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md).  
  
## Distribuire l'implementazione del servizio all'applicazione IIS  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS utilizzano lo stesso modello di compilazione dinamica di [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)]. Come per [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], è possibile distribuire il codice di implementazione per i servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS in vari modi e in varie posizioni, come segue:  
  
-   Come file dll precompilato nella Global Assembly Cache \(GAC\) o nella directory \\bin dell'applicazione. I file binari precompilati non vengono aggiornati finché non viene distribuita una nuova versione della libreria di classi.  
  
-   Come file di origine non compilati situati nella directory \\App\_Code dell'applicazione. I file di origine situati in questa directory vengono richiesti dinamicamente durante l'elaborazione della prima richiesta dell'applicazione. Qualsiasi modifica ai file nella directory \\App\_Code provoca il riciclo e la ricompilazione dell'intera applicazione quando viene ricevuta la richiesta successiva.  
  
-   Come codice non compilato posizionato direttamente nel file con estensione svc. Il codice di implementazione può anche trovarsi in linea nel file con estensione svc del servizio, dopo la direttiva @ServiceHost. Qualsiasi modifica al codice inline provoca il riciclo e la ricompilazione dell'applicazione quando viene ricevuta la richiesta successiva.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]l modello di compilazione [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)], vedere [Cenni preliminari sulla compilazione in ASP.NET](http://go.microsoft.com/fwlink/?LinkId=94773).  
  
## Configurare il servizio WCF  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS memorizzano la propria configurazione nel file Web.config delle applicazioni. I servizi ospitati in IIS utilizzano gli stessi elementi di configurazione e la stessa sintassi dei servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati al di fuori di IIS. I vincoli seguenti sono tuttavia specifici per l'ambiente host IIS:  
  
-   Indirizzi di base per i servizi ospitati in IIS.  
  
-   Le applicazioni che ospitano servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] al di fuori di IIS possono controllarne l'indirizzo di base passando un set di URI dell'indirizzo di base al costruttore <xref:System.ServiceModel.ServiceHost> o fornendo un elemento [\<host\>](../../../../docs/framework/configure-apps/file-schema/wcf/host.md) nella configurazione del servizio. I servizi ospitati in IIS non sono in grado di controllare i propri indirizzi di base che corrispondono agli indirizzi dei rispettivi file con estensione svc.  
  
### Indirizzi endpoint per i servizi ospitati in IIS  
 Quando sono ospitati in IIS, gli indirizzi endpoint sono sempre considerati relativi all'indirizzo del file con estensione svc che rappresenta il servizio. Se, ad esempio, l'indirizzo di base di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è http:\/\/localhost\/Application1\/MyService.svc con la configurazione dell'endpoint seguente.  
  
```  
<endpoint address="anotherEndpoint" .../>  
```  
  
 Tale configurazione fornisce un endpoint che può essere raggiunto all'indirizzo "http:\/\/localhost\/Application1\/MyService.svc\/anotherEndpoint".  
  
 In modo analogo, l'elemento di configurazione dell'endpoint che utilizza una stringa vuota come indirizzo relativo fornisce un endpoint raggiungibile all'indirizzo http:\/\/localhost\/Application1\/MyService.svc, che è l'indirizzo di base.  
  
```  
<endpoint address="" ... />  
```  
  
 Per gli endpoint del servizio ospitati in IIS è necessario utilizzare sempre indirizzi endpoint relativi. La specifica di un indirizzo endpoint completo \(ad esempio, http:\/\/localhost\/MyService.svc\) può comportare errori nella distribuzione del servizio se l'indirizzo endpoint non punta all'applicazione IIS che ospita il servizio che espone l'endpoint. L'utilizzo di indirizzi endpoint relativi per i servizi di hosting evita potenziali conflitti.  
  
### Trasporti disponibili  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS 5.1 e [!INCLUDE[iis601](../../../../includes/iis601-md.md)] sono limitati all'utilizzo di comunicazioni basate su HTTP. Su queste piattaforme IIS, la configurazione di un servizio ospitato affinché utilizzi un'associazione non HTTP, comporta un errore durante l'attivazione del servizio. Per [!INCLUDE[iisver](../../../../includes/iisver-md.md)], i trasporti supportati includono HTTP, Net.TCP, Net.Pipe, Net.MSMQ e msmq.formatname per la compatibilità delle versioni precedenti con le applicazioni MSMQ esistenti.  
  
### Protezione del trasporto HTTP  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitati in IIS possono avvalersi della sicurezza del trasporto HTTP \(ad esempio schemi di autenticazione HTTPS e HTTP quali Basic, Digest e l'autenticazione integrata di Windows\), a condizione che la directory virtuale IIS contenente il servizio supporti tali impostazioni. Le impostazioni di sicurezza del trasporto HTTP sull'associazione di un endpoint di hosting devono corrispondere alle impostazioni di sicurezza del trasporto sulla directory virtuale IIS che lo contiene.  
  
 Un endpoint [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] configurato, ad esempio, per utilizzare l'autenticazione digest HTTP deve risiedere in una directory virtuale IIS configurata anch'essa per consentire la medesima autenticazione. Combinazioni non corrispondenti di impostazioni IIS e impostazioni dell'endpoint [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] provocano un errore durante l'attivazione del servizio.  
  
## Vedere anche  
 [Host in Internet Information Services](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)   
 [Procedure consigliate per l'hosting in Internet Information Services \(IIS\)](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)   
 [Funzionalità di hosting di Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=201276)