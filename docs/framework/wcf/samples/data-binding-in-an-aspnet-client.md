---
title: "Associazione dei dati in un client ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 68b49fa6-94e7-4d4c-a34e-902a2b3770b6
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Associazione dei dati in un client ASP.NET
In questo esempio viene descritto come associare i dati restituiti da un servizio tipico [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] in un'applicazione Web Form.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 In questo esempio viene illustrato un servizio che implementa un contratto in cui viene definito un modello di comunicazione richiesta\-risposta.L'esempio è costituito da un'applicazione Web Form client accessibile da un browser e un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ospitato su Internet Information Services \(IIS\).  
  
 Il servizio implementa un contratto che definisce il modello di comunicazione richiesta\-risposta.Il contratto viene definito mediante l'interfaccia `IWeatherService`, che espone un'operazione denominata `GetWeatherData`.Questa operazione accetta una matrice di città e restituisce una matrice di oggetti `WeatherData` che rappresentano la temperatura massima e minima prevista per una città.  
  
 Sulla pagina aspx del client [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], viene definito un controllo Web DataGrid che contiene la rappresentazione grafica dei dati restituiti dal servizio.Il codice presente sulla pagina aspx chiama il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per ottenere i dati meteorologici e li restituisce a una matrice di oggetti `WeatherData`.Il DataGrid specifica dove ottenere i dati impostando la proprietà `DataSource` su quella matrice.Si verifica l'associazione dati con una chiamata al metodo `DataBind` del DataGrid.Il codice è contenuto nel metodo `Page_Load` della pagina `aspx`, così ogni volta che l'utente aggiorna la pagina del browser, i dati vengono aggiornati nel DataGrid.  
  
### Per impostare, compilare ed eseguire l'esempio DIBLOOK  
  
1.  Assicurarsi di aver eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o in Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Il client di questo esempio è un sito Web che è in esecuzione sotto un server Web di sviluppo.Per avviare il server Web di sviluppo, digitare quanto segue nel prompt dei comandi: "`%SystemDrive%\Program Files\Common Files\Microsoft Shared\DevServer\9.0\WebDev.WebServer.EXE" /port:8000 /path:<WebFormsSamplePath>\CS\client /vpath:/client`.Quindi selezionare http:\/\/localhost:8000\/client.Per eseguire questo esempio tra più computer, sostituire tutti i riferimenti a `localhost` nel file Web.config del client con il nome del computer che ospita il server.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WebForms`  
  
## Vedere anche