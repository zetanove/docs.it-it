---
title: "Procedura: accedere ai servizi con un contratto duplex | Microsoft Docs"
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
helpviewer_keywords: 
  - "contratti duplex [WCF]"
ms.assetid: 746a9d64-f21c-426c-b85d-972e916ec6c5
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Procedura: accedere ai servizi con un contratto duplex
Una funzionalità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è la possibilità di creare un servizio che utilizza un modello di messaggistica duplex.Questo modello consente a un servizio di comunicare con il client tramite un callback.In questo argomento vengono illustrati i passaggi per creare un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in una classe client che implementa l'interfaccia di callback.  
  
 Un'associazione duale espone l'indirizzo IP del client al servizio.Nel client è necessario implementare un meccanismo di sicurezza in grado di garantire che il client si connetta solo a servizi ritenuti attendibili.  
  
 Per un'esercitazione sulla creazione di servizi e client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di base, vedere [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md).  
  
### Per accedere a un servizio duplex  
  
1.  Creare un servizio che contiene due interfacce.La prima interfaccia è per il servizio, la seconda è per il callback.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] creazione di un servizio duplex, vedere [Procedura: creare un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md).  
  
2.  Eseguire il servizio.  
  
3.  Utilizzare lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per generare contratti \(interfacce\) per il client.Per informazioni su tale procedura, vedere [Procedura: creare un client](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
4.  Implementare l'interfaccia di callback nella classe client, come illustrato nell'esempio seguente.  
  
    ```csharp  
    public class CallbackHandler : ICalculatorDuplexCallback  
    {  
        public void Result(double result)  
        {  
            Console.WriteLine("Result ({0})", result);  
        }  
        public void Equation(string equation)  
        {  
            Console.WriteLine("Equation({0})", equation);  
        }  
    }  
    ```  
  
    ```vb  
    Public Class CallbackHandler   
    Implements ICalculatorDuplexCallback  
       Public Sub Result (ByVal result As Double)  
          Console.WriteLine("Result ({0})", result)  
       End Sub  
        Public Sub Equation(ByVal equation As String)  
            Console.Writeline("Equation({0})", equation)  
        End Sub  
    End Class  
  
    ```  
  
5.  Creare un'istanza della classe <xref:System.ServiceModel.InstanceContext>.Il costruttore richiede un'istanza della classe client.  
  
    ```csharp  
    InstanceContext site = new InstanceContext(new CallbackHandler());  
    ```  
  
    ```vb  
    Dim site As InstanceContext = New InstanceContext(new CallbackHandler())  
    ```  
  
6.  Creare un'istanza del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzando il costruttore che richiede un oggetto <xref:System.ServiceModel.InstanceContext>.Il secondo parametro del costruttore è il nome di un endpoint contenuto nel file di configurazione.  
  
    ```csharp  
    CalculatorDuplexClient wcfClient =   
    new CalculatorDuplexClient(site, "default")  
    ```  
  
    ```vb  
    Dim wcfClient As New CalculatorDuplexClient(site, "default")  
    ```  
  
7.  Chiamare i metodi del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] secondo le esigenze.  
  
## Esempio  
 Nell'esempio di codice seguente viene descritto come creare una classe client che accede a un contratto duplex.  
  
 [!code-csharp[S_DuplexClients#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_duplexclients/cs/client.cs#1)]
 [!code-vb[S_DuplexClients#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_duplexclients/vb/client.vb#1)]  
  
## Sicurezza di .NET Framework  
  
## Vedere anche  
 [Esercitazione introduttiva](../../../../docs/framework/wcf/getting-started-tutorial.md)   
 [Procedura: creare un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)   
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [Procedura: creare un client](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [Procedura: usare ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)