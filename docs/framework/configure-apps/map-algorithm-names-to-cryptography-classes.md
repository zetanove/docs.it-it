---
title: "Mapping di nomi di algoritmi a classi di crittografia | Microsoft Docs"
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
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "algoritmi di crittografia"
  - "crittografia, mapping di nomi di algoritmi"
  - "mapping di nomi di algoritmi"
  - "nomi [.NET Framework], mapping di algoritmi"
ms.assetid: 01327c69-c5e1-4ef6-b73f-0a58351f0492
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Mapping di nomi di algoritmi a classi di crittografia
Per la creazione di un oggetto di crittografia mediante [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] gli sviluppatori hanno a disposizione le quattro tecniche indicate di seguito:  
  
-   Creazione di un oggetto mediante l'operatore **new**.  
  
-   Creazione di un oggetto che implementa un determinato algoritmo di crittografia chiamando il metodo **Create** sulla classe astratta relativa a tale algoritmo.  
  
-   Creazione di un oggetto che implementa un determinato algoritmo di crittografia chiamando il metodo [System.Security.Cryptography.CryptoConfig.CreateFromName](frlrfSystemSecurityCryptographyCryptoConfigClassCreateFromNameTopic).  
  
-   Creare un oggetto che implementa una classe di algoritmi di crittografia, ad esempio un algoritmo di tipo block cipher simmetrico, chiamando il metodo **Create** sulla classe astratta relativa a tale algoritmo, ad esempio <xref:System.Security.Cryptography.SymmetricAlgorithm>.  
  
 Si supponga ad esempio che uno sviluppatore desideri calcolare il valore hash SHA1 di un insieme di byte.  Lo spazio dei nomi <xref:System.Security.Cryptography> contiene due implementazioni dell'algoritmo SHA1, una è puramente gestita mentre l'altra esegue il wrapping di CryptoAPI.  Lo sviluppatore può scegliere di creare un'istanza di una determinata implementazione SHA1, ad esempio la [classe SHA1Managed](frlrfSystemSecurityCryptographySHA1ManagedClassTopic), chiamando l'operatore **new**.  Se tuttavia non è rilevante che venga caricata una classe specifica da Common Language Runtime, purché venga implementato l'algoritmo hash SHA1, lo sviluppatore può creare un oggetto chiamando il metodo [System.Security.Cryptography.SHA1.Create](frlrfSystemSecurityCryptographySHA1ClassCreateTopic).  Quest'ultimo chiama a sua volta **System.Security.Cryptography.CryptoConfig.CreateFromName\("System.Security.Cryptography.SHA1"\)**, che deve restituire un'implementazione dell'algoritmo hash SHA1.  
  
 Lo sviluppatore può chiamare anche **System.Security.Cryptography.CryptoConfig.CreateFromName\("SHA1"\)** poiché, per impostazione predefinita, il sistema di configurazione della crittografia supporta l'utilizzo di nomi brevi per gli algoritmi forniti con .NET Framework.  
  
 Se non è rilevante che venga utilizzato un algoritmo hash specifico, lo sviluppatore può chiamare il metodo [System.Security.Cryptography.HashAlgorithm.Create](frlrfSystemSecurityCryptographyHashAlgorithmClassCreateTopic), che restituisce un oggetto per l'implementazione di una trasformazione basata su hash.  
  
## Mapping di nomi di algoritmi nei file di configurazione  
 Per impostazione predefinita, viene restituito un oggetto della [classe System.Security.Cryptography.SHA1CryptoServiceProvider](frlrfSystemSecurityCryptographySHA1CryptoServiceProviderClassTopic) in tutti e quattro gli scenari.  Tuttavia, un amministratore può modificare il tipo di oggetto restituito dai metodi negli ultimi due scenari.  Per eseguire questa operazione, è necessario mappare un nome descrittivo di un algoritmo alla classe che si desidera utilizzare nel file di configurazione del computer \(Machine.config\).  
  
 Nell'esempio riportato di seguito viene illustrato come configurare il runtime affinché i metodi **System.Security.Cryptography.SHA1.Create**, **System.Security.CryptoConfig.CreateFromName\("SHA1"\)** e **System.Security.Cryptography.HashAlgorithm.Create** restituiscano un oggetto `MySHA1HashClass`.  
  
```  
<configuration>  
   <!-- Other configuration settings. -->  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MySHA1Hash="MySHA1HashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="SHA1" class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.SHA1"  
                       class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MySHA1Hash"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 È possibile specificare il nome dell'attributo nell'[elemento \<cryptoClass\>](../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclass-element.md) \(nell'esempio precedente, all'attributo è stato assegnato il nome `MySHA1Hash`\).  Il valore dell'attributo nell'elemento **\<cryptoClass\>** è una stringa utilizzata da Common Language Runtime per individuare la classe.  È possibile utilizzare qualsiasi stringa in grado di soddisfare i requisiti definiti nella sezione [Specifica di nomi di tipo completi](../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).  
  
 È possibile mappare molti nomi di algoritmo alla stessa classe.  L'[elemento \<nameEntry\>](../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md) mappa una classe a un solo nome descrittivo di algoritmo.  L'attributo **name** può essere una stringa utilizzata durante la chiamata al metodo **System.Security.Cryptography.CryptoConfig.CreateFromName** o il nome di una classe di crittografia astratta nello spazio dei nomi <xref:System.Security.Cryptography>.  Il valore dell'attributo **class** è il nome dell'attributo nell'elemento **\<cryptoClass\>**.  
  
> [!NOTE]
>  È possibile ottenere un algoritmo SHA1 chiamando il metodo [System.Security.Cryptography.SHA1.Create](frlrfSystemSecurityCryptographySHA1ClassCreateTopic) o **Security.CryptoConfig.CreateFromName\("SHA1"\)**.  Ciascun metodo assicura solo che venga restituito un oggetto che implementa l'algoritmo SHA1.  Non è necessario mappare ogni nome descrittivo di un algoritmo alla stessa classe nel file di configurazione.  
  
 Per l'elenco dei nomi predefiniti e delle classi a cui sono mappati, vedere [Classe CryptoConfig](frlrfSystemSecurityCryptographyCryptoConfigClassTopic).  
  
## Vedere anche  
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)   
 [Configurazione di classi di crittografia](../../../docs/framework/configure-apps/configure-cryptography-classes.md)