---
title: "Walkthrough: Encrypting and Decrypting Strings in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "encryption, strings"
  - "strings [Visual Basic], encrypting"
  - "decryption, strings"
  - "strings [Visual Basic], decrypting"
ms.assetid: 1f51e40a-2f88-43e2-a83e-28a0b5c0d6fd
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Walkthrough: Encrypting and Decrypting Strings in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa procedura dettagliata viene illustrato l'utilizzo della classe <xref:System.Security.Cryptography.DESCryptoServiceProvider> per la crittografia e decrittografia di stringhe mediante la versione del provider di servizi di crittografia \(CSP\) dell'algoritmo Triple Data Encryption Standard \(<xref:System.Security.Cryptography.TripleDES>\).  Il primo passo è la creazione di una classe wrapper semplice che incapsula l'algoritmo 3DES e memorizza i dati crittografati come stringa con codifica Base 64.  Il wrapper viene quindi utilizzato per archiviare in modo protetto i dati personali dell'utente in un file di testo pubblicamente accessibile.  
  
 È possibile utilizzare la crittografia per proteggere informazioni riservate dell'utente \(ad esempio, la password\) e impedire a utenti non autorizzati la lettura delle credenziali.  È possibile impedire che l'identità di un utente autorizzato venga prelevata, proteggere le risorse dell'utente e fornire il non ripudio.  La crittografia consente inoltre di proteggere i dati dell'utente dall'accesso di utenti non autorizzati.  
  
 Per ulteriori informazioni, vedere [Servizi di crittografia](../Topic/Cryptographic%20Services.md).  
  
> [!IMPORTANT]
>  Gli algoritmi Rijndael, noto ora come Advanced Encryption Standard \(AES\), e Triple Data Encryption Standard \(3DES\) garantiscono una maggiore sicurezza rispetto al DES in quanto più complessi dal punto di vista del calcolo.  Per ulteriori informazioni, vedere <xref:System.Security.Cryptography.DES> e <xref:System.Security.Cryptography.Rijndael>.  
  
### Per creare il wrapper di crittografia  
  
1.  Creare una classe `Simple3Des` per incapsulare i metodi di crittografia e decrittografia.  
  
     [!code-vb[VbVbalrStrings#38](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_1.vb)]  
  
2.  Aggiungere un'importazione dello spazio dei nomi di crittografia all'inizio del file che contiene la classe `Simple3Des`.  
  
     [!code-vb[VbVbalrStrings#77](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_2.vb)]  
  
3.  Nella classe `Simple3Des`, aggiungere un campo privato per archiviare il provider di servizi crittografici 3DES.  
  
     [!code-vb[VbVbalrStrings#39](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_3.vb)]  
  
4.  Aggiungere un metodo privato per creare una matrice di byte di lunghezza specificata dall'hash della chiave indicata.  
  
     [!code-vb[VbVbalrStrings#41](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_4.vb)]  
  
5.  Aggiungere un costruttore per inizializzare il provider di servizi crittografici 3DES.  
  
     Il parametro `key` controlla i metodi `EncryptData` e `DecryptData`.  
  
     [!code-vb[VbVbalrStrings#40](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_5.vb)]  
  
6.  Aggiungere un metodo pubblico per la crittografia della stringa.  
  
     [!code-vb[VbVbalrStrings#42](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_6.vb)]  
  
7.  Aggiungere un metodo pubblico per la decrittografia della stringa.  
  
     [!code-vb[VbVbalrStrings#43](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_7.vb)]  
  
     È ora possibile utilizzare la classe wrapper per proteggere le risorse dell'utente.  Nel seguente esempio, la classe viene utilizzata per archiviare in modo protetto i dati personali dell'utente in un file di testo accessibile pubblicamente.  
  
### Per verificare il funzionamento del wrapper di crittografia  
  
1.  Aggiungere in un'altra classe un metodo che utilizza il metodo `EncryptData` del wrapper per crittografare una stringa e scriverla nella cartella Documenti dell'utente.  
  
     [!code-vb[VbVbalrStrings#78](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_8.vb)]  
  
2.  Aggiungere un metodo con cui è possibile leggere la stringa crittografata nella cartella Documenti dell'utente e decrittografare tale stringa con il metodo `DecryptData` del wrapper.  
  
     [!code-vb[VbVbalrStrings#79](../../../../visual-basic/language-reference/functions/codesnippet/visualbasic/walkthrough-encrypting-a_9.vb)]  
  
3.  Aggiungere il codice dell'interfaccia dell'utente per chiamare i metodi `TestEncoding` e `TestDecoding`.  
  
4.  Eseguire l'applicazione.  
  
     Se viene fornita una password errata, non è possibile decrittografare i dati durante la verifica dell'applicazione.  
  
## Vedere anche  
 <xref:System.Security.Cryptography>   
 <xref:System.Security.Cryptography.DESCryptoServiceProvider>   
 <xref:System.Security.Cryptography.DES>   
 <xref:System.Security.Cryptography.TripleDES>   
 <xref:System.Security.Cryptography.Rijndael>   
 [Servizi di crittografia](../Topic/Cryptographic%20Services.md)