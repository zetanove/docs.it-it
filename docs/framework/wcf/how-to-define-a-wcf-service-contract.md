---
title: "Procedura: definire un contratto di servizio di Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "contratti di servizio [WCF], definizione"
ms.assetid: 67bf05b7-1d08-4911-83b7-a45d0b036fc3
caps.latest.revision: 58
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 58
---
# Procedura: definire un contratto di servizio di Windows Communication Foundation
Questa è la prima delle sei attività necessarie per creare un'applicazione [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] di base.Per una panoramica di tutte e sei le attività, vedere l'argomento [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md).  
  
 Quando si crea un servizio di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] di base, la prima attività consiste nel definire un contratto di servizio.Nel contratto di servizio vengono specificate le operazioni supportate dal servizio.Un'operazione può essere considerata un metodo del servizio Web.I contratti vengono creati definendo un'interfaccia C\+\+, C\# o Visual Basic \(VB\).Ogni metodo nell'interfaccia corrisponde a un'operazione del servizio specifica.A ogni interfaccia deve essere applicato l'oggetto <xref:System.ServiceModel.ServiceContractAttribute> e a ogni operazione deve essere applicato l'attributo <xref:System.ServiceModel.OperationContractAttribute>.Se un metodo di un'interfaccia a cui è associato l'attributo <xref:System.ServiceModel.ServiceContractAttribute> non dispone dell'attributo <xref:System.ServiceModel.OperationContractAttribute>, tale metodo non viene esposto dal servizio.  
  
 Nell'esempio riportato dopo la procedura, viene fornito il codice utilizzato per questa attività.  
  
### Per definire un contratto di servizio  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] come amministratore facendo clic con il pulsante destro del mouse sul programma nel menu **Start** e selezionare **Esegui come amministratore**.  
  
2.  Creare un progetto di libreria di servizi WCF facendo clic sul menu **File** e scegliendo **Nuovo**, **Progetto**.Sul lato sinistro della finestra di dialogo **Nuovo progetto** espandere **Visual C\#** per un progetto C\# o **Altre linguaggi**, quindi **Visual Basic** per un progetto Visual Basic.Sotto il linguaggio selezionato scegliere **WCF**; in questo modo, nella sezione centrale della finestra di dialogo, verrà visualizzato un elenco dei modelli di progetto.Selezionare **Libreria di servizi WCF** e digitare `GettingStartedLib` nella casella di testo **Nome** e `GettingStarted` nella casella di testo **Nome soluzione** nella parte inferiore della finestra di dialogo.  
  
3.  Visual Studio creerà il progetto che contiene 3 file: IService1.cs \(or IService1.vb\), Service1.cs \(or Service1.vb\) e App.config.Il file IService1 contiene un contratto di servizio predefinito.Il file Service1 contiene un'implementazione predefinita del contratto di servizio.Il file app.config contiene la configurazione necessaria per caricare il servizio predefinito con l'host dei servizi WCF di Visual Studio.Per ulteriori informazioni sullo strumento Host del servizio WCF, vedere [Host servizio WCF \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)  
  
4.  Aprire il file IService1.cs o IService1.vb ed eliminare il codice all'interno della dichiarazione dello spazio dei nomi mantenendo però quest'ultima.All'interno della dichiarazione dello spazio dei nomi definire una nuova interfaccia denominata `ICalculator` come mostrato nel codice seguente.  
  
    ```  
    // IService.cs  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Runtime.Serialization;  
    using System.ServiceModel;  
    using System.Text;  
  
    namespace GettingStartedLib  
    {  
            [ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
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
    }  
  
    ```  
  
    ```  
    ‘IService.vb  
    Imports System  
    Imports System.ServiceModel  
  
    Namespace GettingStartedLib  
  
        <ServiceContract(Namespace:="http://Microsoft.ServiceModel.Samples")> _  
        Public Interface ICalculator  
  
            <OperationContract()> _  
            Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double  
            <OperationContract()> _  
            Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double  
            <OperationContract()> _  
            Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double  
            <OperationContract()> _  
            Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double  
        End Interface  
    End Namespace  
  
    ```  
  
     Questo contratto definisce una calcolatrice online.Si noti che l'interfaccia `ICalculator` è contrassegnata con l'attributo <xref:System.ServiceModel.ServiceContractAttribute>.Questo attributo definisce uno spazio dei nomi utilizzato per distinguere il nome del contratto.Ogni operazione della calcolatrice è contrassegnata con l'attributo <xref:System.ServiceModel.OperationContractAttribute>.  
  
    > [!NOTE]
    >  Quando vengono utilizzati attributi per annotare un'interfaccia, un membro o una classe, è possibile eliminare la parte "Attribute" dal nome dell'attributo.In questo modo <xref:System.ServiceModel.ServiceContractAttribute> diventa `[ServiceContract]` in C\# o `<ServiceContract>` in Visual Basic.  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 [Procedura: implementare un contratto di servizio](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)   
 [Guida introduttiva](../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [Servizio indipendente](../../../docs/framework/wcf/samples/self-host.md)