---
title: "Elemento &lt;cryptoClass&gt; | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/cryptoNameMapping/cryptoClasses/cryptoClass"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptoClass"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<cryptoClass> (elemento)"
  - "cryptoClass (elemento)"
ms.assetid: 03db52ef-010e-44ea-b6fd-b9c900ecad50
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 14
---
# Elemento &lt;cryptoClass&gt;
Contiene una classe di crittografia per la quale è stato eseguito il mapping su un nome descrittivo nell'elemento [\<nameEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md).  
  
## Sintassi  
  
```  
<cryptoClass customClassName="fully qualified type name" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|`customClassName`|Attributo obbligatorio.<br /><br /> Contiene le informazioni per la classe di crittografia.  Utilizzare l'attributo per fornire un nome breve per la classe.  È necessario specificare una stringa che soddisfi i requisiti indicati in [Specifica di nomi di tipo completi](../../../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md).|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`configuration`|Elemento radice in ciascun file di configurazione utilizzato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`cryptoClasses`|Contiene un elenco delle classi di crittografia per le quali è stato eseguito il mapping su un nome descrittivo nell'elemento [\<nameEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md).|  
|`cryptographySettings`|Contiene le impostazioni di crittografia.|  
|`cryptoNameMapping`|Contiene i mapping delle classi sui nomi descrittivi.|  
|`mscorlib`|Contiene l'elemento [\<cryptographySettings\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptographysettings-element.md).|  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare l'elemento **\<cryptoClass\>** per fare riferimento a una classe di crittografia e configurare il runtime.  È quindi possibile passare la stringa "RSA" al metodo <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=fullName> e utilizzare il metodo <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> per restituire un oggetto `MyCryptoRSAClass`.  
  
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