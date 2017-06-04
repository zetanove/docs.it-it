---
title: "Istruzioni per la configurazione di directory virtuali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 3c62cab5-81a4-48b6-ac8c-9ce33a85a157
caps.latest.revision: 36
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 36
---
# Istruzioni per la configurazione di directory virtuali
Gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] devono condividere una directory virtuale comune denominata servicemodelsamples associata alla cartella %SystemDrive%\\inetpub\\wwwroot\\servicemodelsamples.  
  
> [!NOTE]
>  %SystemDrive% è in genere C: o D:, a seconda della posizione dell'unità dove è installato IIS \(Internet Information Services\).  
  
 È possibile eseguire i file Setupvroot.bat e Cleanupvroot.bat da [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) per creare la directory virtuale.Se si preferisce creare la directory virtuale manualmente, utilizzare le procedure seguenti.  
  
## Procedure  
  
#### Per creare una directory virtuale in IIS 7.0 o 7.5  
  
1.  Dal menu **Start** fare clic su **Esegui**, quindi scegliere **inetmgr** per aprire lo snap\-in MMC di Internet Information Services \(IIS\).  
  
2.  Nel riquadro sinistr, espandere il nodo con il nome del computer, quindi espandere il nodo **Siti**.  
  
3.  Fare clic con il pulsante destro del mouse su **Sito Web predefinito**, selezionare **Aggiungi applicazione** per aprire la finestra **Aggiungi applicazione**.  
  
4.  Nella finestra, digitare  `servicemodelsamples` come alias della directory virtuale che si sta creando.  
  
5.  Creare la directory seguente: %SystemDrive%\\inetpub\\wwwroot\\servicemodelsamples  
  
6.  Impostare il percorso fisico su %SystemDrive%\\inetpub\\wwwroot\\servicemodelsamples.Molti degli esempi WCF copiano file eseguibili di servizi in questo percorso quando vengono generati.  
  
7.  Fare clic su **OK**.L'applicazione Web è stata creata per gli esempi WCF.  
  
    > [!NOTE]
    >  Questa attività deve essere eseguita solo una volta poiché tutti gli esempi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzano la stessa applicazione Web servicemodelsamples.  
  
    > [!NOTE]
    >  Ai fini di questa documentazione, il termine `virtual directory` è sinonimo di `Web application`.  
  
     Oltre a creare la directory virtuale, è necessario impostarne le proprietà per consentire ai servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di essere in esecuzione.Di seguito sono riportate informazioni dettagliate.  
  
#### Per creare una directory virtuale in IIS 5.1 o 6.0  
  
1.  Aprire una finestra del prompt dei comandi e digitare `start inetmgr` per aprire lo snap\-in MMC di Internet Information Services \(IIS\).  
  
2.  Nel riquadro sinistro, espandere il nodo con il nome del computer, quindi espandere il nodo **Siti Web**.  
  
3.  Fare clic con il pulsante destro del mouse su **Sito Web predefinito** e selezionare **Nuovo, Directory virtuale** per avviare la procedura guidata Creazione directory virtuale.  
  
4.  Nella procedura guidata, digitare  `servicemodelsamples` come alias della directory virtuale che si sta creando.  
  
5.  Impostare il percorso su %SystemDrive%\\inetpub\\wwwroot\\servicemodelsamples.Molti degli esempi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] copiano file eseguibili di servizi in questo percorso quando vengono generati.  
  
6.  Fare clic su **Avanti**.  
  
7.  Per impostazione predefinita, le caselle di controllo seguenti sono selezionate:  
  
    -   **Lettura**  
  
    -   **Esecuzione script \(ad esempio, ASP\)**  
  
8.  Fare clic su **Avanti**, quindi su **Fine** per completare la procedura guidata.  
  
    > [!NOTE]
    >  Questa attività deve essere eseguita solo una volta poiché tutti gli esempi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzano la stessa directory virtuale servicemodelsamples.  
  
#### Per impostare proprietà aggiuntive della directory virtuale in IIS 7.0 o 7.5  
  
1.  Fare clic sul nodo servicemodelsamples.Lungo la parte inferiore della finestra sono elencate due visualizzazioni.Se non è ancora selezionata, selezionare l'opzione **Visualizzazione funzionalità**.  
  
2.  Fare doppio clic sulla voce per **Esplorazione directory**.  
  
3.  Nel riquadro Azioni selezionare l'opzione **Abilita**.In questo modo sarà possibile accedere alla directory della directory utilizzando Internet Explorer che facilita l’esecuzione del debug di un servizio.  
  
 Infine, è necessario impostare le proprietà di sicurezza della cartella servicemodelsamples per renderla accessibile ad altri.Di seguito sono riportate informazioni dettagliate.  
  
#### Per impostare proprietà aggiuntive della directory virtuale in IIS 5.1 o 6.0  
  
1.  Fare clic con il pulsante destro del mouse sul nodo servicemodelsamples, quindi scegliere **Proprietà**.  
  
2.  Per impostazione predefinita, le caselle di controllo seguenti sono selezionate:  
  
    -   **Lettura**  
  
    -   **Registrazione visite**  
  
    -   **Indicizza questa risorsa**  
  
3.  Selezionare la casella di controllo **Esplorazione directory**.In questo modo sarà possibile accedere alla directory della directory utilizzando Internet Explorer che facilita l’esecuzione del debug di un servizio.  
  
#### Per impostare le proprietà di sicurezza della cartella in IIS 7.0 o 7.5  
  
1.  Passare a %SystemDrive%\\inetpub\\wwwroot\\servicemodelsamples.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella, quindi scegliere **Condividi** o **Condividi con**.  
  
3.  Fare clic sulla freccia verso il basso alla sinistra del pulsante **Aggiungi**.  
  
4.  Selezionare la voce **Trova**.Verrà visualizzata la finestra **Selezione utenti o gruppi**.  
  
5.  Fare clic su **Avanzate**.  
  
6.  Fare clic su **Percorsi**.Verrà aperta la finestra **Percorsi**.  
  
7.  Selezionare la voce per il computer utilizzato.È importante selezionare il computer locale e non una voce per qualsiasi dominio o reti elencati.Dopo aver selezionato il computer, fare clic su **OK**.  
  
8.  Fare clic su **Trova**.Nei risultati di ricerca vengono inseriti gli oggetti associati al computer locale.  
  
9. Cercare la voce **IIS\_IUSRS** nella colonna **Nome \(RDN\)**.Selezionare tale voce e fare clic su **OK** per chiudere la finestra dei risultati della ricerca.  
  
10. Fare clic su **OK** per chiudere la finestra **Selezione utenti o gruppi**.  
  
11. Fare clic su **Condividi** per mantenere le modifiche.  
  
12. Una volta completate le modifiche per abilitare la condivisione, fare clic su **Completato** per chiudere la finestra **Condivisione File**.  
  
#### Per impostare le proprietà di sicurezza della cartella in IIS 5.1 o 6.0  
  
1.  Passare a %SystemDrive%\\inetpub\\wwwroot\\servicemodelsamples.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **servicemodelsamples**, quindi scegliere **Condivisione e protezione**.  
  
3.  Fare clic sulla scheda **Sicurezza**.  
  
4.  Se si sta utilizzando IIS 6.0, nella casella **Utenti e gruppi** verificare che l’**Account Internet Guest** sia elencato.  
  
     Se non è elencato:  
  
    1.  Fare clic sul pulsante **Start**, quindi scegliere **Pannello di controllo**.  
  
    2.  Se non viene visualizzata l'icona **Account utente** fare clic su **Passa alla visualizzazione per categorie**.  
  
    3.  Fare clic sull'icona **Account utente**.  
  
    4.  In “o seleziona una icona del Pannello di controllo”, fare clic su **Account utente**.  
  
    5.  Nella finestra di dialogo **Account utente** fare clic sulla scheda **Avanzate**.  
  
    6.  Fare clic su **Avanzate**.  
  
    7.  Nella finestra di dialogo **Utenti e gruppi locali** fare clic per espandere la cartella **Utenti**.  
  
    8.  Nel riquadro di destra, fare doppio clic su **Account Internet Guest**.  
  
    9. Nella finestra di dialogo **Proprietà**, copiare il nome utilizzato come account Internet guest.Per impostazione predefinita, il nome inizia con “USR\_” seguito dal nome del computer.  
  
    10. Chiudere la finestra di dialogo **Proprietà**.  
  
    11. Chiudere la finestra di dialogo **Utenti e gruppi locali**.  
  
    12. Chiudere la finestra di dialogo **Account utente**.  
  
    13. Chiudere l’altra finestra di dialogo **Account utente**.  
  
    14. Nella finestra di dialogo **Proprietà \- servicemodelsamples** fare clic su **Aggiungi** nella scheda **Sicurezza**.  
  
    15. Digitare il nome del computer seguito da una barra rovesciata, quindi incollare il nome dell'account utente di Internet, ad esempio, NomeComputer\\%NomeAccountGuestInternet\\%  
  
    16. Fare clic sul pulsante **Controlla nomi** per verificare l'aggiunta.Se è valido, il nome è composto di tutti caratteri maiuscoli ed è sottolineato.  
  
5.  Per IIS 6.0, controllare anche che SERVIZIO DI RETE sia elencato nella casella **Utenti e gruppi**.  
  
     Se SERVIZIO DI RETE non è elencato:  
  
    1.  Fare clic su **Aggiungi**.  
  
    2.  Nella finestra di dialogo **Selezione utenti o gruppi** digitare il nome del computer seguito da una barra rovesciata.  
  
    3.  Digitare service dopo la barra rovesciata \(senza spazi\).  
  
    4.  Scegliere **Controlla nomi**.  
  
    5.  Se vengono trovati più nomi, selezionare **SERVIZIO DI RETE** e fare clic su **OK**.  
  
    6.  Fare clic su **OK** per chiudere la finestra di dialogo **Selezione utenti o gruppi**.  
  
6.  Se si sta utilizzando Windows XP SP2 con IIS 5.1, controllare che Account Internet Guest e ASPNET siano elencati nella casella **Utenti e gruppi**.  
  
     Si noti che l'utente ASPNET può essere un membro del gruppo di sicurezza **Utenti** incorporato.Quindi, se il gruppo **Utenti** è elencato nella finestra di dialogo, non è necessario aggiungerlo come elemento separato nell'elenco di utenti consentiti.  
  
     Per controllare se ASPNET fa parte del gruppo di sicurezza **Utenti**:  
  
    1.  Fare clic sul menu **Start**, quindi scegliere **Pannello di controllo**.  
  
    2.  Fare clic sull'icona **Account utente**.  
  
    3.  Nella colonna **Gruppo**, controllare che il valore per **ASPNET** sia “Utenti”.  
  
## Vedere anche  
 [Istruzioni per l'hosting su IIS \(Internet Information Services\)](../../../../docs/framework/wcf/samples/internet-information-service-hosting-instructions.md)