---
title: ".NET Framework Cryptography Model | Microsoft Docs"
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
  - "cryptography [.NET Framework], model"
  - "encryption [.NET Framework], model"
ms.assetid: 12fecad4-fbab-432a-bade-2f05976a2971
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# .NET Framework Cryptography Model
.NET Framework fornisce le implementazioni di numerosi algoritmi di crittografia standard.  Questi algoritmi sono facili da usare e le loro proprietà predefinite sono il più sicure possibile.  Inoltre, il modello di crittografia di .NET Framework di ereditarietà degli oggetti, progettazione tramite flusso e configurazione è estremamente estendibile.  
  
## Ereditarietà degli oggetti  
 Il sistema di sicurezza di .NET Framework implementa un modello estendibile di ereditarietà delle classi derivate.  La gerarchia è la seguente:  
  
-   Classe di tipo algoritmo, ad esempio <xref:System.Security.Cryptography.SymmetricAlgorithm>, <xref:System.Security.Cryptography.AsymmetricAlgorithm> o <xref:System.Security.Cryptography.HashAlgorithm>.  Questo livello è astratto.  
  
-   Classe di algoritmo che eredita da una classe di tipo algoritmo, ad esempio <xref:System.Security.Cryptography.Aes>, <xref:System.Security.Cryptography.RC2> o <xref:System.Security.Cryptography.ECDiffieHellman>.  Questo livello è astratto.  
  
-   Implementazione di una classe di algoritmo che eredita da una classe di algoritmo, ad esempio <xref:System.Security.Cryptography.AesManaged>, <xref:System.Security.Cryptography.RC2CryptoServiceProvider> o <xref:System.Security.Cryptography.ECDiffieHellmanCng>.  Questo livello è completamente implementato.  
  
 Usando questo modello di classi derivate, è possibile aggiungere in modo semplice un nuovo algoritmo o una nuova implementazione di un algoritmo esistente.  Ad esempio, per creare un nuovo algoritmo a chiave pubblica, si eredita dalla classe <xref:System.Security.Cryptography.AsymmetricAlgorithm>.  Per creare una nuova implementazione di un algoritmo specifico, è necessario creare una classe derivata non astratta di tale algoritmo.  
  
## Modalità di implementazione degli algoritmi in .NET Framework  
 Come esempio delle diverse implementazioni disponibili per un algoritmo, considerare gli algoritmi simmetrici.  La base per tutti gli algoritmi simmetrici è l'oggetto <xref:System.Security.Cryptography.SymmetricAlgorithm>, ereditato dagli algoritmi seguenti:  
  
1.  <xref:System.Security.Cryptography.Aes>  
  
2.  <xref:System.Security.Cryptography.DES>  
  
3.  <xref:System.Security.Cryptography.RC2>  
  
4.  <xref:System.Security.Cryptography.Rijndael>  
  
5.  <xref:System.Security.Cryptography.TripleDES>  
  
 L'oggetto <xref:System.Security.Cryptography.Aes> viene ereditato da due classi: <xref:System.Security.Cryptography.AesCryptoServiceProvider> e <xref:System.Security.Cryptography.AesManaged>.  La classe <xref:System.Security.Cryptography.AesCryptoServiceProvider> è un wrapper per l'implementazione dell'API di crittografia \(CAPI, Cryptography API\) Windows di Aes, mentre la classe <xref:System.Security.Cryptography.AesManaged> viene scritta interamente in codice gestito.  Vi è anche un terzo tipo di implementazione, Cryptography Next Generation \(CNG\), oltre alle implementazioni gestita e CAPI.  Un esempio di algoritmo CNG è <xref:System.Security.Cryptography.ECDiffieHellmanCng>.  Gli algoritmi CNG sono disponibili in Windows Vista e versioni successive.  
  
 È possibile scegliere l'implementazione più appropriata.  Le implementazioni gestite sono disponibili in tutte le piattaforme che supportano .NET Framework.  Le implementazioni CAPI sono disponibili nei sistemi operativi precedenti e non vengono più sviluppate.  CNG è l'implementazione più recente, su cui si baseranno le nuove attività di sviluppo.  Tuttavia, le implementazioni gestite non sono certificate da FIPS \(Federal Information Processing Standards\) e potrebbero essere più lente rispetto alle classi wrapper.  
  
## Progettazione tramite flusso  
 Common Language Runtime usa una progettazione orientata al flusso per l'implementazione di algoritmi simmetrici e algoritmi hash.  La base di questa progettazione è la classe <xref:System.Security.Cryptography.CryptoStream>, che deriva dalla classe <xref:System.IO.Stream>.  Gli oggetti di crittografia basati sul flusso supportano una singola interfaccia standard \(`CryptoStream`\) per la gestione della porzione di trasferimento di dati dell'oggetto.  Poiché tutti gli oggetti sono basati su un'interfaccia standard, è possibile concatenare più oggetti \(ad esempio un oggetto hash seguito da un oggetto di crittografia\) ed eseguire più operazioni sui dati senza che sia necessaria un'archiviazione intermedia.  Il modello di flusso consente inoltre di creare oggetti da oggetti più piccoli.  Ad esempio, un algoritmo di crittografia e hash combinato può essere visto come un singolo oggetto flusso, anche se questo oggetto può essere costituito da un set di oggetti flusso.  
  
## Configurazione della crittografia  
 La configurazione della crittografia consente di risolvere un'implementazione specifica di un algoritmo in un nome di algoritmo, garantendo estendibilità delle classi di crittografia .NET Framework.  È possibile aggiungere la propria implementazione hardware o software di un algoritmo e mappare l'implementazione al nome di algoritmo desiderato.  Se un algoritmo non è specificato nel file di configurazione, vengono usate le impostazioni predefinite.  Per altre informazioni sulla configurazione della crittografia, vedere [Configurazione di classi di crittografia](../../../docs/framework/configure-apps/configure-cryptography-classes.md).  
  
## Scelta di un algoritmo  
 È possibile scegliere un algoritmo per motivi diversi: ad esempio, per l'integrità dei dati, per la privacy dei dati o per generare una chiave.  Gli algoritmi simmetrici e hash sono finalizzati alla protezione dei dati per motivi di integrità \(proteggere da eventuali modifiche\) o di privacy \(impedire la visualizzazione\).  Gli algoritmi hash vengono usati principalmente per l'integrità dei dati.  
  
 Ecco un elenco degli algoritmi consigliati in base all'applicazione:  
  
-   Privacy dei dati:  
  
    -   <xref:System.Security.Cryptography.Aes>  
  
-   Integrità dei dati:  
  
    -   <xref:System.Security.Cryptography.HMACSHA256>  
  
    -   <xref:System.Security.Cryptography.HMACSHA512>  
  
-   Firma digitale:  
  
    -   <xref:System.Security.Cryptography.ECDsa>  
  
    -   <xref:System.Security.Cryptography.RSA>  
  
-   Scambio di chiave:  
  
    -   <xref:System.Security.Cryptography.ECDiffieHellman>  
  
    -   <xref:System.Security.Cryptography.RSA>  
  
-   Generazione casuale di numeri:  
  
    -   <xref:System.Security.Cryptography.RNGCryptoServiceProvider>  
  
-   Generazione di una chiave da una password:  
  
    -   <xref:System.Security.Cryptography.Rfc2898DeriveBytes>  
  
## Vedere anche  
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)   
 [Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)