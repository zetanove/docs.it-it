---
title: "Utilizzo del moniker WCF con i client COM | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e2799bfe-88bd-49d7-9d6d-ac16a9b16b04
caps.latest.revision: 34
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 34
---
# Utilizzo del moniker WCF con i client COM
In questo esempio viene illustrato come usare il moniker del servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per integrare servizi Web in ambienti di sviluppo basati su COM, ad esempio Microsoft Office Visual Basic for Applications \(Office VBA\) o Visual Basic 6.0.  L'esempio è costituito da un client Windows Script Host \(file con estensione vbs\), una libreria di classi di supporto \(file con estensione dll\) e una libreria di servizi \(file con estensione dll\) ospitati in Internet Information Services \(IIS\).  Il servizio è un servizio di calcolatrice e il client COM chiama operazioni matematiche, Add, Subtract, Multiply e Divide, nel servizio.  L'attività del client è visibile nella finestra di messaggio.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Interop\COM`  
  
 Il servizio implementa un contratto `ICalculator` definito nel modo illustrato nel codice di esempio seguente.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
    [OperationContract]  
    double Subtract(double n1, double n2);  
    [OperationContract]  
    double Multiply(double n1, double n2);  
    [OperationContract]  
    double Divide(double n1, double n2);  
}  
```  
  
 Nell'esempio vengono descritti tre approcci alternativi per l'uso del moniker:  
  
-   Contratto tipizzato: il contratto viene registrato come tipo visibile a COM sul computer client.  
  
-   Contratto WSDL: il contratto viene fornito sotto forma di documento WSDL.  
  
-   Contratto MEX: il contratto viene recuperato in fase di esecuzione da un endpoint di scambio di metadati \(MEX\).  
  
## Contratto tipizzato  
 Per usare il moniker con un uso del contratto tipizzato, è necessario registrare con COM i tipi per il contratto di servizio forniti degli attribuiti appropriati.  Prima di tutto, è necessario generare un client usando lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  Eseguire il comando seguente da un prompt dei comandi nella directory del client per generare il proxy tipizzato.  
  
```  
svcutil.exe /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost/servicemodelsamples/service.svc /out:generatedClient.cs  
  
```  
  
 Questa classe deve essere inclusa in un progetto e il progetto deve essere configurato per generare un assembly visibile a COM e firmato durante la compilazione.  Nel file AssemblyInfo.cs deve essere incluso l'attributo seguente:  
  
```  
[assembly: ComVisible(true)]  
  
```  
  
 Dopo aver compilato il progetto, registrare i tipi visibili a COM usando `regasm`, come illustrato nell'esempio seguente:  
  
```  
regasm.exe /tlb:CalcProxy.tlb client.dll  
```  
  
 L'assembly creato deve essere aggiunto alla Global Assembly Cache.  Sebbene non sia strettamente obbligatoria, questa operazione semplifica il processo in cui la fase di esecuzione individua l'assembly.  Il comando seguente aggiunge l'assembly alla Global Assembly Cache.  
  
```  
gacutil.exe /i client.dll  
```  
  
> [!NOTE]
>  Il moniker del servizio richiede solo la registrazione del tipo e non usa il proxy per comunicare con il servizio.  
  
 L'applicazione client ComCalcClient.vbs usa la funzione `GetObject` per costruire un proxy per il servizio, usando la sintassi del moniker del servizio per specificare l'indirizzo, l'associazione e contratto per il servizio.  
  
```  
Set typedServiceMoniker = GetObject(  
"service4:address=http://localhost/ServiceModelSamples/service.svc, binding=wsHttpBinding,   
contractType={9213C6D2-5A6F-3D26-839B-3BA9B82228D3}")  
```  
  
 I parametri usati dal moniker specificano:  
  
-   L'indirizzo dell'endpoint del servizio.  
  
-   L'associazione che il client dovrebbe usare per connettersi a quell'endpoint.  In questo caso, il wsHttpBinding definito dal sistema viene usato anche se le associazioni personalizzate possono essere definite nei file di configurazione del client.  Per l'uso con Windows Script Host, l'associazione personalizzata viene definita in un file Cscript.exe.config nella stessa directory di Cscript.exe.  
  
-   Il tipo del contratto è supportato sull'endpoint.  Questo è il tipo generato e registrato in precedenza.  Poiché lo script di Visual Basic non fornisce un ambiente COM fortemente tipizzato, è necessario specificare un identificatore per il contratto.  Questo GUID è l'`interfaceID` da CalcProxy.tlb e può essere visualizzato usando gli strumenti COM, ad esempio il Visualizzatore oggetti OLE\/COM \(OleView.exe\).  Per ambienti fortemente tipizzati, ad esempio Office VBA o Visual Basic 6.0, è possibile aggiungere un riferimento esplicito alla libreria dei tipi e dichiarare quindi il tipo dell'oggetto proxy, invece di usare il parametro del contratto.  In questo modo si fornisce anche supporto IntelliSense durante lo sviluppo dell'applicazione client.  
  
 Una volta costruita l'istanza del proxy con il moniker del servizio, l'applicazione client può chiamare i metodi sul proxy e l'infrastruttura del moniker del servizio può chiamare le operazioni del servizio corrispondenti:  
  
```  
' Call the service operations using the moniker object  
WScript.Echo "Typed service moniker: 100 + 15.99 = " & typedServiceMoniker.Add(100, 15.99)  
  
```  
  
 Quando si esegue l'esempio, la risposta dell'operazione viene visualizzata in una finestra di messaggio di Windows Script Host.  Viene descritto un client COM che esegue chiamate COM usando il moniker tipizzato per comunicare con un servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Nonostante si usi COM nell'applicazione client, la comunicazione con il servizio è costituita solo da chiamate del servizio Web.  
  
## Contratto WSDL  
 Per usare il moniker con un contratto WSDL non è richiesta alcuna registrazione della libreria client, ma il contratto WSDL per il servizio deve essere recuperato tramite un meccanismo fuori banda, ad esempio usando un browser per accedere all'endpoint WSDL per il servizio.  Il moniker può accedere quindi a quel contratto in fase di esecuzione.  
  
 L'applicazione client ComCalcClient.vbs usa `FileSystemObject` per accedere al file WSDL salvato sul computer locale, quindi usa la funzione `GetObject` per costruire un proxy per il servizio:  
  
```  
' Open the WSDL contract file and read it all into the wsdlContract string  
Const ForReading = 1  
Set objFSO = CreateObject("Scripting.FileSystemObject")  
Set objFile = objFSO.OpenTextFile("serviceWsdl.xml", ForReading)  
wsdlContract = objFile.ReadAll  
objFile.Close  
  
' Create a string for the service moniker including the content of the WSDL contract file  
wsdlMonikerString = "service4:address='http://localhost/ServiceModelSamples/service.svc'"  
wsdlMonikerString = wsdlMonikerString + ", binding=WSHttpBinding_ICalculator, bindingNamespace='http://Microsoft.ServiceModel.Samples'"  
wsdlMonikerString = wsdlMonikerString + ", wsdl='" & wsdlContract & "'"  
wsdlMonikerString = wsdlMonikerString + ", contract=ICalculator, contractNamespace='http://Microsoft.ServiceModel.Samples'"  
  
' Create the service moniker object  
Set wsdlServiceMoniker = GetObject(wsdlMonikerString)  
```  
  
 I parametri usati dal moniker specificano:  
  
-   L'indirizzo dell'endpoint del servizio.  
  
-   L'associazione che il client deve usare per connettersi con quell'endpoint e lo spazio dei nomi nel quale viene definita quell'associazione.  In questo caso, viene usata `wsHttpBinding_ICalculator`.  
  
-   Il WSDL che definisce il contratto.  In questo caso è la stringa letta dal file serviceWsdl.xml.  
  
-   Il nome e lo spazio dei nomi del contratto.  Questa identificazione è richiesta perché il WSDL potrebbe contenere più di un contratto.  
  
    > [!NOTE]
    >  Per impostazione predefinita, i servizi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] generano file WSDL separati per ogni spazio dei nomi che usano.  Questi vengono collegati usando il costrutto di importazione di WSDL.  Poiché il moniker si aspetta una sola definizione WSDL, il servizio deve usare un solo spazio dei nomi, come illustrato in questo esempio, o i file separati devono essere uniti manualmente.  
  
 Una volta costruita l'istanza del proxy con il moniker del servizio, l'applicazione client può chiamare i metodi sul proxy e l'infrastruttura del moniker del servizio può chiamare le operazioni del servizio corrispondenti:  
  
```  
' Call the service operations using the moniker object  
WScript.Echo "WSDL service moniker: 145 - 76.54 = " & wsdlServiceMoniker.Subtract(145, 76.54)  
  
```  
  
 Quando si esegue l'esempio, la risposta dell'operazione viene visualizzata in una finestra di messaggio di Windows Script Host.  Viene descritto un client COM che esegue chiamate COM usando il moniker con un contratto WSDL per comunicare con un servizio di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Contratto di scambio di metadati  
 Per usare il moniker con un contratto MEX, come per il contratto WSDL, non è richiesta alcuna registrazione client.  Il contratto per il servizio viene recuperato in fase di esecuzione usando lo scambio di metadati interno.  
  
 L'applicazione client ComCalcClient.vbs usa quindi la funzione `GetObject` per costruire un proxy per il servizio.  
  
```  
' Create a string for the service moniker specifying the address to retrieve the service metadata from  
mexMonikerString = "service4:mexAddress='http://localhost/servicemodelsamples/service.svc/mex'"  
mexMonikerString = mexMonikerString + ", address='http://localhost/ServiceModelSamples/service.svc'"  
mexMonikerString = mexMonikerString + ", binding=WSHttpBinding_ICalculator, bindingNamespace='http://Microsoft.ServiceModel.Samples'"  
mexMonikerString = mexMonikerString + ", contract=ICalculator, contractNamespace='http://Microsoft.ServiceModel.Samples'"  
  
' Create the service moniker object  
Set mexServiceMoniker = GetObject(mexMonikerString)  
```  
  
 I parametri usati dal moniker specificano:  
  
-   L'indirizzo dell'endpoint di scambio di metadati del servizio.  
  
-   L'indirizzo dell'endpoint del servizio.  
  
-   L'associazione che il client deve usare per connettersi con quell'endpoint e lo spazio dei nomi nel quale viene definita quell'associazione.  In questo caso, viene usata `wsHttpBinding_ICalculator`.  
  
-   Il nome e lo spazio dei nomi del contratto.  Questa identificazione è richiesta perché il WSDL potrebbe contenere più di un contratto.  
  
 Una volta costruita l'istanza del proxy con il moniker del servizio, l'applicazione client può chiamare i metodi sul proxy e l'infrastruttura del moniker del servizio può chiamare le operazioni del servizio corrispondenti:  
  
```  
' Call the service operations using the moniker object  
WScript.Echo "MEX service moniker: 9 * 81.25 = " & mexServiceMoniker.Multiply(9, 81.25)  
  
```  
  
 Quando si esegue l'esempio, la risposta dell'operazione viene visualizzata in una finestra di messaggio di Windows Script Host.  Viene descritto un client COM che esegue chiamate COM usando il moniker con un contratto MEX per comunicare con un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
#### Per impostare e compilare l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  In un prompt dei comandi di [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] aprire la cartella \\client\\bin nella cartella specifica del linguaggio.  
  
    > [!NOTE]
    >  Se si usa [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../../includes/lserver-md.md)], Windows 7 o Windows Server 2008 R2, verificare di eseguire il prompt dei comandi con privilegi di amministratore.  
  
4.  Digitare `tlbexp.exe client.dll /out:CalcProxy.tlb` per esportare il file con estensione dll in un file con estensione tlb.  È previsto un "Avviso dell'utilità di esportazione della libreria dei tipi", ma ciò non rappresenta un problema, perché il tipo generico non è obbligatorio.  
  
5.  Digitare `regasm.exe /tlb:CalcProxy.tlb client.dll` per registrare i tipi con COM.  È previsto un "Avviso dell'utilità di esportazione della libreria dei tipi", ma ciò non rappresenta un problema, perché il tipo generico non è obbligatorio.  
  
6.  Digitare `gacutil.exe /i client.dll` per aggiungere l'assembly alla Global Assembly Cache.  
  
#### Per eseguire l'esempio nello stesso computer  
  
1.  Verificare l'accesso al servizio in un browser immettendo l'indirizzo seguente: `http://localhost/servicemodelsamples/service.svc`.  In risposta, viene visualizzata un pagina di conferma.  
  
2.  Eseguire ComCalcClient.vbs da \\client, nella cartella specifica della lingua.  L'attività del client viene visualizzata nella finestra di messaggio.  
  
3.  Se il client e il servizio non sono in grado di comunicare, vedere [Troubleshooting Tips](http://msdn.microsoft.com/it-it/8787c877-5e96-42da-8214-fa737a38f10b).  
  
#### Per eseguire l'esempio tra più computer  
  
1.  Sul computer del servizio creare una directory virtuale denominata ServiceModelSamples.  Lo script Setupvroot.bat incluso nell'esempio può essere usato per creare la directory del disco e quella virtuale.  
  
2.  Copiare i file del programma del servizio da %SystemDrive%\\Inetpub\\wwwroot\\servicemodelsamples nella directory virtuale di ServiceModelSamples nel computer del servizio.  Verificare di includere i file nella directory \\bin.  
  
3.  Copiare il file script del client dalla cartella \\client, nella cartella specifica della lingua, ne computer client.  
  
4.  Nel file script modificare il valore dell'indirizzo della definizione dell'endpoint affinché corrisponda al nuovo indirizzo del servizio.  Nell'indirizzo sostituire qualsiasi riferimento a "localhost" con un nome di dominio completo.  
  
5.  Copiare il file WSDL nel computer client.  Nel file WSDL, serviceWsdl.xml, sostituire qualsiasi riferimento a "localhost" con un nome di dominio completo nell'indirizzo.  
  
6.  Copiare la libreria Client.dll dalla cartella \\client\\bin\\, nella cartella specifica della lingua, a una directory sul computer client.  
  
7.  Da un prompt dei comandi spostarsi a tale directory di destinazione sul computer client.  Se si usa [!INCLUDE[wv](../../../../includes/wv-md.md)] o [!INCLUDE[lserver](../../../../includes/lserver-md.md)] assicurarsi di eseguire il prompt dei comandi come amministratore.  
  
8.  Digitare `tlbexp.exe client.dll /out:CalcProxy.tlb` per esportare il file con estensione dll in un file con estensione tlb.  È previsto un "Avviso dell'utilità di esportazione della libreria dei tipi", ma ciò non rappresenta un problema, perché il tipo generico non è obbligatorio.  
  
9. Digitare `regasm.exe /tlb:CalcProxy.tlb client.dll` per registrare i tipi con COM.  Assicurarsi che il percorso sia stato impostato sulla cartella che contiene `regasm.exe` prima di eseguire il comando.  
  
10. Digitare `gacutil.exe /i client.dll` per aggiungere l'assembly alla Global Assembly Cache.  Assicurarsi che il percorso sia stato impostato sulla cartella che contiene `gacutil.exe` prima di eseguire il comando.  
  
11. Verificare che sia possibile accedere al servizio dal computer client usando un browser.  
  
12. Sul computer client avviare ComCalcClient.vbs.  
  
#### Per eseguire la pulizia dopo l'esempio  
  
-   Per motivi di sicurezza, rimuovere la definizione della directory virtuale e le autorizzazioni concesse durante l'installazione quando si è finito di lavorare con gli esempi eseguendo il file batch denominato Cleanupvroot.bat.  
  
## Vedere anche