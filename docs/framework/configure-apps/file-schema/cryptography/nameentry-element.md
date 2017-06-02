---
title: "Elemento &lt;nameEntry&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#nameEntry"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/cryptoNameMapping/nameEntry"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<nameEntry> (elemento)"
  - "nameEntry (elemento)"
ms.assetid: 7d7535e9-4b4a-4b8c-82e2-e40dff5a7821
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Elemento &lt;nameEntry&gt;
Esegue il mapping del nome di una classe su un nome di algoritmo descrittivo consentendo l'uso di più nomi descrittivi per un'unica classe.  
  
## Sintassi  
  
```  
<nameEntry name="friendly name" Class="class name" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|**name**|Attributo obbligatorio.<br /><br /> Specifica il nome descrittivo dell'algoritmo implementato dalla classe di crittografia.|  
|**classe**|Attributo obbligatorio.<br /><br /> Specifica il valore per l'attributo **name** nell'elemento [\<cryptoClass\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclass-element.md).|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`system.web`|Specifica l'elemento radice per la sezione di configurazione ASP.NET.|  
  
## Note  
 L'attributo **name** può essere il nome di una delle classi astratte individuate nello spazio dei nomi <xref:System.Security.Cryptography>.  Quando si chiama il metodo **Create** su una classe astratta di crittografia, il nome di tale classe viene passato al metodo [Security.CryptoConfig.CreateFromName](frlrfSystemSecurityCryptographyCryptoConfigClassCreateFromNameTopic).  **CreateFromName** restituisce un'istanza del tipo indicato dall'attributo **class**.  Se l'attributo **name** è un nome breve, ad esempio RSA, è possibile utilizzare tale nome quando si chiama il metodo **CreateFromName**.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare l'elemento **\<nameEntry\>** per fare riferimento a una classe di crittografia e configurare il runtime.  È quindi possibile passare la stringa "RSA" al metodo <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=fullName> e utilizzare il metodo <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> per restituire un oggetto `MyCryptoRSAClass`.  
  
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