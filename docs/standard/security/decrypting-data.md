---
title: "Decrypting Data | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "data [.NET Framework], decryption"
  - "symmetric decryption"
  - "asymmetric decryption"
  - "decryption"
ms.assetid: 9b266b6c-a9b2-4d20-afd8-b3a0d8fd48a0
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# Decrypting Data
La decrittografia è l'inverso della crittografia. Per la crittografia a chiave privata è necessario conoscere sia la chiave che il valore di inizializzazione usati per crittografare i dati. Per la crittografia a chiave pubblica, è necessario conoscere sia la chiave pubblica \(se i dati sono stati crittografati mediante la chiave privata\) che la chiave privata \(se i dati sono stati crittografati mediante la chiave pubblica\).  
  
## Decrittografia simmetrica  
 La decrittografia dei dati crittografati con gli algoritmi simmetrici è simile al processo usato per crittografare i dati con algoritmi simmetrici. La classe <xref:System.Security.Cryptography.CryptoStream> viene usata con le classi di crittografia simmetrica fornite da .NET Framework per decrittografare i dati letti da qualsiasi oggetto flusso gestito.  
  
 L'esempio seguente illustra come creare una nuova istanza della classe <xref:System.Security.Cryptography.RijndaelManaged> e usarla per eseguire la decrittografia su un oggetto <xref:System.Security.Cryptography.CryptoStream>. Questo esempio crea prima di tutto una nuova istanza della classe **RijndaelManaged**. Crea quindi un oggetto **CryptoStream** e lo inizializza sul valore di un flusso gestito denominato `MyStream`. Al metodo **CreateDecryptor** della classe **RijndaelManaged** vengono quindi passati la stessa chiave e lo stesso valore di inizializzazione usati per la crittografia e il metodo viene quindi passato al costruttore **CryptoStream**. L'enumerazione **CryptoStreamMode.Read** viene infine passata al costruttore **CryptoStream** per specificare l'accesso in lettura al flusso.  
  
```vb  
Dim RMCrypto As New RijndaelManaged() Dim CryptStream As New CryptoStream(MyStream, RMCrypto.CreateDecryptor(RMCrypto.Key, RMCrypto.IV), CryptoStreamMode.Read)  
  
```  
  
```csharp  
RijndaelManaged RMCrypto = new RijndaelManaged(); CryptoStream CryptStream = new CryptoStream(MyStream, RMCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read);  
```  
  
 L'esempio seguente illustra l'intero processo di creazione di un flusso, decrittografia del flusso, lettura dal flusso e chiusura dei flussi. Viene creato un oggetto <xref:System.Net.Sockets.TcpListener> che inizializza un flusso di rete quando viene stabilita una connessione all'oggetto in ascolto. Il flusso di rete viene quindi decrittografato mediante la classe **CryptoStream** e la classe **RijndaelManaged**. Questo esempio presuppone che il valore della chiave e il valore di inizializzazione siano stati trasferiti correttamente o siano stati concordati in precedenza. Non mostra il codice necessario per crittografare e trasferire questi valori.  
  
```vb  
Imports System Imports System.Net.Sockets Imports System.Threading Imports System.IO Imports System.Net Imports System.Security.Cryptography Module Module1 Sub Main() 'The key and IV must be the same values that were used 'to encrypt the stream. Dim Key As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16} Dim IV As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16} Try 'Initialize a TCPListener on port 11000 'using the current IP address. Dim TCPListen As New TcpListener(IPAddress.Any, 11000) 'Start the listener. TCPListen.Start() 'Check for a connection every five seconds. While Not TCPListen.Pending() Console.WriteLine("Still listening. Will try in 5 seconds.") Thread.Sleep(5000) End While 'Accept the client if one is found. Dim TCP As TcpClient = TCPListen.AcceptTcpClient() 'Create a network stream from the connection. Dim NetStream As NetworkStream = TCP.GetStream() 'Create a new instance of the RijndaelManaged class 'and decrypt the stream. Dim RMCrypto As New RijndaelManaged() 'Create an instance of the CryptoStream class, pass it the NetworkStream, and decrypt 'it with the Rijndael class using the key and IV. Dim CryptStream As New CryptoStream(NetStream, RMCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read) 'Read the stream. Dim SReader As New StreamReader(CryptStream) 'Display the message. Console.WriteLine("The decrypted original message: {0}", SReader.ReadToEnd()) 'Close the streams. SReader.Close() NetStream.Close() TCP.Close() 'Catch any exceptions. Catch Console.WriteLine("The Listener Failed.") End Try End Sub End Module  
  
```  
  
```csharp  
using System; using System.Net.Sockets; using System.Threading; using System.IO; using System.Net; using System.Security.Cryptography; class Class1 { static void Main(string[] args) { //The key and IV must be the same values that were used //to encrypt the stream. byte[] Key = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16}; byte[] IV = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16}; try { //Initialize a TCPListener on port 11000 //using the current IP address. TcpListener TCPListen = new TcpListener(IPAdress.Any, 11000); //Start the listener. TCPListen.Start(); //Check for a connection every five seconds. while(!TCPListen.Pending()) { Console.WriteLine("Still listening. Will try in 5 seconds."); Thread.Sleep(5000); } //Accept the client if one is found. TcpClient TCP = TCPListen.AcceptTcpClient(); //Create a network stream from the connection. NetworkStream NetStream = TCP.GetStream(); //Create a new instance of the RijndaelManaged class // and decrypt the stream. RijndaelManaged RMCrypto = new RijndaelManaged(); //Create a CryptoStream, pass it the NetworkStream, and decrypt //it with the Rijndael class using the key and IV. CryptoStream CryptStream = new CryptoStream(NetStream, RMCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read); //Read the stream. StreamReader SReader = new StreamReader(CryptStream); //Display the message. Console.WriteLine("The decrypted original message: {0}", SReader.ReadToEnd()); //Close the streams. SReader.Close(); NetStream.Close(); TCP.Close(); } //Catch any exceptions. catch { Console.WriteLine("The Listener Failed."); } } }  
```  
  
 Per permettere il funzionamento dell'esempio precedente, è necessario stabilire una connessione crittografata con il listener. La connessione deve usare la stessa chiave, lo stesso valore di inizializzazione e lo stesso algoritmo usati nel listener. Se si stabilisce la connessione, il messaggio verrà crittografato e visualizzato nella console.  
  
## Decrittografia asimmetrica  
 In genere, una parte \(parte A\) genera la sia la chiave pubblica che quella privata e archivia la chiave in memoria o in un contenitore di chiavi crittografiche.  La parte A invia quindi la chiave pubblica a un'altra parte \(parte B\).  Usando la chiave pubblica, tramite la parte B i dati vengono crittografati e inviati alla parte A. Dopo la ricezione, i dati vengono decrittografati dalla parte A mediante la chiave privata corrispondente.  La decrittografia avrà esito positivo solo se la parte A usa la chiave privata corrispondente alla chiave pubblica usata dalla parte B per crittografare i dati.  
  
 Per informazioni su come archiviare una chiave asimmetrica in un contenitore protetto di chiavi crittografiche e su come recuperare in seguito la chiave asimmetrica, vedere [How to: Store Asymmetric Keys in a Key Container](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md).  
  
 L'esempio seguente illustra la decrittografia di due matrici di byte che rappresentano una chiave simmetrica e il valore di inizializzazione.  Per informazioni su come estrarre la chiave pubblica simmetrica dall'oggetto <xref:System.Security.Cryptography.RSACryptoServiceProvider> in un formato facilmente inviabile a terze parti, vedere [Encrypting Data](../../../docs/standard/security/encrypting-data.md).  
  
```vb  
'Create a new instance of the RSACryptoServiceProvider class. Dim RSA As New RSACryptoServiceProvider() ' Export the public key information and send it to a third party. ' Wait for the third party to encrypt some data and send it back. 'Decrypt the symmetric key and IV. SymmetricKey = RSA.Decrypt(EncryptedSymmetricKey, False) SymmetricIV = RSA.Decrypt(EncryptedSymmetricIV, False)  
  
```  
  
```csharp  
//Create a new instance of the RSACryptoServiceProvider class. RSACryptoServiceProvider RSA = new RSACryptoServiceProvider(); // Export the public key information and send it to a third party. // Wait for the third party to encrypt some data and send it back. //Decrypt the symmetric key and IV. SymmetricKey = RSA.Decrypt( EncryptedSymmetricKey, false); SymmetricIV = RSA.Decrypt( EncryptedSymmetricIV , false);  
```  
  
## Vedere anche  
 [Generating Keys for Encryption and Decryption](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)   
 [Encrypting Data](../../../docs/standard/security/encrypting-data.md)   
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)