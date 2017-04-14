---
title: "Generating Keys for Encryption and Decryption | Microsoft Docs"
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
  - "keys, encryption and decryption"
  - "keys, asymmetric"
  - "keys, symmetric"
  - "encryption [.NET Framework], keys"
  - "symmetric keys"
  - "asymmetric keys [.NET Framework]"
  - "cryptography [.NET Framework], keys"
ms.assetid: c197dfc9-a453-4226-898d-37a16638056e
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# Generating Keys for Encryption and Decryption
La creazione e la gestione di chiavi sono due momenti importanti del processo di crittografia. Per gli algoritmi simmetrici è richiesta la creazione di una chiave e un vettore di inizializzazione \(IV\). La chiave deve rimanere segreta per chiunque non debba decrittografare i dati. Il vettore di inizializzazione non deve rimanere segreto, ma dovrebbe essere modificato per ogni sessione. Gli algoritmi asimmetrici richiedono la creazione di una chiave pubblica e di una chiave privata. La chiave pubblica può essere resa pubblica a chiunque, mentre quella privata deve essere nota solo alla parte che decrittograferà i dati crittografati con la chiave pubblica. Questa sezione descrive come generare e gestire chiavi sia per gli algoritmi simmetrici che per quelli asimmetrici.  
  
## Chiavi simmetriche  
 Le classi di crittografia simmetrica disponibili in .NET Framework richiedono una chiave e un nuovo vettore di inizializzazione \(IV, Initialization Vector\) per crittografare e decrittografare i dati. Ogni volta che si crea una nuova istanza di una delle classi di crittografia simmetrica gestite con il costruttore predefinito, vengono automaticamente creati una chiave e un vettore di inizializzazione nuovi. Per riuscire a decrittografare i dati, i destinatari devono avere la stessa chiave e lo stesso vettore di inizializzazione e devono usare il medesimo algoritmo di crittografia. Generalmente è necessario creare una chiave e un vettore di inizializzazione nuovi per ogni sessione e né la chiave né il vettore devono essere archiviati per un uso in una sessione successiva.  
  
 Per comunicare una chiave simmetrica e un vettore di inizializzazione a una parte remota, la chiave simmetrica viene generalmente crittografata mediante la crittografia asimmetrica. L'invio della chiave in una rete non protetta senza crittografarla non è sicuro, poiché chiunque intercetti la chiave e il vettore di inizializzazione è in grado di decrittografare i dati. Per ulteriori informazioni sullo scambio di dati utilizzando la crittografia, vedere [Creare uno schema di crittografia](../../../docs/standard/security/creating-a-cryptographic-scheme.md).  
  
 L'esempio seguente illustra la creazione di una nuova istanza della classe <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider> che implementa l'algoritmo TripleDES.  
  
```vb  
Dim TDES As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider()  
  
```  
  
```csharp  
TripleDESCryptoServiceProvider TDES = new TripleDESCryptoServiceProvider();  
```  
  
 Quando viene eseguito il codice precedente, una chiave e un vettore di inizializzazione nuovi vengono generati e inseriti rispettivamente nelle proprietà **Key** e **IV**.  
  
 Talvolta può essere necessario generare più chiavi. In questa situazione è possibile creare una nuova istanza di una classe che implementa un algoritmo simmetrico e quindi creare una chiave e un vettore di inizializzazione nuovi chiamando i metodi **GenerateKey** e **GenerateIV**. L'esempio di codice seguente illustra come generare chiavi e vettori di inizializzazione nuovi dopo aver creato una nuova istanza della classe di crittografia asimmetrica.  
  
```vb  
Dim TDES As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider() TDES.GenerateIV() TDES.GenerateKey()  
  
```  
  
```csharp  
TripleDESCryptoServiceProvider TDES = new TripleDESCryptoServiceProvider(); TDES.GenerateIV(); TDES.GenerateKey();  
```  
  
 Quando viene eseguito il codice precedente, una chiave e un vettore di inizializzazione nuovi vengono generati quando viene creata la nuova istanza di **TripleDESCryptoServiceProvider**. Un'altra chiave e vettore di inizializzazione vengono creati quando vengono chiamati i metodi **GenerateKey** e **GenerateIV**.  
  
## Chiavi asimmetriche  
 In .NET Framework sono incluse le classi <xref:System.Security.Cryptography.RSACryptoServiceProvider> e <xref:System.Security.Cryptography.DSACryptoServiceProvider> per la crittografia asimmetrica. Queste classi creano una coppia di chiavi pubblica\/privata quando si usa il costruttore predefinito per creare una nuova istanza. Le chiavi asimmetriche possono essere archiviate per un uso in più sessioni o generate per una sola sessione. Mentre la chiave pubblica può essere generalmente resa disponibile, la chiave privata va custodita con cura.  
  
 Una coppia di chiavi pubblica\/privata viene generata ogni volta che viene creata una nuova istanza di una classe di algoritmo asimmetrico. Dopo che è stata creata una nuova istanza della classe, le informazioni sulla chiave possono essere estratte con uno dei metodi indicati di seguito:  
  
-   Il metodo <xref:System.Security.Cryptography.RSA.ToXmlString%2A>, che restituisce una rappresentazione XML delle informazioni sulla chiave.  
  
-   Il metodo <xref:System.Security.Cryptography.RSACryptoServiceProvider.ExportParameters%2A>, che restituisce una struttura <xref:System.Security.Cryptography.RSAParameters> contenente le informazioni sulla chiave.  
  
 Entrambi i metodi accettano un valore Boolean che indica se restituire solo le informazioni sulla chiave pubblica o le informazioni sia sulla chiave pubblica che sulla chiave privata. Una classe **RSACryptoServiceProvider** può essere inizializzata in base al valore di una struttura **RSAParameters** usando il metodo <xref:System.Security.Cryptography.RSACryptoServiceProvider.ImportParameters%2A>.  
  
 Le chiavi private asimmetriche non devono essere mai archiviate in modalità verbatim o in testo normale nel computer locale. Se è necessario archiviare una chiave privata, è opportuno usare un contenitore di chiavi. Per altre informazioni su come archiviare una chiave privata in un contenitore di chiavi, vedere [How to: Store Asymmetric Keys in a Key Container](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md).  
  
 L'esempio di codice seguente crea una nuova istanza della classe **RSACryptoServiceProvider**, che crea una coppia di chiavi pubblica\/privata e salva le informazioni sulla chiave pubblica in una struttura **RSAParameters**.  
  
```vb  
'Generate a public/private key pair. Dim RSA as RSACryptoServiceProvider = new RSACryptoServiceProvider() 'Save the public key information to an RSAParameters structure. Dim RSAKeyInfo As RSAParameters = RSA.ExportParameters(false)  
  
```  
  
```csharp  
//Generate a public/private key pair. RSACryptoServiceProvider RSA = new RSACryptoServiceProvider(); //Save the public key information to an RSAParameters structure. RSAParameters RSAKeyInfo = RSA.ExportParameters(false);  
```  
  
## Vedere anche  
 [Encrypting Data](../../../docs/standard/security/encrypting-data.md)   
 [Decrypting Data](../../../docs/standard/security/decrypting-data.md)   
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)   
 [How to: Store Asymmetric Keys in a Key Container](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md)