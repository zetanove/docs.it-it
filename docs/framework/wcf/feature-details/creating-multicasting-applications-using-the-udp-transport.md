---
title: "Creazione di applicazioni multicasting utilizzando il trasporto UDP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7485154a-6e85-4a67-a9d4-9008e741d4df
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Creazione di applicazioni multicasting utilizzando il trasporto UDP
Le applicazioni multicasting inviano piccoli messaggi a numerosi destinatari contemporaneamente senza la necessità di definire connessioni punto a punto.In queste applicazioni viene data più importanza alla velocità che all'affidabilità.In altre parole, è più importante inviare dati in modo tempestivo che garantire che qualsiasi messaggio specifico venga effettivamente ricevuto.WCF ora supporta la scrittura di applicazioni multicasting tramite l'oggetto <xref:System.ServiceModel.UdpBinding>.Questo trasporto è utile negli scenari in cui un servizio deve spedire contemporaneamente piccoli messaggi a una serie di client.Un'applicazione di codici di titoli è un esempio di questo servizio.  
  
## Implementazione di un'applicazione multicast  
 Per implementare un'applicazione multicast, definire un contratto di servizio e per ogni componente software che deve rispondere ai messaggi multicast, implementare il contratto di servizio.Ad esempio, un'applicazione di codici di titoli potrebbe definire un contratto di servizio:  
  
```  
// Shared contracts between the client and the service  
    [ServiceContract]  
    interface IStockTicker  
    {  
        [OperationContract(IsOneWay = true)]  
        void SendStockInfo(StockInfo[] stockInfo);  
    }  
  
    [DataContract]  
    class StockInfo  
    {  
        [DataMember]  
        public string Symbol;  
  
        [DataMember]  
        public float Price;  
  
        public StockInfo(string symbol, float price)  
        {  
            this.Symbol = symbol;  
            this.Price = price;  
        }  
    }  
  
```  
  
 Ogni applicazione che desidera ricevere messaggi multicast deve ospitare un servizio che espone l'interfaccia.Ad esempio, di seguito è riportato un esempio di codice che illustra come ricevere messaggi multicast:  
  
```  
// Service Address  
            string serviceAddress = "soap.udp://224.0.0.1:40000";  
            // Binding  
            UdpBinding myBinding = new UdpBinding();  
            // Host  
            ServiceHost host = new ServiceHost(typeof  
                (StockTickerService), new Uri(serviceAddress));  
            // Add service endpoint  
            host.AddServiceEndpoint(typeof(IStockTicker), myBinding, string.Empty);  
            // Openup the service host  
            host.Open();  
  
            Console.WriteLine("Start receiving stock information");  
            Console.ReadLine();  
  
```  
  
 L'applicazione specifica un indirizzo UDP in cui tutti i servizi saranno in ascolto.Viene creato un nuovo oggetto <xref:System.ServiceModel.ServiceHost> e tramite l'oggetto <xref:System.ServiceModel.UdpBinding> viene esposto un endpoint del servizio.L'oggetto <xref:System.ServiceModel.ServiceHost> viene quindi aperto e verrà avviato l'ascolto di messaggi in ingresso.  
  
 In questo tipo di scenario è il client che invia effettivamente i messaggi multicast.Ogni servizio che è in ascolto nell'indirizzo UDP corretto riceverà i messaggi multicast.Di seguito è riportato un esempio di un client che invia messaggi multicast:  
  
```  
// Multicast Address  
            string serviceAddress = "soap.udp://224.0.0.1:40000";  
  
            // Binding  
            UdpBinding myBinding = new UdpBinding();  
  
            // Channel factory  
            ChannelFactory<IStockTicker> factory  
                = new ChannelFactory<IStockTicker>(myBinding,  
                            new EndpointAddress(serviceAddress));  
  
            // Call service  
            IStockTicker proxy = factory.CreateChannel();  
  
            while (true)  
            {  
                // This will continue to mulicast stock information   
                proxy.SendStockInfo(GetStockInfo());  
                Console.WriteLine(String.Format("sent stock info at {0}", DateTime.Now));  
                // Wait for one second before sending another update  
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 1));  
            }  
  
```  
  
 Questo codice genera informazioni azionarie e, successivamente, utilizza il contratto di servizio IStockTicker per inviare messaggi multicast ai servizi di chiamata in ascolto nell'indirizzo UDP corretto.  
  
### UDP e messaggistica affidabile  
 L'associazione UDP non supporta la messaggistica affidabile a causa della semplicità del protocollo UDP.Se è necessario verificare che i messaggi vengano ricevuti da un endpoint remoto, utilizzare un trasporto che supporta la messaggistica affidabile come HTTP o TCP.Per ulteriori informazioni sulla messaggistica affidabile, vedere http:\/\/go.microsoft.com\/fwlink\/?LinkId\=231830  
  
### Messaggistica multicast bidirezionale  
 Mentre i messaggi multicast sono generalmente unidirezionali, UdpBinding supporta lo scambio di messaggi di richiesta\/risposta.I messaggi inviati tramite il trasporto UDP contengono sia un indirizzo del mittente sia del destinatario.È necessario prestare attenzione quando si utilizza l'indirizzo del mittente poiché potrebbe essere modificato in modo dannoso durante il trasferimento.L'indirizzo può essere controllato utilizzando il codice seguente:  
  
```  
if (address.AddressFamily == AddressFamily.InterNetwork)  
          {  
              // IPv4  
              byte[] addressBytes = address.GetAddressBytes();  
              return ((addressBytes[0] & 0xE0) == 0xE0);  
          }  
          else  
          {  
              // IPv6   
              return address.IsIPv6Multicast;  
          }  
  
```  
  
 Questo codice controlla il primo byte dell'indirizzo del mittente per verificare se contiene 0xE0, cioè se si tratta di un indirizzo multicast.  
  
### Considerazioni sulla sicurezza  
 Se si è in ascolto di messaggi multicast, un pacchetto ICMP viene inviato al router per notificare che l'utente è in ascolto nell'indirizzo multicast.Chiunque nella subnet locale che dispone delle autorizzazioni può essere in ascolto di questi tipi di pacchetti e determinare l'indirizzo multicast e la porta in cui si è in ascolto.  
  
 Non utilizzare l'indirizzo IP del mittente per nessun fine di sicurezza.Queste informazioni possono essere sottoposte a spoofing e possono causare l'invio di risposte al computer sbagliato da parte di un'applicazione.Un modo per limitare questa minaccia consiste nell'abilitare la sicurezza a livello di messaggio.A livello di rete, è possibile utilizzare anche IPSec \(Internet Protocol Security\) e\/o la Protezione accesso alla rete.