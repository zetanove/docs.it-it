---
title: "Denominazione sicura avanzata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "denominazione sicura [.NET Framework], ottimizzata"
  - "assembly con nome sicuro"
ms.assetid: 6cf17a82-62a1-4f6d-8d5a-d7d06dec2bb5
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Denominazione sicura avanzata
Una firma con nome sicuro è un meccanismo di identità in .NET Framework per l'identificazione degli assembly.  È una firma digitale a chiave pubblica utilizzata in genere per verificare l'integrità dei dati passati da un mittente \(il firmatario\) ad un destinatario \(il verificatore\).  Questa firma viene utilizzata come un'identità univoca per un assembly e garantisce che i riferimenti all'assembly non siano ambigui.  L'assembly è firmato come parte del processo di compilazione e quindi viene verificato quando viene caricato.  
  
 Le firme con nome sicuro consentono di impedire alle parti dannose di alterare un assembly e quindi firmare di nuovo l'assembly con la chiave originale del firmatario.  Tuttavia, le chiavi con nome sicuro non contengono alcuna informazione affidabile sull'editore, né contengono una gerarchia del certificato.  Una firma con nome sicuro non garantisce l'attendibilità della persona che ha firmato l'assembly o indica se tale utente è un proprietario legittimo della chiave; indica solo il possessore della chiave che ha firmato l'assembly.  Pertanto, non si consiglia l'utilizzo di una firma con nome sicuro come validator di sicurezza per considerare attendibile il codice di terze parti.  Microsoft Authenticode è la soluzione consigliata per autenticare il codice.  
  
## Limitazioni dei nomi sicuri convenzionali  
 La tecnologia dei nomi sicuri utilizzata nelle versioni precedenti [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] presenta le seguenti lacune:  
  
-   Le chiavi sono continuamente sotto attacco e le tecniche avanzate e l'hardware rendono più facile dedurre una chiave privata da una chiave pubblica.  Per proteggersi dagli attacchi, sono necessarie chiavi di dimensioni maggiori. Versioni di .NET Framework precedenti a [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] forniscono la possibilità di firmare con una chiave di qualsiasi dimensione \(la dimensione predefinita è 1024 bit\), ma firmare un assembly con una nuova chiave interrompe tutti i binari che fanno riferimento all'identità precedente dell'assembly.  Pertanto, è estremamente difficile aggiornare la dimensione di una chiave di firma se si desidera mantenere la compatibilità.  
  
-   La firma con nome sicuro supporta solo l'algoritmo SHA\-1.  SHA\-1 è stato recentemente trovato inadatto per le applicazioni protette di hashing.  Pertanto, è necessario un algoritmo più sicuro \(SHA\-256 o versione successiva\).  È possibile che SHA\-1 perda la condizione conforme a FIPS, che presenterebbe i problemi per coloro che scelgono di utilizzare solo il software e algoritmi conformi a FIPS.  
  
## Vantaggi dei nomi sicuri avanzati  
 I principali vantaggi dei nomi sicuri avanzati sono la compatibilità con i nomi sicuri preesistenti e la possibilità di stabilire che un'identità è equivalente a un'altra:  
  
-   Gli sviluppatori che hanno assembly preesistenti firmati possono eseguire la migrazione delle identità agli algoritmi SHA\-2 mentre mantengono la compatibilità con gli assembly che fanno riferimento alle identità precedenti.  
  
-   Gli sviluppatori che creano nuovi assembly e non sono interessati a firme con nome sicuro preesistenti possono utilizzare algoritmi SHA\-2 più sicuri e firmare assembly come hanno sempre fatto.  
  
## Utilizzo dei nomi sicuri avanzati  
 Le chiavi con nome sicuro sono costituiti da una chiave di firma e di una chiave di identità.  L'assembly viene firmato con la chiave di firma e viene identificato dalla chiave di identità.  Prima di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], queste due chiavi erano identiche.  A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], la chiave di identità rimane la stessa delle versioni precedenti di .NET Framework, ma la chiave di firma viene migliorata con un algoritmo di hash più sicuro.  Inoltre, la chiave di firma viene firmata con la chiave di identità per creare una controfirma.  
  
 L'attributo <xref:System.Reflection.AssemblySignatureKeyAttribute> consente ai metadati dell'assembly di utilizzare la chiave pubblica preesistente per l'identità dell'assembly, la quale consente ai riferimenti agli assembly precedenti di continuare a funzionare.  L'attributo <xref:System.Reflection.AssemblySignatureKeyAttribute> utilizza la controfirma per garantire che il proprietario della nuova chiave di firma sia anche il possessore della vecchia chiave di identità.  
  
### Firmare con SHA\-2, senza migrazione della chiave  
 Eseguire il comando seguente da una finestra del prompt dei comandi per firmare un assembly senza eseguire la migrazione di una firma con nome sicuro:  
  
1.  Generare una nuova chiave di identità \(se necessario\).  
  
    ```  
    sn -k IdentityKey.snk  
    ```  
  
2.  Estrarre la chiave di identità pubblica e specificare che un algoritmo SHA\-2 deve essere utilizzato quando si firma con questa chiave.  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk sha256  
    ```  
  
3.  Ritardare la firma dell'assembly con il file di chiave di identità pubblica.  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
4.  Firmare di nuovo l'assembly con la coppia completa di chiavi di identità.  
  
    ```  
    sn -Ra MyAssembly.exe IdentityKey.snk  
    ```  
  
### Firmare con SHA\-2, con migrazione della chiave  
 Eseguire il comando seguente da una finestra del prompt dei comandi per firmare un assembly eseguendo la migrazione di una firma con nome sicuro.  
  
1.  Generare una coppia di chiavi di firma e di identità \(se necessario\).  
  
    ```  
    sn -k IdentityKey.snk  
    sn -k SignatureKey.snk  
    ```  
  
2.  Estrarre la chiave di segnatura pubblica e specificare che un algoritmo SHA\-2 deve essere utilizzato quando si firma con questa chiave.  
  
    ```  
    sn -p SignatureKey.snk SignaturePubKey.snk sha256  
    ```  
  
3.  Estrarre la chiave di identità pubblica, che determina l'algoritmo hash che genera una controfirma.  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk  
    ```  
  
4.  Generare i parametri per un attributo <xref:System.Reflection.AssemblySignatureKeyAttribute> e aggiungere l'attributo all'assembly.  
  
    ```  
    sn -ac IdentityPubKey.snk IdentityKey.snk SignaturePubKey.snk  
    ```  
  
5.  Ritardare la firma dell'assembly con il file di chiave di identità pubblica.  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
  
    ```  
  
6.  Firmare completamente l'assembly con la coppia di chiavi di firma.  
  
    ```  
    sn -Ra MyAssembly.exe SignatureKey.snk  
    ```  
  
## Vedere anche  
 [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)