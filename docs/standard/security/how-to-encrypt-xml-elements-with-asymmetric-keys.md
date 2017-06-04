---
title: "How to: Encrypt XML Elements with Asymmetric Keys | Microsoft Docs"
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
  - "cryptography [.NET Framework], asymmetric keys"
  - "AES algorithm"
  - "System.Security.Cryptography.RSACryptoServiceProvider class"
  - "asymmetric keys [.NET Framework]"
  - "System.Security.Cryptography.EncryptedXml class"
  - "XML encryption"
  - "key containers"
  - "Advanced Encryption Standard algorithm"
  - "Rijndael"
  - "encryption [.NET Framework], asymmetric keys"
ms.assetid: a164ba4f-e596-4bbe-a9ca-f214fe89ed48
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Encrypt XML Elements with Asymmetric Keys
È possibile usare le classi dello spazio dei nomi <xref:System.Security.Cryptography.Xml> per crittografare un elemento all'interno di un documento XML.  La crittografia XML consente di scambiare o archiviare dati XML crittografati in modo standard, garantendo un'adeguata protezione dei dati da letture non autorizzate.  Per altre informazioni sullo standard di crittografia XML, vedere la specifica World Wide Web Consortium \(W3C\) per la crittografia XML disponibile all'indirizzo http:\/\/www.w3.org\/TR\/xmldsig\-core\/.  
  
 È possibile usare la crittografia XML per sostituire qualsiasi elemento o documento XML con un elemento \<`EncryptedData`\> contenente i dati XML crittografati.  Nell'elemento \<`EncryptedData`\> possono essere inclusi anche sottoelementi in cui sono incluse informazioni sulle chiavi e sui processi usati durante la crittografia.  La crittografia XML consente a un documento di contenere più elementi crittografati e consente a un elemento di essere crittografato più volte.  Nell'esempio di codice relativo a questa procedura viene illustrato come creare un elemento \<`EncryptedData`\> insieme a diversi altri sottoelementi utilizzabili in un secondo momento durante la decrittografia.  
  
 Questo esempio crittografa un elemento XML mediante due chiavi.  L'esempio genera una coppia di chiavi pubblica\/privata RSA e salva la coppia di chiavi in un contenitore di chiavi protetto.  L'esempio crea quindi una chiave di sessione separata usando l'algoritmo AES \(Advanced Encryption Standard\), definito anche algoritmo Rijndael.  La chiave di sessione AES viene usata dall'esempio per crittografare il documento XML e la chiave pubblica RSA viene usata per crittografare la chiave di sessione AES.  L'esempio salva infine la chiave di sessione AES crittografata e i dati XML crittografati nel documento XML entro un nuovo elemento \<`EncryptedData`\>.  
  
 Per decrittografare l'elemento XML, recuperare la chiave privata RSA dal contenitore di chiavi, usarla per decrittografare la chiave di sessione e quindi usare la chiave di sessione per decrittografare il documento.  Per altre informazioni su come decrittografare un elemento XML che era stato crittografato mediante questa procedura, vedere [How to: Decrypt XML Elements with Asymmetric Keys](../../../docs/standard/security/how-to-decrypt-xml-elements-with-asymmetric-keys.md).  
  
 Questo esempio è adatto per situazioni in cui più applicazioni devono condividere dati crittografati o in cui un'applicazione deve salvare dati crittografati tra un'esecuzione e l'altra.  
  
### Per crittografare un elemento XML con una chiave asimmetrica  
  
1.  Creare un oggetto <xref:System.Security.Cryptography.CspParameters> e specificare il nome del contenitore di chiavi.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2.  Generare una chiave simmetrica usando la classe <xref:System.Security.Cryptography.RSACryptoServiceProvider>.  La chiave viene salvata automaticamente nel contenitore di chiavi quando si passa l'oggetto <xref:System.Security.Cryptography.CspParameters> al costruttore della classe <xref:System.Security.Cryptography.RSACryptoServiceProvider>.  Questa chiave verrà usata per crittografare la chiave di sessione AES e può essere recuperata in un secondo momento per decrittografarla.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3.  Creare un oggetto <xref:System.Xml.XmlDocument> caricando un file XML dal disco.  L'oggetto <xref:System.Xml.XmlDocument> contiene l'elemento XML da crittografare.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#4)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#4)]  
  
4.  Individuare l'elemento specificato nell'oggetto <xref:System.Xml.XmlDocument> e creare un nuovo oggetto <xref:System.Xml.XmlElement> per rappresentare l'elemento che si vuole crittografare.  In questo esempio l'elemento `"creditcard"` è crittografato.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
5.  Creare una nuova chiave di sessione usando la classe <xref:System.Security.Cryptography.RijndaelManaged>.  Questa chiave crittograferà l'elemento XML e quindi verrà crittografata a sua volta e inserita nel documento XML.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
6.  Creare una nuova istanza della classe <xref:System.Security.Cryptography.Xml.EncryptedXml> e usarla per crittografare l'elemento specificato mediante la chiave di sessione.  Il metodo <xref:System.Security.Cryptography.Xml.EncryptedXml.EncryptData%2A> restituisce l'elemento crittografato come una matrice di byte crittografati.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
7.  Costruire un oggetto <xref:System.Security.Cryptography.Xml.EncryptedData> e popolarlo con l'identificatore dell'URL dell'elemento XML crittografato.  Questo identificatore dell'URL comunica a chi esegue la decrittografia che l'elemento XML contiene un elemento crittografato.  È possibile usare il campo <xref:System.Security.Cryptography.Xml.EncryptedXml.XmlEncElementUrl> per specificare l'identificatore dell'URL.  L'elemento XML in testo non crittografato verrà sostituito da un elemento \<`EncryptedData`\> incapsulato da questo oggetto <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
8.  Creare un oggetto <xref:System.Security.Cryptography.Xml.EncryptionMethod> inizializzato sull'identificatore dell'URL dell'algoritmo di crittografia usato per generare la chiave di sessione.  Passare l'oggetto <xref:System.Security.Cryptography.Xml.EncryptionMethod> alla proprietà <xref:System.Security.Cryptography.Xml.EncryptedType.EncryptionMethod%2A>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#9)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#9)]  
  
9. Creare un oggetto <xref:System.Security.Cryptography.Xml.EncryptedKey> in cui includere la chiave di sessione crittografata.  Crittografare la chiave di sessione, aggiungerla all'oggetto <xref:System.Security.Cryptography.Xml.EncryptedKey> e immettere un nome di chiave di sessione e l'URL dell'identificatore della chiave.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#10)]  
  
10. Creare un nuovo oggetto <xref:System.Security.Cryptography.Xml.DataReference> che esegue il mapping dei dati crittografati a una chiave di sessione specifica.  Questo passaggio facoltativo permette di specificare con facilità che più parti di un documento XML sono state crittografate da una singola chiave.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#11)]  
  
11. Aggiungere la chiave crittografata all'oggetto <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#12)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#12)]  
  
12. Creare un nuovo oggetto <xref:System.Security.Cryptography.Xml.KeyInfo> per specificare il nome della chiave RSA.  Aggiungerlo all'oggetto <xref:System.Security.Cryptography.Xml.EncryptedData>.  Ciò permette a chi esegue la crittografia di identificare la chiave asimmetrica corretta da usare per decrittografare la chiave di sessione.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#13)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#13)]  
  
13. Aggiungere i dati dell'elemento crittografato all'oggetto <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#14)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#14)]  
  
14. Sostituire l'elemento dall'oggetto <xref:System.Xml.XmlDocument> originale con l'elemento <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#15)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#15)]  
  
15. Salvare l'oggetto <xref:System.Xml.XmlDocument>.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#16)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#16)]  
  
## Esempio  
 Questo esempio presuppone che sia presente un file denominato `"test.xml"` nella stessa directory del programma compilato  e che `"test.xml"` contenga un elemento `"creditcard"`.  È possibile inserire il codice XML seguente in un file denominato `test.xml` e usarlo con questo esempio.  
  
```  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
  
```  
  
 [!code-csharp[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## Compilazione del codice  
  
-   Per compilare questo esempio, è necessario includere un riferimento a `System.Security.dll`.  
  
-   Includere gli spazi dei nomi seguenti: <xref:System.Xml>, <xref:System.Security.Cryptography> e <xref:System.Security.Cryptography.Xml>.  
  
## Sicurezza di .NET Framework  
 Non archiviare mai una chiave crittografica in testo non crittografato e non trasferire mai in testo non crittografato una chiave simmetrica tra computer.  Non archiviare né trasferire mai in testo non crittografato, inoltre, la chiave privata di una coppia di chiavi asimmetriche.  Per altre informazioni sulle chiavi crittografiche simmetriche e asimmetriche, vedere [Generating Keys for Encryption and Decryption](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md).  
  
 Non incorporare mai una chiave direttamente nel codice sorgente.  Le chiavi incorporate possono essere lette facilmente da un assembly mediante [Ildasm.exe \(IL Disassembler\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) oppure aprendo l'assembly in un editor di testo quale Blocco note.  
  
 Dopo avere usato una chiave crittografica, cancellarla dalla memoria impostando ogni byte su zero oppure chiamando il metodo <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> della classe di crittografia gestita.  Le chiavi crittografiche possono essere a volte lette dalla memoria da un debugger oppure possono essere lette da un disco rigido, se viene eseguito il paging su disco della posizione di memoria.  
  
## Vedere anche  
 <xref:System.Security.Cryptography.Xml>   
 [How to: Decrypt XML Elements with Asymmetric Keys](../../../docs/standard/security/how-to-decrypt-xml-elements-with-asymmetric-keys.md)