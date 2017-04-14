---
title: "Procedura: utilizzare un moniker di servizio con i contratti WSDL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a88d9650-bb50-4f48-8c85-12f5ce98a83a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: utilizzare un moniker di servizio con i contratti WSDL
In alcune situazioni può essere necessario disporre di un client per l'interoperabilità COM completamente autonomo.Il servizio che si desidera chiamare può non esporre un endpoint MEX e la DLL del client WCF può non essere registrata per l'interoperabilità COM.In questi casi è possibile creare un file WSDL che descriva il servizio e lo passi nel moniker del servizio WCF.In questo argomento viene illustrato come chiamare l'esempio WCF della Guida introduttiva utilizzando un moniker WSDL WCF.  
  
### Utilizzo del moniker del servizio WSDL  
  
1.  Aprire e compilare la soluzione di esempio GettingStarted.  
  
2.  Aprire Internet Explorer e immettere http:\/\/localhost\/ServiceModelSamples\/Service.svc per assicurarsi che il servizio sia in funzione.  
  
3.  Nel file Service.cs aggiungere l'attributo seguente alla classe CalculatorService:  
  
     [!code-csharp[S_WSDL_Client#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wsdl_client/cs/service.cs#0)]  
  
4.  Aggiungere un spazio dei nomi dell'associazione al servizio App.config:  
  
  
  
5.  Creare un file WSDL che deve essere letto dall'applicazione.Poiché gli spazi dei nomi vengono aggiunti nei passaggi 3 e 4, è possibile utilizzare Internet Explorer per eseguire una query per l'intera descrizione WSDL del servizio immettendo http:\/\/localhost\/ServiceModelSamples\/Service.svc?wsdl.È quindi possibile salvare il file da Internet Explorer come serviceWSDL.xml.Se non si specificano gli spazi dei nomi nei passaggi 3 e 4, il documento WSDL restituito dalla query sull'URL precedente non sarà il WSDL completo.Il documento WSDL restituito includerà molte istruzioni di importazione che consentono di importare altri documenti WSDL.Sarà quindi necessario esaminare ogni istruzione di importazione e compilare il documento WSDL completo, combinando il WSDL restituito dal servizio con il WSDL importato.  
  
6.  Aprire Visual Basic 6.0 e creare un nuovo file standard con estensione exe.Aggiungere un pulsante al form e fare doppio clic su di esso per aggiungere il codice seguente al gestore Click:  
  
    ```  
    ' Open the WSDL contract file and read it all into the wsdlContract string.  
    Const ForReading = 1  
    Set objFSO = CreateObject("Scripting.FileSystemObject")  
    Set objFile = objFSO.OpenTextFile("c:\serviceWsdl.xml", ForReading)  
    wsdlContract = objFile.ReadAll  
    objFile.Close  
  
    ' Create a string for the service moniker including the content of the WSDL contract file.  
    wsdlMonikerString = "service4:address='http://localhost/ServiceModelSamples/service.svc'"  
    wsdlMonikerString = wsdlMonikerString + ", wsdl='" & wsdlContract & "'"  
    wsdlMonikerString = wsdlMonikerString + ", binding=WSHttpBinding_ICalculator, bindingNamespace='http://Microsoft.ServiceModel.Samples'"  
    wsdlMonikerString = wsdlMonikerString + ", contract=ICalculator, contractNamespace='http://Microsoft.ServiceModel.Samples'"  
  
    ' Create the service moniker object.  
    Set wsdlServiceMoniker = GetObject(wsdlMonikerString)  
  
    ' Call the service operations using the moniker object.  
    MsgBox "WSDL service moniker: 145 - 76.54 = " & wsdlServiceMoniker.Subtract(145, 76.54)  
    ```  
  
    > [!NOTE]
    >  Se il formato del moniker non è valido o se il servizio non è disponibile, la chiamata a `GetObject` restituirà un errore "Sintassi non valida".Se si riceve questo errore, verificare che il moniker che si sta utilizzando sia valido e che il servizio sia disponibile.  
  
7.  Eseguire l'applicazione Visual Basic.Verrà visualizzata una finestra di messaggio con i risultati della chiamata a Subtract\(145, 76.54\).  
  
## Vedere anche  
 [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [Panoramica sull'integrazione con applicazioni COM](../../../../docs/framework/wcf/feature-details/integrating-with-com-applications-overview.md)