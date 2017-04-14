---
title: "Istruzioni di installazione certificato server IIS (Internet Information Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11281490-d2ac-4324-8f33-e7714611a34b
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Istruzioni di installazione certificato server IIS (Internet Information Services)
Per eseguire gli esempi che comunicano in modo sicuro con IIS \(Internet Information Services\) è necessario creare e installare un certificato server.  
  
## Passaggio 1.Creazione di certificati  
 Per creare un certificato per il computer, aprire un prompt dei comandi di Visual Studio con privilegi di amministratore ed eseguire Setup.bat incluso in ciascuno degli esempi che utilizza comunicazione sicure con IIS.Assicurarsi che il percorso includa la cartella contenente Makecert.exe prima di eseguire questo file batch.Il comando seguente viene utilizzato per creare il certificato nel file Setup.bat.  
  
```  
makecert -sr LocalMachine -ss My -n CN=ServiceModelSamples-HTTPS-Server -sky exchange -sk ServiceModelSamples-HTTPS-Key  
```  
  
## Passaggio 2.Installazione dei certificati  
 I passaggi necessari per installare i certificati appena creati dipendono dalla versione di IIS che si sta utilizzando.  
  
#### Installazione di IIS su IIS 5.1 \(Windows XP\) e IIS 6.0 \(Windows Server 2003\)  
  
1.  Aprire lo snap\-in MMC della Gestione Internet Information Services \(IIS\).  
  
2.  Fare clic con il pulsante destro del mouse sul Sito Web predefinito e selezionare **Proprietà**.  
  
3.  Selezionare la scheda **Sicurezza directory**.  
  
4.  Fare clic sul pulsante **Certificato server**.Verrà avviata la Procedura guidata certificati server Web.  
  
5.  Completare la procedura guidata.Selezionare l'opzione per assegnare un certificato.Selezionare il certificato server HTTPS ServiceModelSamples nell'elenco di certificati visualizzati.  
  
     ![Gestione guidata certificati IIS](../../../../docs/framework/wcf/samples/media/iiscertificate-wizard.GIF "IISCertificate\_Wizard")  
  
6.  Testare l’accesso al servizio in un browser utilizzando l'indirizzo HTTPS https:\/\/localhost\/servicemodelsamples\/service.svc.  
  
#### Se SSL è stato precedentemente configurato utilizzando Httpcfg.exe  
  
1.  Utilizzare Makecert.exe \(o eseguire Setup.bat\) per creare il certificato server.  
  
2.  Eseguire la gestione IIS e installare il certificato secondo i passaggi precedenti.  
  
3.  Aggiungere le righe di codice seguenti al programma client.  
  
> [!IMPORTANT]
>  Questo codice è necessario solo per certificati di prova come ad esempio quelli creati da Makecert.exe.Non è una pratica consigliabile per il codice di produzione.  
  
```  
PermissiveCertificatePolicy.Enact("CN=ServiceModelSamples-HTTPS-Server");  
```  
  
#### Per installare IIS su IIS 7.0 \(Windows Vista e Windows Server 2008\)  
  
1.  Dal menu **Start** fare clic su **Esegui**, quindi digitare **inetmgr** per aprire lo snap\-in MMC di Internet Information Services \(IIS\).  
  
2.  Fare clic con il pulsante destro del mouse su **Sito Web Predefinito** e selezionare **Modifica Associazioni…**  
  
3.  Fare clic sul pulsante **Aggiungi** della finestra di dialogo **Binding sito**.  
  
4.  Selezionare **HTTPS** dall’elenco a discesa **Tipo**.  
  
5.  Selezionare **ServiceModelSamples\-HTTPS\-Server** dall’elenco a discesa del **Certificato SSL** e fare clic su **OK**.  
  
6.  Testare l’accesso al servizio in un browser utilizzando l'indirizzo HTTPS https:\/\/localhost\/servicemodelsamples\/service.svc.  
  
> [!NOTE]
>  Dato che il certificato di prova appena installato non è un certificato attendibile, possono essere visualizzati avvisi di sicurezza di Internet Explorer aggiuntivi quando si visitano indirizzi Web locali protetti da questo certificato.  
  
## Rimozione dei certificati  
  
-   Utilizzare Gestione Internet Information Services come illustrato in precedenza, ma rimuovere il certificato o l'associazione anziché aggiungerlo.  
  
-   Rimuovere il certificato del computer utilizzando il comando seguente.  
  
    ```  
    httpcfg delete ssl -i 0.0.0.0:443  
    ```