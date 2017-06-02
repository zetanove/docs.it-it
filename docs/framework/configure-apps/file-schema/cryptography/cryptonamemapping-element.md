---
title: "Elemento &lt;cryptoNameMapping&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptoNameMapping"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/cryptoNameMapping"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<cryptoNameMapping> (elemento)"
  - "cryptoNameMapping (elemento)"
ms.assetid: c59c9494-149b-4ce6-b38d-371f896ae85c
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Elemento &lt;cryptoNameMapping&gt;
Contiene i mapping delle classi sui nomi descrittivi.  
  
## Sintassi  
  
```  
  
      <cryptoNameMapping>   
</cryptoNameMapping>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`cryptoClasses`|Contiene un elenco delle classi di crittografia per le quali è stato eseguito il mapping su un nome descrittivo nell'elemento **\<nameEntry\>**.|  
|`nameEntry`|Esegue il mapping del nome di una classe su un nome di algoritmo descrittivo consentendo l'uso di più nomi descrittivi per un'unica classe.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`cryptographySettings`|Contiene le impostazioni di crittografia.|  
|`cryptoNameMapping`|Contiene i mapping delle classi sui nomi descrittivi.|  
|`mscorlib`|Contiene l'elemento \<cryptographySettings\>.|  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare l'elemento **\<cryptoNameMapping\>** per fare riferimento a una classe di crittografia e configurare il runtime.  È quindi possibile passare la stringa "RSA" al metodo <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=fullName> e utilizzare il metodo <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> per restituire un oggetto `MyCryptoRSAClass`.  
  
```  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCryptoRSA="MyCryptoRSAClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RSA" class="MyCryptoRSA"/>  
            <nameEntry name="System.Security.Cryptography.AsymmetricAlgorithm"  
                       class="MyCryptoRSA"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## Vedere anche  
 [Schema dei file di configurazione](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [Schema delle impostazioni di crittografia](../../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)   
 [Servizi di crittografia](../../../../../docs/standard/security/cryptographic-services.md)   
 [Configurazione di classi di crittografia](../../../../../docs/framework/configure-apps/configure-cryptography-classes.md)