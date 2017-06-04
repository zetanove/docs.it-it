---
title: "Convenzioni dello schema di configurazione di WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7864356-f72f-4cae-995c-18e0431f8a58
caps.latest.revision: 3
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 3
---
# Convenzioni dello schema di configurazione di WIF
In questo argomento vengono illustrate le convenzioni utilizzate negli argomenti di configurazione di \(WIF\) della struttura dell'identità Windows e descritte alcune funzionalità comuni e attributi utilizzati in [\<system.identityModel\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md) e le sezioni [\<system.identityModel.services\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md).  
  
<a name="BKMK_Modes"></a>   
## Metodo  
 Molti degli elementi di configurazione di WIF dispongono di un attributo `mode`.  Questo attributo in genere verifica della classe utilizzata per effettuare una determinata parte dell'elaborazione e che gli elementi di configurazione è consentita come elementi figlio dell'elemento corrente.  Un errore di configurazione viene generato se gli elementi inclusi nel file di configurazione viene ignorato a causa delle impostazioni di sistema.  
  
<a name="BKMK_TimespanValues"></a>   
## Valori timespan  
 Dove <xref:System.TimeSpan> viene utilizzato come tipo di attributo, vedere il metodo <xref:System.TimeSpan.Parse%28System.String%29> per visualizzare il formato consentiti.  Questo formato è conforme alla specifica seguente.  
  
```  
[ws][-]{ d | [d.]hh:mm[:ss[.ff]] }[ws]  
```  
  
 Ad esempio, "30 ", "30.00:00", "30.00:00: 00 " tutti media 30 giorni; e "00:05", "00:05: 00 ", "0.00:05: 00,00 " tutti media 5 minuti.  
  
<a name="BKMK_CertificateReferences"></a>   
## Riferimenti del certificato  
 Alcuni riferimenti di ottenere elementi ai certificati mediante l'elemento `<certificateReference>`.  Per fare riferimento a un certificato, i seguenti attributi sono disponibili.  
  
|||  
|-|-|  
|`storeLocation`|Un valore di enumerazione <xref:System.Security.Cryptography.X509Certificates.StoreLocation> : `CurrentUser` o `CurrentMachine`.|  
|`storeName`|Un valore di enumerazione <xref:System.Security.Cryptography.X509Certificates.StoreName> ; il più utili per questo contesto sono `My` e `TrustedPeople`.|  
|`x509FindType`|Un valore di enumerazione <xref:System.Security.Cryptography.X509Certificates.X509FindType> ; il più utili per questo contesto sono `FindBySubjectName` e `FindByThumbprint`.  Per eliminare la probabilità di errore, si consiglia del tipo `FindByThumbprint` viene utilizzato in ambienti di produzione.|  
|`findValue`|Il valore utilizzato per trovare il certificato, in base all'attributo `x509FindType`.  Per eliminare la probabilità di errore, si consiglia del tipo `FindByThumbprint` viene utilizzato in ambienti di produzione.  Quando `FindByThumbPrint` viene specificato, questo attributo accetta un valore che rappresenta il formato stringa esadecimale dell'identificativo del certificato, ad esempio, "97249e1a5fa6bee5e515b82111ef524a4c91583f".|  
  
<a name="BKMK_CustomTypeReferences"></a>   
## Riferimenti di tipo personalizzato  
 Diversi tipi di riferimento personalizzati di elementi utilizzando l'attributo `type`.  Questo attributo deve specificare il nome del tipo personalizzato.  Per fare riferimento a un tipo dalla Global Assembly Cache \(GAC\), un nome sicuro deve essere utilizzato.  Per fare riferimento a un tipo da un assembly nella directory di recipiente, un riferimento completo dell'assembly semplice può essere utilizzato.  I tipi definiti nella directory di App\_Code\/è possibile fare riferimento a semplicemente specificando il nome del tipo senza assembly di qualificazione.  
  
 I tipi personalizzati devono essere derivato dal tipo specificato e devono fornire un costruttore predefinito `public` argomenti \(0\).  
  
## Vedere anche  
 [\<system.identityModel\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel.md)   
 [\<system.identityModel.services\>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md)