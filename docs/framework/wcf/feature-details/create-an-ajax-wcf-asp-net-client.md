---
title: "Procedura: creare un servizio WCF compatibile con AJAX e un client ASP.NET che accede al servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 95012df8-2a66-420d-944a-8afab261013e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: creare un servizio WCF compatibile con AJAX e un client ASP.NET che accede al servizio
In questo argomento viene illustrato come utilizzare Visual Studio 2008 per creare un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] compatibile con AJAX e un client ASP.NET che accede a tale servizio. Il codice per il servizio e per il client viene fornito nella sezione Esempio dopo la descrizione dei passaggi necessari per la creazione del servizio e del client della sezione Procedure.  
  
### <a name="to-create-the-aspnet-client-application"></a>Per creare un'applicazione client ASP.NET  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Dal **File** dal menu **New**, quindi **progetto**, quindi **Web**, quindi selezionare **applicazione Web ASP.NET**.  
  
3.  Denominare il progetto `SandwichServices` e fare clic su **OK**.  
  
### <a name="to-create-the-wcf-ajax-enabled-service"></a>Per creare il servizio WCF compatibile con AJAX  
  
1.  Fare doppio clic sul `SandwichServices` nel progetto di **Esplora** finestra e selezionare **Aggiungi**, quindi **nuovo elemento**e quindi **sevizio WCF compatibile AJAX**.  
  
2.  Nome del servizio `CostService` nel **nome** casella e fare clic su **Aggiungi**.  
  
3.  Aprire il file CostService.svc.cs.  
  
4.  Specificare il `Namespace` per <xref:System.ServiceModel.ServiceContractAttribute> come `SandwichService`:  
  
    ```  
    namespace SandwichServices  
    {  
      [ServiceContract(Namespace = "SandwichServices")]  
      [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
       public class CostService  
       {  
         …  
       }  
     }  
    ```  
  
5.  Implementare le operazioni nel servizio. Aggiungere il <xref:System.ServiceModel.OperationContractAttribute> a ciascuna delle operazioni per indicare che fanno parte del contratto. Nell'esempio seguente viene implementato un metodo che restituisce il costo di una determinata quantità di panini.  
  
    ```  
    public class CostService  
    {  
        [OperationContract]  
        public double CostOfSandwiches(int quantity)  
        {  
            return 1.25 * quantity;  
        }  
  
    // Add more operations here and mark them with [OperationContract]  
    }  
    ```  
  
### <a name="to-configure-the-client-to-access-the-service"></a>Per configurare il client per l'accesso al servizio  
  
1.  Aprire la pagina default. aspx e selezionare il **progettazione** visualizzazione.  
  
2.  Dal **visualizzazione** dal menu **della casella degli strumenti**.  
  
3.  Espandere il **AJAX Extensions** nodo e trascinare un **ScriptManager** sulla pagina default. aspx.  
  
4.  Fare doppio clic su di **ScriptManager** e selezionare **proprietà**.  
  
5.  Espandere il **servizi** insieme il **proprietà** per aprire la finestra di **Editor della raccolta ServiceReference** finestra.  
  
6.  Fare clic su **Aggiungi**, specificare `CostService.svc` come il **percorso** a cui fa riferimento e fare clic su **OK**.  
  
7.  Espandere il **HTML** nodo il **della casella degli strumenti** e trascinare un **Input (pulsante)** sulla pagina default. aspx.  
  
8.  Fare doppio clic su di **pulsante** e selezionare **proprietà**.  
  
9. Modifica il **valore** campo `Price for 3 Sandwiches`.  
  
10. Fare doppio clic su di **pulsante** per accedere al codice JavaScript.  
  
11. Passare il codice JavaScript seguente all'interno di `script`> elemento.  
  
    ```  
    function Button1_onclick() {  
    var service = new SandwichServices.CostService();  
    service.CostOfSandwiches(3, onSuccess, null, null);  
    }  
  
    function onSuccess(result){  
    alert(result);  
    }  
    ```  
  
### <a name="to-access-the-service-from-the-client"></a>Per accedere al servizio dal client  
  
1.  Utilizzare Ctrl + F5 per avviare il servizio e il client Web. Fare clic su di **prezzo di 3 panini alla griglia** per generare l'output previsto di "3.75".  
  
## <a name="example"></a>Esempio  
 In questo esempio è contenuto il codice del servizio presente nel file WCFService.svc.cs e il codice del client presente nel file Default.aspx.  
  
```  
//The service code contained in the CostService.svc.cs file.  
  
using System;  
using System.Linq;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Activation;  
using System.ServiceModel.Web;  
  
namespace SandwichServices  
{  
    [ServiceContract(Namespace="SandwichServices")]  
    [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
    public class CostService  
    {  
        // Add [WebGet] attribute to use HTTP GET  
        [OperationContract]  
        public double CostOfSandwiches(int quantity)  
        {  
            return 1.25 * quantity;  
        }  
  
        // Add more operations here and mark them with [OperationContract]  
    }  
}  
//The code for hosting the service is contained in the CostService.svc file.  
  
<%@ ServiceHost Language="C#" Debug="true" Service="SandwichServices.CostService" CodeBehind="CostService.svc.cs" %>  
  
//The client code contained in the Default.aspx file.  
  
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="SandwichServices._Default" %>  
  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
  
<html >  
<head runat="server">  
    <title>Untitled Page</title>  
<script language="javascript" type="text/javascript">  
// <!CDATA[  
  
function Button1_onclick() {  
var service = new SandwichServices.CostService();  
service.CostOfSandwiches(3, onSuccess, null, null);  
}  
  
function onSuccess(result){  
alert(result);  
}  
  
// ]]>  
</script>  
</head>  
<body>  
    <form id="form1" runat="server">  
    <div>  
  
    </div>  
    <asp:ScriptManager ID="ScriptManager1" runat="server">  
        <services>  
            <asp:servicereference Path="CostService.svc" />  
        </services>  
    </asp:ScriptManager>  
    </form>  
    <p>  
        <input id="Button1" type="button" value="Price for 3 Sandwiches" onclick="return Button1_onclick()" /></p>  
</body>  
</html>  
  
```  
  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->