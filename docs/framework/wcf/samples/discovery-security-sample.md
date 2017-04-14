---
title: "Esempio di sicurezza di individuazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8db01f4-b4a1-43fe-8e31-26d4e9304a65
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# Esempio di sicurezza di individuazione
La specifica Discovery non richiede che gli endpoint che partecipano al processo di individuazione siano sicuri.  Il potenziamento dei messaggi di individuazione tramite la sicurezza riduce tuttavia la possibilità di vari tipi di attacchi \(modifica del messaggio, Denial of Service, replay, spoofing\).  In questo esempio vengono implementati canali personalizzati che calcolano e verificano le firme dei messaggi usando il formato di firma compatto \(descritto nella Sezione 8.2 della specifica WS\-Discovery\).  Questo esempio supporta sia la [specifica Discovery 2005](http://go.microsoft.com/fwlink/?LinkId=177912) sia la [versione 1.1 version](http://go.microsoft.com/fwlink/?LinkId=179677).  
  
 Il canale personalizzato viene applicato sullo stack di canali esistente per gli endpoint di individuazione e degli annunci.  In questo modo, per ogni messaggio inviato viene applicata un'intestazione di firma.  La firma viene verificata nei messaggi ricevuti e quando non corrisponde oppure quando i messaggi non presentano una firma, i messaggi vengono eliminati.  Nell'esempio per firmare e verificare i messaggi vengono usati i certificati.  
  
## Discussione  
 WCF è molto estensibile e offre agli utenti la possibilità di personalizzare i canali nel modo desiderato.  Nell'esempio viene implementato un elemento di associazione protetta dell'individuazione che consente la compilazione di canali sicuri.  I canali sicuri verificano le firme dei messaggi e vengono applicati sullo stack corrente.  
  
 L'elemento di associazione protetta compila le channel factory e i listener di canale sicuri.  
  
## Channel factory protetta  
 La channel factory protetta crea output o canali duplex che aggiungono una firma compatta alle intestazioni dei messaggi.  Per contenere il più possibile le dimensioni dei messaggi, viene usato il formato della firma compatto.  La struttura di una firma compatta viene illustrata nell'esempio seguente.  
  
```  
<d:Security ... >   
  [<d:Sig Scheme="xs:anyURI"   
         [KeyId="xs:base64Binary"]?  
          Refs="..."  
         [PrefixList]=”xs:NMTOKENS”   
          Sig="xs:base64Binary"   
          ... />]?  
  ...   
</d:Security>  
  
```  
  
> [!NOTE]
>  Alla versione 2008 del protocollo Discovery è stato aggiunto `PrefixList`.  
  
 Per calcolare la firma, nell'esempio vengono determinati gli elementi della firma espansi.  Viene creata una firma XML \(`SignedInfo`\) usando il prefisso dello spazio dei nomi `ds`, come richiesto dalla specifica WS\-Discovery.  Al corpo e a tutte le intestazioni presenti negli spazi dei nomi di individuazione e indirizzamento viene fatto riferimento nella firma, impedendone pertanto l'alterazione.  Ogni elemento a cui viene fatto riferimento viene trasformato usando la canonizzazione esclusiva \(http:\/\/www.w3.org\/2001\/10\/xml\-exc\-c14n\# \), quindi viene calcolato un valore digest SHA\-1 \(http:\/\/www.w3.org\/2000\/09\/xmldsig\#sha1 \).  In base a tutti gli elementi a cui viene fatto riferimento e ai valori digest corrispondenti, viene calcolato il valore della firma usando l'algoritmo RSA \(http:\/\/www.w3.org\/2000\/09\/xmldsig\#rsa\-sha1 \).  
  
 I messaggi vengono firmati con un certificato specificato dal client.  Il percorso e il nome dell'archivio, nonché il nome del soggetto del certificato devono essere specificati al momento della creazione dell'elemento di associazione.  `KeyId` nella firma compressa rappresenta l'identificatore di chiave del token di firma e corrisponde all'identificatore di chiave del soggetto \(SKI, Subject Key Identifier\) del token di firma oppure \(se l'identificatore SKI non esiste\) a un hash SHA\-1 della chiave pubblica del token di firma.  
  
## Listener del canale protetto  
 Il listener del canale protetto crea l'input o i canali duplex che verificano la firma compatta nei messaggi ricevuti.  Per verificare la firma, l'elemento `KeyId` specificato nella firma compatta allegata al messaggio viene usato per selezionare un certificato nell'archivio specificato.  Se il messaggio non presenta una firma o il controllo della firma ha esito negativo, i messaggi vengono eliminati.  Per usare l'associazione protetta, nell'esempio viene definita una factory che crea gli oggetti <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> e <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint> personalizzati a cui è stato aggiunto l'elemento di individuazione dell'associazione protetta.  Questi endpoint sicuri possono essere usati nei listener degli annunci di individuazione e nei servizi individuabili.  
  
## Dettagli dell'esempio  
 In questo esempio sono incluse un'applicazione di libreria e 4 applicazioni console:  
  
-   **DiscoverySecurityChannels**: libreria che espone l'associazione protetta.  La libreria calcola e verifica la firma compatta per i messaggi in uscita\/in arrivo.  
  
-   **Service**: servizio che espone il contratto ICalculatorService indipendente.  Il servizio è contrassegnato come individuabile.  L'utente specifica i dettagli del certificato usato per firmare i messaggi specificando il percorso e il nome dell'archivio e il nome del soggetto o di un altro identificatore univoco per il certificato, nonché l'archivio in cui si trovano i certificati client \(i certificati usati per il controllo della firma dei messaggi in arrivo\).  In base a questi dettagli, viene compilato e usato un oggetto UdpDiscoveryEndpoint con sicurezza aggiunta.  
  
-   **Client**: questa classe tenta di individuare un oggetto ICalculatorService e di chiamare metodi nel servizio.  Un <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> con sicurezza aggiunta viene di nuovo compilato e usato per firmare e verificare i messaggi.  
  
-   **AnnouncementListener**: servizio indipendente in attesa degli annunci online e offline e che usa l'endpoint degli annunci protetto.  
  
> [!NOTE]
>  Se Setup.bat viene eseguito più volte, il gestore di certificati richiederà di scegliere un certificato da aggiungere, in quanto esistono certificati duplicati.  In tal caso, Setup.bat dovrà essere interrotto e sarà necessario chiamare Cleanup.bat, poiché i duplicati sono già stati creati.  Cleanup.bat richiederà inoltre di scegliere un certificato da eliminare.  Selezionare un certificato nell'elenco e continuare a eseguire Cleanup.bat fino a quando non rimarrà alcun certificato.  
  
#### Per usare questo esempio  
  
1.  Eseguire lo script Setup.bat da un prompt dei comandi di Visual Studio.  Nell'esempio vengono usati certificati per firmare e verificare i messaggi.  Lo script crea i certificati usando Makecert.exe, quindi li installa usando Certmgr.exe.  Lo script deve essere eseguito con i privilegi di amministratore.  
  
2.  Per compilare ed eseguire l'esempio, aprire il file Security.sln in Visual Studio e scegliere **Ricompila tutto**.  Aggiornare le proprietà della soluzione per avviare più progetti: selezionare **Avvia** per tutti i progetti tranne DiscoverySecureChannels.  Eseguire la soluzione in modo normale.  
  
3.  Dopo aver completato l'esempio, eseguire lo script Cleanup.bat per rimuovere i certificati creati per questo esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Scenario\DiscoveryScenario`  
  
## Vedere anche