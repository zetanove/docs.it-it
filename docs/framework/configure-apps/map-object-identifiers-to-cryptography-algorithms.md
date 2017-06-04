---
title: "Mapping di identificatori di oggetti ad algoritmi di crittografia | Microsoft Docs"
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
  - "crittografia, mapping di identificatori di oggetti"
  - "firme digitali"
  - "identificatori, mapping di identificatori di oggetti"
  - "mapping di identificatori di oggetti"
ms.assetid: c9673f81-bf9e-47fd-bc6f-6bc1c1c4c15e
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# Mapping di identificatori di oggetti ad algoritmi di crittografia
Le firme digitali assicurano l'integrità dei dati durante il trasferimento da un programma a un altro.  In genere la firma digitale viene calcolata applicando una funzione matematica al valore hash dei dati da firmare.  Durante la formattazione di un valore hash da firmare, alcuni algoritmi di firma digitale aggiungono l'identificatore di oggetto \(OID, Object Identifier\) ASN.1 in coda al valore.  L'OID identifica l'algoritmo utilizzato per calcolare il valore hash.  È possibile mappare algoritmi agli identificatori di oggetto per estendere il meccanismo di crittografia in modo che utilizzi algoritmi personalizzati.  Nell'esempio riportato di seguito viene illustrato come mappare un identificatore di oggetto a un nuovo algoritmo hash.  
  
```  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MyNewHash="MyNewHashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="NewHash" class="MyNewHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.14.33.42.46"  name="NewHash"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 L'[elemento \<oidEntry\>](../../../docs/framework/configure-apps/file-schema/cryptography/oidentry-element.md) contiene due attributi.  L'attributo **OID** è il numero dell'identificatore di oggetto.  L'attributo **name** è il valore dell'attributo **name** dall'[elemento \<nameEntry\>](../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md).  Prima di mappare un identificatore di oggetto a un nome semplice, è necessario che il nome di un algoritmo sia mappato a una classe.  
  
## Vedere anche  
 [Configurazione di classi di crittografia](../../../docs/framework/configure-apps/configure-cryptography-classes.md)   
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)