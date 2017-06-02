---
title: "Uso dei servizi UDP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "protocolli, UDP"
  - "risorse di rete, UDP"
  - "richiesta di dati da Internet, UDP"
  - "UDP"
  - "ricezione di dati, UDP"
  - "Internet, UDP"
  - "trasmissione i messaggi a più messaggi"
  - "richiesta di dati, UDP"
  - "UdpClient (classe), informazioni"
  - "invio di dati, UDP"
  - "protocolli applicativi, UDP"
ms.assetid: d5c3477a-e798-454c-a890-738ba14c5707
caps.latest.revision: 15
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Uso dei servizi UDP
La classe <xref:System.Net.Sockets.UdpClient> comunica con i servizi di rete mediante UDP.  Le proprietà e i metodi <xref:System.Net.Sockets.UdpClient> funzioni abstract i dettagli di creare <xref:System.Net.Sockets.Socket> per la richiesta e la ricezione dei dati mediante UDP.  
  
 Il User Datagram Protocol \(UDP\) è un semplice protocollo che esegue il modo richiesto per fornire dati a un host remoto.  Tuttavia, poiché il protocollo di UDP è un protocollo privo di connessione, i datagrams di UDP inviati all'endpoint remoto non sono garantiti per arrivare, né sono è garantito che conduca nella stessa sequenza in cui vengono inviati.  Le applicazioni che utilizzano UDP devono essere preparato per gestire correttamente, duplicare e i datagrams di fuori sequenza.  
  
 Per inviare un datagram mediante UDP, è necessario conoscere l'indirizzo di rete di dispositivo di rete che ospita il servizio necessari e il numero di porta UDP del servizio viene utilizzato per comunicare.  Internet Assigned Numbers AUTHORITY \(Iana\) definisce i numeri di porta per i servizi comuni \(vedere www.iana.org\/assignments\/port\-numbers\).  I servizi non l'elenco di IANA possono includere numeri di porta compreso tra 1.024 e 65.535.  
  
 Gli indirizzi di rete speciali utilizzati per supportare i messaggi trasmessi di UDP alle reti basate su IP.  La discussione seguente viene utilizzata la famiglia degli indirizzi della versione 4 di indirizzi Internet utilizzata come esempio.  
  
 Gli indirizzi della versione 4 di IP utilizzano 32 bit per specificare un indirizzo di rete.  Per gli indirizzi C della classe utilizzando un netmask di 255.255.255.0, questi bit sono suddivisi in quattro ottetti.  Una volta espressi in formato decimale, i quattro ottetti costituiscono la notazione puntata comune, ad esempio 192.168.100.2.  I primi due ottetti \(192,168 in questo esempio\) costituiscono il network number, il terzo ottetto \(100\) definisce ip\/subnet e di ottetto finale \(2\) rappresenta l'identificatore host.  
  
 Impostando tutti i bit di un indirizzo IP a uno, o 255.255.255.255 form, l'indirizzo broadcast limitato.  Inviando un datagram di UDP a questo indirizzo consegna il messaggio a qualsiasi host del segmento di rete locale.  Poiché i messaggi non vengano inviati a questo indirizzo, solo router host del segmento di rete riceve il messaggio in tempo reale.  
  
 Che trasmette possono essere indirizzate a parti specifiche di rete impostando tutti i bit dell'identificatore host.  Ad esempio, per inviare una trasmissione a tutti gli host in rete identificata dagli indirizzi IP che iniziano con 192.168.1, utilizzare l'indirizzo 192.168.1.255.  
  
 Nell'esempio di codice riportato <xref:System.Net.Sockets.UdpClient> per l'ascolto dei datagrams di UDP inviati all'indirizzo broadcast diretto 192.168.1.255 sulla porta 11.000.  Il client riceve una stringa di messaggio e scrivere il messaggio nella console.  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Net.Sockets  
Imports System.Text  
  
Public Class UDPListener  
   Private Const listenPort As Integer = 11000  
  
   Private Shared Sub StartListener()  
      Dim done As Boolean = False  
      Dim listener As New UdpClient(listenPort)  
      Dim groupEP As New IPEndPoint(IPAddress.Any, listenPort)  
      Try  
         While Not done  
            Console.WriteLine("Waiting for broadcast")  
            Dim bytes As Byte() = listener.Receive(groupEP)  
            Console.WriteLine("Received broadcast from {0} :", _  
                groupEP.ToString())   
            Console.WriteLine( _  
                Encoding.ASCII.GetString(bytes, 0, bytes.Length))  
            Console.WriteLine()  
         End While  
      Catch e As Exception  
         Console.WriteLine(e.ToString())  
      Finally  
         listener.Close()  
      End Try  
   End Sub 'StartListener  
  
   Public Shared Function Main() As Integer  
      StartListener()  
      Return 0  
   End Function 'Main  
End Class 'UDPListener  
```  
  
```csharp  
using System;  
using System.Net;  
using System.Net.Sockets;  
using System.Text;  
  
public class UDPListener   
{  
    private const int listenPort = 11000;  
  
    private static void StartListener()   
    {  
        bool done = false;  
  
        UdpClient listener = new UdpClient(listenPort);  
        IPEndPoint groupEP = new IPEndPoint(IPAddress.Any,listenPort);  
  
        try   
        {  
            while (!done)   
            {  
                Console.WriteLine("Waiting for broadcast");  
                byte[] bytes = listener.Receive( ref groupEP);  
  
                Console.WriteLine("Received broadcast from {0} :\n {1}\n",  
                    groupEP.ToString(),  
                    Encoding.ASCII.GetString(bytes,0,bytes.Length));  
            }  
  
        }   
        catch (Exception e)   
        {  
            Console.WriteLine(e.ToString());  
        }  
        finally  
        {  
            listener.Close();  
        }  
    }  
  
    public static int Main()   
    {  
        StartListener();  
  
        return 0;  
    }  
}  
```  
  
 Nell'esempio di codice riportato <xref:System.Net.Sockets.UdpClient> per inviare i datagrams di UDP all'indirizzo broadcast diretto 192.168.1.255, l'utilizzo della porta 11.000.  Il client invia la stringa di messaggio specificata nella riga di comando.  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Net.Sockets  
Imports System.Text  
  
Public Class Program  
  
    Overloads Public Shared Function Main(args() As [String]) As Integer  
      Dim s As New Socket(AddressFamily.InterNetwork, SocketType.Dgram,  
          ProtocolType.Udp)  
      Dim broadcast As IPAddress = IPAddress.Parse("192.168.1.255")  
      Dim sendbuf As Byte() = Encoding.ASCII.GetBytes(args(0))  
      Dim ep As New IPEndPoint(broadcast, 11000)  
      s.SendTo(sendbuf, ep)  
      Console.WriteLine("Message sent to the broadcast address")  
   End Function 'Main  
End Class   
```  
  
```csharp  
using System;  
using System.Net;  
using System.Net.Sockets;  
using System.Text;  
  
class Program   
{  
    static void Main(string[] args)   
    {  
        Socket s = new Socket(AddressFamily.InterNetwork, SocketType.Dgram,  
            ProtocolType.Udp);  
  
        IPAddress broadcast = IPAddress.Parse("192.168.1.255");  
  
        byte[] sendbuf = Encoding.ASCII.GetBytes(args[0]);  
        IPEndPoint ep = new IPEndPoint(broadcast, 11000);  
  
        s.SendTo(sendbuf, ep);  
  
        Console.WriteLine("Message sent to the broadcast address");  
    }  
}  
```  
  
## Vedere anche  
 <xref:System.Net.Sockets.UdpClient>   
 <xref:System.Net.IPAddress>   
 [TCP\/UDP](../../../docs/framework/network-programming/tcp-udp.md)