---
title: "How to: Decrypt XML Elements with Asymmetric Keys | Microsoft Docs"
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
  - "System.Security.Cryptography.RSACryptoServiceProvider class"
  - "asymmetric keys"
  - "System.Security.Cryptography.EncryptedXml class"
  - "XML encryption"
  - "decryption"
ms.assetid: dd5de491-dafe-4b94-966d-99714b2e754a
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# How to: Decrypt XML Elements with Asymmetric Keys
È possibile usare le classi dello spazio dei nomi <xref:System.Security.Cryptography.Xml> per crittografare e decrittografare un elemento all'interno di un documento XML.  La crittografia XML consente di scambiare o archiviare dati XML crittografati in modo standard, garantendo un'adeguata protezione dei dati da letture non autorizzate.  Per altre informazioni sullo standard di crittografia XML, vedere la raccomandazione del World Wide Web Consortium \(W3C\) relativa all'[elaborazione e alla sintassi della firma XML](http://go.microsoft.com/fwlink/?LinkID=136777).  
  
 L'esempio in questa procedura decrittografa un elemento XML crittografato mediante i metodi illustrati in [How to: Encrypt XML Elements with Asymmetric Keys](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md).  Trova un elemento \<`EncryptedData`\>, lo decrittografa e quindi lo sostituisce con l'elemento XML originale in testo non crittografato.  
  
 Questo esempio decrittografa un elemento XML mediante due chiavi.  Recupera una chiave privata RSA generata in precedenza da un contenitore di chiavi e quindi usa la chiave RSA per decrittografare una chiave di sessione archiviata nell'elemento \<`EncryptedKey`\> dell'elemento \<`EncryptedData`\>.  L'esempio usa quindi la chiave di sessione per decrittografare l'elemento XML.  
  
 Questo esempio è adatto per situazioni in cui più applicazioni devono condividere dati crittografati o in cui un'applicazione deve salvare dati crittografati tra un'esecuzione e l'altra.  
  
### Per decrittografare un elemento XML con una chiave asimmetrica  
  
1.  Creare un oggetto <xref:System.Security.Cryptography.CspParameters> e specificare il nome del contenitore di chiavi.  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2.  Recuperare una chiave asimmetrica generata in precedenza dal contenitore usando l'oggetto <xref:System.Security.Cryptography.RSACryptoServiceProvider>.  La chiave viene recuperata automaticamente dal contenitore di chiavi quando si passa l'oggetto <xref:System.Security.Cryptography.CspParameters> al costruttore <xref:System.Security.Cryptography.RSACryptoServiceProvider>.  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3.  Creare un nuovo oggetto <xref:System.Security.Cryptography.Xml.EncryptedXml> per decrittografare il documento.  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
4.  Aggiungere un mapping di chiave\/nome per associare la chiave RSA all'elemento entro il documento da decrittografare.  È necessario usare per la chiave lo stesso nome specificato durante la crittografia del documento.  Si noti che questo nome è distinto dal nome usato per identificare la chiave nel contenitore di chiavi specificato nel passaggio 1.  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
5.  Chiamare il metodo <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> per decrittografare l'elemento \<`EncryptedData`\>.  Questo metodo usa la chiave RSA per decrittografare la chiave di sessione e usa automaticamente la chiave di sessione per decrittografare l'elemento XML.  Sostituisce anche automaticamente l'elemento \<`EncryptedData`\> con il testo non crittografato originale.  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
6.  Salvare il documento XML.  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
## Esempio  
 Questo esempio presuppone che sia presente un file denominato `test.xml` nella stessa directory del programma compilato.  e che `test.xml` contenga un elemento XML crittografato usando le tecniche descritte in [How to: Encrypt XML Elements with Asymmetric Keys](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md).  
  
 [!code-csharp[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## Compilazione del codice  
  
-   Per compilare questo esempio, è necessario includere un riferimento a `System.Security.dll`.  
  
-   Includere gli spazi dei nomi seguenti: <xref:System.Xml>, <xref:System.Security.Cryptography> e <xref:System.Security.Cryptography.Xml>.  
  
## Sicurezza di .NET Framework  
 Non archiviare mai una chiave crittografica in testo non crittografato e non trasferire mai in testo non crittografato una chiave simmetrica tra computer.  Non archiviare né trasferire mai in testo non crittografato, inoltre, la chiave privata di una coppia di chiavi asimmetriche.  Per altre informazioni sulle chiavi crittografiche simmetriche e asimmetriche, vedere [Generating Keys for Encryption and Decryption](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md).  
  
 Non incorporare mai una chiave direttamente nel codice sorgente.  Le chiavi incorporate possono essere lette facilmente da un assembly mediante [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) oppure aprendo l'assembly in un editor di testo quale Blocco note.  
  
 Dopo avere usato una chiave crittografica, cancellarla dalla memoria impostando ogni byte su zero oppure chiamando il metodo <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> della classe di crittografia gestita.  Le chiavi crittografiche possono essere a volte lette dalla memoria da un debugger oppure possono essere lette da un disco rigido, se viene eseguito il paging su disco della posizione di memoria.  
  
## Vedere anche  
 <xref:System.Security.Cryptography.Xml>   
 [How to: Encrypt XML Elements with Asymmetric Keys](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md)