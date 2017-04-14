---
title: "Specifica di un algoritmo di crittografia personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d662a305-8e09-451d-9a59-b0f12b012f1d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Specifica di un algoritmo di crittografia personalizzato
WCF consente di specificare un algoritmo di crittografia personalizzato da usare per crittografare i dati o calcolare le firme digitali.  A tale scopo, attenersi alla procedura seguente:  
  
1.  Derivare una classe da <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.  
  
2.  Registrare l'algoritmo.  
  
3.  Configurare l'associazione con la classe derivata da <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>.  
  
## Derivare una classe da SecurityAlgorithmSuite.  
 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> è una classe di base astratta che consente di specificare l'algoritmo da usare per eseguire diverse operazioni relative alla sicurezza.  Ad esempio, calcolare un hash per una firma digitale o crittografare un messaggio.  Nel codice seguente viene illustrato come derivare una classe da <xref:System.ServiceModel.Security.SecurityAlgorithm>.  
  
```csharp  
public class MyCustomAlgorithmSuite : SecurityAlgorithmSuite  
    {  
        public override string DefaultAsymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaOaepKeyWrap; }  
        }  
  
        public override string DefaultAsymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaSha1Signature; }  
        }  
  
        public override string DefaultCanonicalizationAlgorithm  
        {  
            get { return SecurityAlgorithms.ExclusiveC14n; ; }  
        }  
  
        public override string DefaultDigestAlgorithm  
        {  
            get { return SecurityAlgorithms.MyCustomHashAlgorithm; }  
        }  
  
        public override string DefaultEncryptionAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override int DefaultEncryptionKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSignatureKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSymmetricKeyLength  
        {  
            get { return 128; }  
        }  
  
        public override string DefaultSymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override string DefaultSymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.HmacSha1Signature; }  
        }  
  
        public override bool IsAsymmetricKeyLengthSupported(int length)  
        {  
            return length >= 1024 && length <= 4096;  
        }  
  
        public override bool IsSymmetricKeyLengthSupported(int length)  
        {  
            return length >= 128 && length <= 256;  
        }  
    }  
  
```  
  
## Registrare l'algoritmo personalizzato  
 La registrazione può essere eseguita in un file di configurazione o nel codice imperativo.  La registrazione di un algoritmo personalizzato viene eseguita creando un mapping tra una classe che implementa un provider di servizi di crittografia e un alias.  L'alias viene quindi mappato a un URI che viene usato per specificare l'algoritmo nell'associazione del servizio WCF.  Nel frammento di configurazione seguente viene illustrato come registrare un algoritmo personalizzato in config:  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
           <cryptoClasses>  
              <cryptoClass SHA256CSP="System.Security.Cryptography.SHA256CryptoServiceProvider, System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
           </cryptoClasses>  
           <nameEntry name="http://constoso.com/CustomAlgorithms/CustomHashAlgorithm"  
              class="SHA256CSP" />  
           </cryptoNameMapping>  
        </cryptographySettings>  
    </mscorlib>  
</configuration>  
  
```  
  
 La sezione sotto l'elemento \<`cryptoClasses`\> crea il mapping tra SHA256CryptoServiceProvider e l'alias "SHA256CSP".  L'elemento \<[nameEntry](assetId:///nameEntry?qualifyHint=False&amp;autoUpgrade=True)\> crea il mapping tra l'alias "SHA256CSP" e l'URL specificato \(http:\/\/constoso.com\/CustomAlgorithms\/CustomHashAlgorithm \).  
  
 Per registrare l'algoritmo personalizzato nel codice usare il metodo [M:System.Security.Cryptography.CryptoConfig.AddAlgorithm\(System.Type, System.String\<xref:System.Security.Cryptography.CryptoConfig.AddAlgorithm%2A> System.String[])?qualifyHint=False&autoUpgrade=True.  Questo metodo crea entrambi i mapping.  Nell'esempio seguente viene illustrato come chiamare questo metodo:  
  
```  
// Register the custom URI string defined for the hashAlgorithm in MyCustomAlgorithmSuite class to create the   
// SHA256CryptoServiceProvider hash algorithm object.  
CryptoConfig.AddAlgorithm(typeof(SHA256CryptoServiceProvider), "http://constoso.com/CustomAlgorithms/CustomHashAlgorithm");  
  
```  
  
## Configurare l'associazione  
 L'associazione si configura specificando la classe derivata da <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> nelle impostazioni di associazione, come indicato nel frammento di codice seguente:  
  
```csharp  
WSHttpBinding binding = new WSHttpBinding();  
            binding.Security.Message.AlgorithmSuite = new MyCustomAlgorithmSuite();  
  
```  
  
 Per un esempio di codice completo, vedere [Agilità di crittografia nella sicurezza WCF](../../../../docs/framework/wcf/samples/cryptographic-agility-in-wcf-security.md).  
  
## Vedere anche  
 [Protezione di servizi e client](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Protezione dei servizi](../../../../docs/framework/wcf/securing-services.md)   
 [Cenni preliminari sulla sicurezza](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Concetti sulla protezione](../../../../docs/framework/wcf/feature-details/security-concepts.md)