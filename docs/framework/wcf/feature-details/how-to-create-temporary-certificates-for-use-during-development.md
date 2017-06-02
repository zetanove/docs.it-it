---
title: "Procedura: creare certificati temporanei da usare durante lo sviluppo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "certificati [WCF], creazione di certificati temporanei"
  - "certificati temporanei [WCF]"
ms.assetid: bc5f6637-5513-4d27-99bb-51aad7741e4a
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: creare certificati temporanei da usare durante lo sviluppo
Quando si sviluppa un servizio o un client protetto usando [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], è spesso necessario fornire un certificato X.509 da usare come credenziale. Il certificato in genere fa parte di una catena di certificati con autorità radice contenuta nell'archivio Autorità di certificazione radice attendibile del computer. La catena di certificati consente di definire l'ambito per un set di certificati quando in genere l'autorità radice è dell'organizzazione o dell'unità aziendale. Per emulare questo comportamento in fase di sviluppo, è possibile creare due certificati per soddisfare i requisiti di sicurezza. Il primo è un certificato autofirmato che si trova nell'archivio Autorità di certificazione radice attendibile, mentre il secondo certificato viene creato dal primo e si trova nell'archivio Personale del computer locale o dell'utente corrente. Questo argomento descrive i passaggi per la creazione di questi due certificati mediante lo [strumento di creazione certificati \(MakeCert.exe\)](http://go.microsoft.com/fwlink/?LinkId=248185), fornito da [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] SDK.  
  
> [!IMPORTANT]
>  I certificati generati dallo strumento di creazione certificati sono forniti solo a scopo di test. Quando si distribuisce un servizio o un client, assicurarsi di usare un certificato appropriato rilasciato da un'autorità di certificazione. Tale certificato può essere fornito da un server dei certificati di [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] dell'organizzazione o da terze parti.  
>   
>  Per impostazione predefinita, lo [Makecert.exe \(Certificate Creation Tool\)](../Topic/Makecert.exe%20\(Certificate%20Creation%20Tool\).md) crea certificati la cui autorità radice è denominata "Agenzia radice"**.** Poiché l'Agenzia radice non è inclusa nell'archivio Autorità di certificazione radice attendibili, i certificati non sono protetti. La creazione di un certificato autofirmato posizionato nell'archivio di Autorità di certificazione radice attendibili consente di creare un ambiente di sviluppo che simula in modo più accurato l'ambiente di distribuzione.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla creazione e sull'uso di certificati, vedere [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'uso di un certificato come credenziale, vedere [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md). Per un'esercitazione sull'uso della tecnologia Microsoft Authenticode, vedere [Panoramica di Authenticode ed esercitazioni](http://go.microsoft.com/fwlink/?LinkId=88919).  
  
### Per creare un certificato dell'autorità radice autofirmato ed esportare la chiave privata  
  
1.  Usare lo strumento MakeCert.exe con le opzioni seguenti:  
  
    1.  `-n` `subjectName`. Specifica il nome del soggetto. La convenzione prevede l'inserimento del prefisso "CN \= " per "Nome comune" prima del nome del soggetto.  
  
    2.  `-r`. Specifica che il certificato sarà autofirmato.  
  
    3.  `-sv` `privateKeyFile`. Specifica il file che contiene il contenitore della chiave privata.  
  
     Ad esempio, nel comando seguente viene creato un certificato autofirmato con il nome del soggetto "CN\=TempCA".  
  
    ```  
    makecert -n "CN=TempCA" -r -sv TempCA.pvk TempCA.cer  
    ```  
  
     Verrà richiesto di fornire una password per proteggere la chiave privata. Questa password è richiesta quando si crea un certificato firmato mediante questo certificato radice.  
  
### Per creare un nuovo certificato firmato mediante un certificato dell'autorità radice  
  
1.  Usare lo strumento MakeCert.exe con le opzioni seguenti:  
  
    1.  `-sk` `subjectKey`. La posizione del contenitore di chiavi del soggetto che contiene la chiave privata. Se non esiste alcun contenitore di chiavi, ne viene creato uno. Per impostazione predefinita, se le opzioni \-sk o \-sv non vengono usate, viene creato un contenitore di chiavi denominato JoeSoft.  
  
    2.  `-n` `subjectName`. Specifica il nome del soggetto. La convenzione prevede l'inserimento del prefisso "CN \= " per "Nome comune" prima del nome del soggetto.  
  
    3.  `-iv` `issuerKeyFile`. Specifica il file della chiave privata dell'autorità emittente.  
  
    4.  `-ic` `issuerCertFile`. Specifica la posizione del certificato dell'autorità emittente.  
  
     Ad esempio, nel comando seguente viene creato un certificato firmato mediante il certificato dell'autorità radice `TempCA` con il nome del soggetto `"CN=SignedByCA"` usando la chiave privata dell'autorità emittente.  
  
    ```  
    makecert -sk SignedByCA -iv TempCA.pvk -n "CN=SignedByCA" -ic TempCA.cer SignedByCA.cer -sr currentuser -ss My  
    ```  
  
## Installazione di un certificato nell'archivio dell'Autorità di certificazione radice attendibili  
 Se è stato creato un certificato autofirmato, è possibile installarlo nell'archivio Autorità di certificazione radice attendibili. Qualsiasi certificato firmato con il certificato in questa fase viene considerato attendibile dal computer. Per questo motivo, eliminare il certificato dall'archivio quando non è più necessario. Quando si elimina questo certificato dell'autorità radice, tutti gli altri certificati che sono stati firmati mediante tale certificato diventano non autorizzati. I certificati dell'autorità radice sono semplicemente un meccanismo che consente di definire come necessario un gruppo di certificati. Ad esempio, nelle applicazioni peer\-to\-peer in genere non è necessaria un'autorità radice perché l'identità di un individuo viene ritenuta attendibile semplicemente sulla base del certificato fornito.  
  
#### Per installare un certificato autofirmato nell'Autorità di certificazione radice attendibili  
  
1.  Aprire lo snap\-in del certificato.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Procedura: visualizzare certificati con lo snap\-in MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).  
  
2.  Aprire la cartella in cui archiviare il certificato, **Computer locale** o **Utente corrente**.  
  
3.  Aprire la cartella **Autorità di certificazione radice attendibili**.  
  
4.  Fare clic con il pulsante destro del mouse sulla cartella **Certificati**, scegliere **Tutte le attività**, quindi fare clic su **Importa**.  
  
5.  Seguire le istruzioni della procedura guidata per importare TempCa.cer nell'archivio.  
  
## Uso dei certificati con WCF  
 Dopo avere impostato i certificati temporanei, è possibile usarli per sviluppare soluzioni WCF che specifichino i certificati come tipo di credenziali client. Nella configurazione XML seguente, ad esempio, vengono specificati la sicurezza dei messaggi e un certificato come tipo di credenziali client.  
  
#### Per specificare un certificato come tipo di credenziali client  
  
-   Nel file di configurazione di un servizio usare l'XML seguente per impostare la modalità di sicurezza su messaggio e il tipo di credenziali client su certificato.  
  
    ```xml  
    <bindings>       
      <wsHttpBinding>  
        <binding name="CertificateForClient">  
          <security>  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  
    ```  
  
 Nel file di configurazione di un client usare l'XML seguente per specificare che il certificato è disponibile nell'archivio dell'utente e può essere trovato cercando il valore "CohoWinery" nel campo SubjectName.  
  
```xml  
  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="CertForClient">  
      <clientCredentials>  
        <clientCertificate findValue="CohoWinery" x509FindType="FindBySubjectName" />  
       </clientCredentials>  
     </behavior>  
   </endpointBehaviors>  
</behaviors>  
```  
  
 Per altre informazioni sull'uso di certificati in WCF, vedere [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
## Sicurezza di .NET Framework  
 Assicurarsi di eliminare qualsiasi certificato temporaneo dell'autorità di radice dalle cartelle **Autorità di certificazione radice attendibili** e **Personale** facendo clic con il pulsante destro del mouse sul certificato e scegliendo **Elimina**.  
  
## Vedere anche  
 [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Procedura: visualizzare certificati con lo snap\-in MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md)   
 [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)