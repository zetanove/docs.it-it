---
title: "How to: Encrypt XML Elements with Symmetric Keys | Microsoft Docs"
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
  - "AES algorithm"
  - "cryptography [.NET Framework], symmetric keys"
  - "encryption [.NET Framework], symmetric keys"
  - "symmetric keys"
  - "System.Security.Cryptography.EncryptedXml class"
  - "System.Security.Cryptography.RijndaelManaged class"
  - "XML encryption"
  - "Advanced Encryption Standard algorithm"
  - "Rijndael"
ms.assetid: d8461a44-aa2c-4ef4-b3e4-ab7cbaaee1b5
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Encrypt XML Elements with Symmetric Keys
È possibile usare le classi dello spazio dei nomi <xref:System.Security.Cryptography.Xml> per crittografare un elemento all'interno di un documento XML.  La crittografia XML consente di archiviare o trasportare contenuti XML sensibili, senza preoccuparsi che i dati vengano letti con facilità.  Questa procedura consente di decrittografare un elemento XML usando l'algoritmo Advanced Encryption Standard \(AES\), noto anche come Rijndael.  
  
 Per altre informazioni su come decrittografare un elemento XML crittografato mediante questa procedura, vedere [How to: Decrypt XML Elements with Symmetric Keys](../../../docs/standard/security/how-to-decrypt-xml-elements-with-symmetric-keys.md).  
  
 Quando si usa un algoritmo simmetrico come AES per crittografare i dati XML, è necessario usare la stessa chiave per crittografare e decrittografare i dati XML.  L'esempio riportato in questa procedura presuppone che i dati XML crittografati verranno decrittografati mediante la stessa chiave e che le parti che eseguono le operazioni di crittografia e decrittografia si accordino sull'algoritmo e sulla chiave da usare.  L'esempio non archivia né crittografa la chiave AES nei dati XML crittografati.  
  
 Questo esempio è appropriato per situazioni in cui una singola applicazione deve crittografare i dati in base a una chiave della sessione archiviata in memoria o in base a una chiave di crittografia avanzata derivata da una password.  Per i casi in cui due o più applicazioni devono condividere dati XML crittografati, è consigliabile usare uno schema di crittografia basato su un algoritmo asimmetrico o un certificato X.509.  
  
### Per crittografare un elemento XML con una chiave simmetrica  
  
1.  Generare una chiave simmetrica usando la classe <xref:System.Security.Cryptography.RijndaelManaged>.  Questa chiave verrà usata per crittografare l'elemento XML.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#2)]
     [!code-vb[HowToEncryptXMLElementSymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#2)]  
  
2.  Creare un oggetto <xref:System.Xml.XmlDocument> caricando un file XML dal disco.  L'oggetto <xref:System.Xml.XmlDocument> contiene l'elemento XML da crittografare.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#3)]
     [!code-vb[HowToEncryptXMLElementSymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#3)]  
  
3.  Individuare l'elemento specificato nell'oggetto <xref:System.Xml.XmlDocument> e creare un nuovo oggetto <xref:System.Xml.XmlElement> per rappresentare l'elemento che si vuole crittografare.  In questo esempio l'elemento `"creditcard"` è crittografato.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#4)]
     [!code-vb[HowToEncryptXMLElementSymmetric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#4)]  
  
4.  Creare una nuova istanza della classe <xref:System.Security.Cryptography.Xml.EncryptedXml> e usarla per crittografare l'oggetto <xref:System.Xml.XmlElement> con la chiave simmetrica.  Il metodo <xref:System.Security.Cryptography.Xml.EncryptedXml.EncryptData%2A> restituisce l'elemento crittografato come una matrice di byte crittografati.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#5)]
     [!code-vb[HowToEncryptXMLElementSymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#5)]  
  
5.  Costruire un oggetto <xref:System.Security.Cryptography.Xml.EncryptedData> e popolarlo con l'identificatore dell'URL dell'elemento di crittografia XML.  Questo identificatore dell'URL comunica a chi esegue la decrittografia che l'elemento XML contiene un elemento crittografato.  È possibile usare il campo <xref:System.Security.Cryptography.Xml.EncryptedXml.XmlEncElementUrl> per specificare l'identificatore dell'URL.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#6)]
     [!code-vb[HowToEncryptXMLElementSymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#6)]  
  
6.  Creare un oggetto <xref:System.Security.Cryptography.Xml.EncryptionMethod> inizializzato sull'identificatore dell'URL dell'algoritmo di crittografia usato per generare la chiave.  Passare l'oggetto <xref:System.Security.Cryptography.Xml.EncryptionMethod> alla proprietà <xref:System.Security.Cryptography.Xml.EncryptedType.EncryptionMethod%2A>.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#7)]
     [!code-vb[HowToEncryptXMLElementSymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#7)]  
  
7.  Aggiungere i dati dell'elemento crittografato all'oggetto <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#8)]
     [!code-vb[HowToEncryptXMLElementSymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#8)]  
  
8.  Sostituire l'elemento dall'oggetto <xref:System.Xml.XmlDocument> originale con l'elemento <xref:System.Security.Cryptography.Xml.EncryptedData>.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#9)]
     [!code-vb[HowToEncryptXMLElementSymmetric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#9)]  
  
## Esempio  
  
```  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
  
```  
  
 [!code-csharp[HowToEncryptXMLElementSymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementSymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#1)]  
  
## Compilazione del codice  
  
-   Per compilare questo esempio, è necessario includere un riferimento a `System.Security.dll`.  
  
-   Includere gli spazi dei nomi seguenti: <xref:System.Xml>, <xref:System.Security.Cryptography> e <xref:System.Security.Cryptography.Xml>.  
  
## Sicurezza di .NET Framework  
 Non archiviare mai una chiave crittografica in testo non crittografato e non trasferire mai in testo non crittografato una chiave tra computer.  Usare invece un contenitore di chiavi sicuro per archiviare le chiavi di crittografia.  
  
 Dopo avere usato una chiave crittografica, cancellarla dalla memoria impostando ogni byte su zero oppure chiamando il metodo <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> della classe di crittografia gestita.  
  
## Vedere anche  
 <xref:System.Security.Cryptography.Xml>   
 [How to: Decrypt XML Elements with Symmetric Keys](../../../docs/standard/security/how-to-decrypt-xml-elements-with-symmetric-keys.md)