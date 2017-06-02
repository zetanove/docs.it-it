---
title: "File Leggimi sull&#39;esempio relativo alla protezione estesa per l&#39;autenticazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80bf2e97-398d-4db5-9040-d96478a2ccab
caps.latest.revision: 3
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 3
---
# File Leggimi sull&#39;esempio relativo alla protezione estesa per l&#39;autenticazione
La protezione estesa è un'iniziativa per la sicurezza che consente di impedire attacchi man\-in\-the\-middle \(MITM\) in cui l'autore di un attacco intercetta le credenziali del client e le utilizza per accedere a risorse protette nel server associato al client.  
  
 Per ulteriori informazioni, vedere [Panoramica sulla protezione estesa per l'autenticazione](../../../../docs/framework/wcf/feature-details/extended-protection-for-authentication-overview.md).  
  
> [!NOTE]
>  Questo esempio funziona solo quando è ospitato in IISe non funziona in Visual Studio Development Server perché non supporta HTTPS.  
  
## Per impostare, compilare ed eseguire l'esempio  
  
1.  Installare IIS nel computer utilizzando Installazione applicazioni \-\> Funzionalità Windows.  
  
2.  Attivare l'autenticazione di Windows nelle funzionalità di Windows, ovvero Internet Information Services \-\> Servizi World Wide Web \-\> Sicurezza \-\> Autenticazione Windows.  
  
3.  Abilitare l'attivazione HTTP nelle funzionalità di Windows, ovvero Microsoft .NET Framework 3.5.1 \-\> Attivazione HTTP di Windows Communication Foundation.  
  
4.  In questo esempio il client deve stabilire un canale protetto con il server ed è di conseguenza necessario che sia presente un certificato del server che può essere installato da Gestione Internet Information Services.  
  
    1.  Aprire Gestione IIS \-\> Certificati server \(dalla scheda delle funzionalità\).  
  
    2.  Ai fini dimostrativi di questo esempio, è possibile creare un certificato autofirmato.Se non si desidera che venga visualizzato un messaggio relativo alla sicurezza del certificato, è possibile installare un certificato presente nell'archivio Autorità di certificazione radice attendibili.  
  
5.  Spostarsi sul riquadro azioni per il sito Web predefinito.Fare clic su Modifica sito \-\> Binding.Aggiungere HTTPS come tipo, se non è già presente, con il numero di porta 443 e assegnare il certificato SSL creato nel passaggio precedente.  
  
6.  Compilare il servizio.In questo modo viene creata automaticamente una directory virtuale in IIS \(dall'azione di post\-compilazione specificata nelle proprietà di progetto\) e vengono copiati i file con estensione dll e svc e il file di configurazione per un servizio da ospitare nel Web.  
  
7.  Aprire Gestione IIS.Fare clic con il pulsante destro del mouse sulla directory virtuale \(ExtendedProtection\) creata nel passaggio precedente, quindi scegliere Converti in applicazione.  
  
8.  Aprire il modulo di autenticazione in Gestione IIS relativo alla directory virtuale e abilitare l'autenticazione di Windows.  
  
9. Aprire le impostazioni avanzate per l'autenticazione di Windows relativa alla directory virtuale e specificare il valore in modo che sia richiesta poiché nell'esempio il valore ExtendedProtection corrispondente è impostata su Sempre.  
  
10. Per testare il servizio, accedere all'URL da una finestra del browser.Se si desidera accedere a tale URL da più computer, verificare che il firewall sia aperto per tutte le connessioni HTTP e HTTPS in ingresso.  
  
11. Aprire il file di configurazione del client e fornire un nome di computer completo per l'attributo dell'indirizzo \<client\> \- \<endpoint\>, sostituendo \<\<full\_machine\_name\>\>.  
  
12. Eseguire il client.Per comunicare con il servizio, il client stabilisce un canale protetto e utilizza la protezione estesa tra gli elementi.