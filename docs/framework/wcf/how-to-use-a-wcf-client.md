---
title: "Procedura: usare un client di Windows Communication Foundation | Microsoft Docs"
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
  - "Client WCF [WCF], utilizzo"
ms.assetid: 190349fc-0573-49c7-bb85-8e316df7f31f
caps.latest.revision: 38
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 38
---
# Procedura: usare un client di Windows Communication Foundation
Questa è l'ultima delle sei attività necessarie per creare un'applicazione [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] di base.  Per una panoramica di tutte e sei le attività, vedere l'argomento [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md).  
  
 Una volta creato e configurato un proxy [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], è possibile creare un'istanza del client e l'applicazione client può essere compilata e utilizzata per comunicare con il servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  In questo argomento vengono illustrate le procedure per la creazione di un'istanza e l'utilizzo di un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  La procedura consente di eseguire tre operazioni:  
  
1.  Creazione di un'istanza di un client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
2.  Chiamata delle operazioni del servizio dal proxy generato.  
  
3.  Chiusura del client dopo il completamento dell'operazione.  
  
### Per utilizzare un client di Windows Communication Foundation  
  
1.  Aprire il file Program.cs o Program.vb dal progetto GettingStartedClient e sostituire il codice esistente con quello seguente:  
  
    ```  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using GettingStartedClient.ServiceReference1;  
  
    namespace GettingStartedClient  
    {  
        class Program  
        {  
            static void Main(string[] args)  
            {  
                //Step 1: Create an instance of the WCF proxy.  
                CalculatorClient client = new CalculatorClient();  
  
                // Step 2: Call the service operations.  
                // Call the Add service operation.  
                double value1 = 100.00D;  
                double value2 = 15.99D;  
                double result = client.Add(value1, value2);  
                Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
                // Call the Subtract service operation.  
                value1 = 145.00D;  
                value2 = 76.54D;  
                result = client.Subtract(value1, value2);  
                Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
                // Call the Multiply service operation.  
                value1 = 9.00D;  
                value2 = 81.25D;  
                result = client.Multiply(value1, value2);  
                Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
                // Call the Divide service operation.  
                value1 = 22.00D;  
                value2 = 7.00D;  
                result = client.Divide(value1, value2);  
                Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
                //Step 3: Closing the client gracefully closes the connection and cleans up resources.  
                client.Close();  
            }  
        }  
    }  
  
    ```  
  
    ```  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.Text  
    Imports System.ServiceModel  
    Imports GettingStartedClientVB2.ServiceReference1  
  
    Module Module1  
  
        Sub Main()  
            ' Step 1: Create an instance of the WCF proxy  
            Dim Client As New CalculatorClient()  
  
            'Step 2: Call the service operations.  
            'Call the Add service operation.  
            Dim value1 As Double = 100D  
            Dim value2 As Double = 15.99D  
            Dim result As Double = Client.Add(value1, value2)  
            Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)  
  
            'Call the Subtract service operation.  
            value1 = 145D  
            value2 = 76.54D  
            result = Client.Subtract(value1, value2)  
            Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result)  
  
            'Call the Multiply service operation.  
            value1 = 9D  
            value2 = 81.25D  
            result = Client.Multiply(value1, value2)  
            Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result)  
  
            'Call the Divide service operation.  
            value1 = 22D  
            value2 = 7D  
            result = Client.Divide(value1, value2)  
            Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result)  
  
            ' Step 3: Closing the client gracefully closes the connection and cleans up resources.  
            Client.Close()  
  
            Console.WriteLine()  
            Console.WriteLine("Press <ENTER> to terminate client.")  
            Console.ReadLine()  
  
        End Sub  
  
    End Module  
  
    ```  
  
     Si noti l'istruzione Using o Imports con cui viene importato l'oggetto GettingStartedClient.ServiceReference1.  In questo modo viene importato il codice generato da Aggiungi riferimento al servizio in Visual Studio.  Il codice crea un'istanza del proxy WCF, chiama tutte le operazioni del servizio esposte dal servizio calcolatrice, chiude il proxy, quindi termina.  
  
 L'esercitazione è ora completata.  È stato definito e implementato un contratto di servizio, è stato generato un proxy WCF, è stata configurata un'applicazione client WCF, quindi è stato utilizzato il proxy per chiamare le operazioni del servizio.  Per testare l'applicazione, eseguire innanzitutto GettingStartedHost per l'avvio del servizio, quindi eseguire GettingStartedClient.  L'aspetto dell'output da GettingStartedHost è simile al seguente:  
  
```Output  
  
            Il servizio è pronto.  Premere <INVIO> per terminare il servizio.  Received Add(100,15.99)  
Valore restituito: 115,99  
Received Subtract(145,76.54)  
Valore restituito: 68,46  
Received Multiply(9,81.25)  
Valore restituito: 731,25  
Received Divide(22,7)  
Valore restituito: 3,14285714285714    
```  
  
 L'aspetto dell'output da GettingStartedClient è simile al seguente:  
  
```Output  
  
            Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Premere <INVIO> per terminare il client.  
  
```  
  
## Vedere anche  
 [Creazione di client](../../../docs/framework/wcf/building-clients.md)   
 [Procedura: creare un client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md)   
 [Programmazione WCF di base](../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Procedura: creare un contratto duplex](../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)   
 [Procedura: accedere ai servizi con un contratto duplex](../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)   
 [Guida introduttiva](../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [Servizio indipendente](../../../docs/framework/wcf/samples/self-host.md)