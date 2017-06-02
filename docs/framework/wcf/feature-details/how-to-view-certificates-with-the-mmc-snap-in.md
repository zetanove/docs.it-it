---
title: "Procedura: visualizzare certificati con lo snap-in MMC | Microsoft Docs"
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
  - "certificati [WCF], visualizzazione con lo snap-in MMC"
ms.assetid: 2b8782aa-ebb4-4ee7-974b-90299e356dc5
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Procedura: visualizzare certificati con lo snap-in MMC
Un tipo comune di credenziale è il certificato X.509.Al momento di creare servizi o client protetti, è possibile specificare il certificato che deve essere utilizzato come credenziale client o del servizio tramite metodi come, ad esempio, <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>.Il metodo richiede vari parametri, ad esempio l'archivio in cui il certificato è memorizzato e un valore da utilizzare quando si cerca il certificato.Nella procedura seguente viene illustrato come esaminare gli archivi in un computer per trovare un certificato adatto.Per un esempio di ricerca dell'identificazione personale del certificato, vedere [Procedura: recuperare l'identificazione personale di un certificato](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md).  
  
### Per visualizzare certificati nello snap\-in MMC  
  
1.  Aprire una finestra del prompt dei comandi.  
  
2.  Digitare `mmc`, quindi premere INVIO.Si noti che per visualizzare certificati nell'archivio del computer locale, è necessario avere il ruolo di Amministratore.  
  
3.  Scegliere **Aggiungi\/Rimuovi snap\-in** dal menu **File**.  
  
4.  Scegliere **Aggiungi**.  
  
5.  Nella finestra di dialogo **Aggiungi snap\-in autonomo**, selezionare **Certificati**.  
  
6.  Scegliere **Aggiungi**.  
  
7.  Nella finestra di dialogo **Snap\-in certificati**, selezionare **Account del computer** e fare clic su **Avanti**.Facoltativamente, è possibile selezionare **Account dell'utente** o **Account del servizio**.Se non si è un amministratore del computer, è possibile gestire i certificati solo per il proprio account utente.  
  
8.  Nella finestra di dialogo **Seleziona computer**, fare clic su **Fine**.  
  
9. Nella finestra di dialogo **Aggiungi snap\-in autonomo**, fare clic su **Chiudi**.  
  
10. Nella finestra di dialogo **Aggiungi\/Rimuovi snap\-in** fare clic su **OK**.  
  
11. Nella finestra **Radice console**, fare clic su **Certificati \(computer locale\)** per visualizzare gli archivi dei certificati per il computer.  
  
12. Facoltativo.Per visualizzare i certificati per il proprio account, ripetere i passaggi da 3 a 6.Nel passaggio 7, anziché selezionare **Account del computer**, fare clic su **Account dell'utente** e ripetere i passaggi da 8 a 10.  
  
13. Facoltativo.Scegliere **Salva** o **Salva con nome** dal menu **File**.Salvare il file di console per riutilizzarlo in seguito.  
  
## Visualizzazione di certificati con Internet Explorer  
 È anche possibile visualizzare, esportare, importare ed eliminare certificati utilizzando Internet Explorer.  
  
#### Per visualizzare certificati con Internet Explorer  
  
1.  In Internet Explorer, fare clic su  **Strumenti**,  **Opzioni Internet** per visualizzare la finestra di dialogo **Opzioni Internet**.  
  
2.  Fare clic sulla scheda **Contenuto**.  
  
3.  In **Certificati**, scegliere **Certificati**.  
  
4.  Per visualizzare i dettagli di qualsiasi certificato, selezionare il certificato e fare clic su **Visualizza**.  
  
## Vedere anche  
 [Utilizzo dei certificati](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Procedura: creare certificati temporanei da usare durante lo sviluppo](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)   
 [Procedura: recuperare l'identificazione personale di un certificato](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)