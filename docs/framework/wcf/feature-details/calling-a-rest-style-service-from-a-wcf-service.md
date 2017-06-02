---
title: "Chiamata di un servizio in stile REST da un servizio WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77df81d8-7f53-4daf-8d2d-bf7996e94d5a
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Chiamata di un servizio in stile REST da un servizio WCF
Quando si chiama un servizio in stile REST da un normale un servizio WCF \(basato su SOAP\), il contesto dell'operazione sul metodo del servizio \(contenente le informazioni sulla richiesta in entrata\) sostituisce il contesto che deve essere utilizzato dalla richiesta in uscita.  Ciò determina la modifica delle richieste HTTP GET in richieste HTTP.  Per forzare il servizio WCF a utilizzare il giusto contesto per chiamare il servizio in stile REST, creare un nuovo oggetto <xref:System.ServiceModel.OperationContextScope> e chiamare il servizio in stile REST dall'ambito del contesto dell'operazione.  In questo argomento viene descritto come creare un semplice esempio che illustra questa tecnica.  
  
## Definire il contratto del servizio in stile REST  
 Definire un semplice contratto del servizio in stile REST:  
  
```  
[ServiceContract]  
        public interface IRestInterface  
        {  
            [OperationContract, WebGet]  
            int Add(int x, int y);  
            [OperationContract, WebGet]  
            string Echo(string input);  
        }  
```  
  
## Implementare il contratto del servizio in stile REST  
 Implementare il contratto del servizio in stile REST:  
  
```  
public class RestService : IRestInterface  
        {  
            public int Add(int x, int y)  
            {  
                return x + y;  
            }  
  
            public string Echo(string input)  
            {  
                return input;  
            }  
        }  
  
```  
  
## Definire il contratto di servizio WCF  
 Definire un contratto di servizio WCF che verrà utilizzato per chiamare il servizio in stile REST:  
  
```  
[ServiceContract]  
 public interface INormalInterface  
 {  
     [OperationContract]  
     int CallAdd(int x, int y);  
     [OperationContract]  
     string CallEcho(string input);  
 }  
```  
  
## Implementare il contratto di servizio WCF  
 Implementare il contratto di servizio WCF:  
  
```  
public class NormalService : INormalInterface  
        {  
            static MyRestClient client = new MyRestClient(RestServiceBaseAddress);  
            public int CallAdd(int x, int y)  
            {  
                return client.Add(x, y);  
            }  
  
            public string CallEcho(string input)  
            {  
                return client.Echo(input);  
            }  
        }  
```  
  
## Creare il proxy client per il servizio in stile REST  
 Utilizzo di <xref:System.ServiceModel.ClientBase%60> per implementare il proxy client.  Per ogni metodo chiamato, un nuovo oggetto <xref:System.ServiceModel.OperationContextScope> viene creato e utilizzato per chiamare l'operazione.  
  
```  
public class MyRestClient : ClientBase<IRestInterface>, IRestInterface  
        {  
            public MyRestClient(string address)  
                : base(new WebHttpBinding(), new EndpointAddress(address))  
            {  
                this.Endpoint.Behaviors.Add(new WebHttpBehavior());  
            }  
  
            public int Add(int x, int y)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Add(x, y);  
                }  
            }  
  
            public string Echo(string input)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Echo(input);  
                }  
            }  
        }  
```  
  
## Ospitare e chiamare i servizi  
 Ospitare entrambi i servizi in un'applicazione console, aggiungendo gli endpoint e i comportamenti necessari.  Quindi, chiamare il servizio WCF normale:  
  
```  
public static void Main()  
        {  
            ServiceHost restHost = new ServiceHost(typeof(RestService), new Uri(RestServiceBaseAddress));  
            restHost.AddServiceEndpoint(typeof(IRestInterface), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            restHost.Open();  
  
            ServiceHost normalHost = new ServiceHost(typeof(NormalService), new Uri(NormalServiceBaseAddress));  
            normalHost.AddServiceEndpoint(typeof(INormalInterface), new BasicHttpBinding(), "");  
            normalHost.Open();  
  
            Console.WriteLine("Hosts opened");  
  
            ChannelFactory<INormalInterface> factory = new ChannelFactory<INormalInterface>(new BasicHttpBinding(), new EndpointAddress(NormalServiceBaseAddress));  
            INormalInterface proxy = factory.CreateChannel();  
  
            Console.WriteLine(proxy.CallAdd(123, 456));  
            Console.WriteLine(proxy.CallEcho("Hello world"));  
        }  
```  
  
## Elenco codice completo  
 Di seguito è riportato un elenco completo dell'esempio implementato in questo argomento:  
  
```  
public class CallingRESTSample  
    {  
        static readonly string RestServiceBaseAddress = "http://" + Environment.MachineName + ":8008/Service";  
        static readonly string NormalServiceBaseAddress = "http://" + Environment.MachineName + ":8000/Service";  
  
        [ServiceContract]  
        public interface IRestInterface  
        {  
            [OperationContract, WebGet]  
            int Add(int x, int y);  
            [OperationContract, WebGet]  
            string Echo(string input);  
        }  
  
        [ServiceContract]  
        public interface INormalInterface  
        {  
            [OperationContract]  
            int CallAdd(int x, int y);  
            [OperationContract]  
            string CallEcho(string input);  
        }  
  
        public class RestService : IRestInterface  
        {  
            public int Add(int x, int y)  
            {  
                return x + y;  
            }  
  
            public string Echo(string input)  
            {  
                return input;  
            }  
        }  
  
        public class MyRestClient : ClientBase<IRestInterface>, IRestInterface  
        {  
            public MyRestClient(string address)  
                : base(new WebHttpBinding(), new EndpointAddress(address))  
            {  
                this.Endpoint.Behaviors.Add(new WebHttpBehavior());  
            }  
  
            public int Add(int x, int y)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Add(x, y);  
                }  
            }  
  
            public string Echo(string input)  
            {  
                using (new OperationContextScope(this.InnerChannel))  
                {  
                    return base.Channel.Echo(input);  
                }  
            }  
        }  
  
        public class NormalService : INormalInterface  
        {  
            static MyRestClient client = new MyRestClient(RestServiceBaseAddress);  
            public int CallAdd(int x, int y)  
            {  
                return client.Add(x, y);  
            }  
  
            public string CallEcho(string input)  
            {  
                return client.Echo(input);  
            }  
        }  
        public static void Main()  
        {  
            ServiceHost restHost = new ServiceHost(typeof(RestService), new Uri(RestServiceBaseAddress));  
            restHost.AddServiceEndpoint(typeof(IRestInterface), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            restHost.Open();  
  
            ServiceHost normalHost = new ServiceHost(typeof(NormalService), new Uri(NormalServiceBaseAddress));  
            normalHost.AddServiceEndpoint(typeof(INormalInterface), new BasicHttpBinding(), "");  
            normalHost.Open();  
  
            Console.WriteLine("Hosts opened");  
  
            ChannelFactory<INormalInterface> factory = new ChannelFactory<INormalInterface>(new BasicHttpBinding(), new EndpointAddress(NormalServiceBaseAddress));  
            INormalInterface proxy = factory.CreateChannel();  
  
            Console.WriteLine(proxy.CallAdd(123, 456));  
            Console.WriteLine(proxy.CallEcho("Hello world"));  
        }  
    }  
```  
  
## Vedere anche  
 [Procedura: creare un servizio HTTP Web WCF](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md)   
 [Modello a oggetti per la programmazione HTTP Web di WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)