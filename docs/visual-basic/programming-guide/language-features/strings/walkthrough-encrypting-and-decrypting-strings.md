---
title: La crittografia e decrittografia di stringhe in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- encryption, strings
- strings [Visual Basic], encrypting
- decryption, strings
- strings [Visual Basic], decrypting
ms.assetid: 1f51e40a-2f88-43e2-a83e-28a0b5c0d6fd
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ae3d599f7173162c07fbaeda60435615f101b10d
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-encrypting-and-decrypting-strings-in-visual-basic"></a>Procedura dettagliata: crittografia e decrittografia di stringhe in Visual Basic
Questa procedura dettagliata viene illustrato come utilizzare il <xref:System.Security.Cryptography.DESCryptoServiceProvider>(classe) per crittografare e decrittografare le stringhe utilizzando la versione del provider (CSP) del servizio di crittografia di Triple Data Encryption Standard (<xref:System.Security.Cryptography.TripleDES>) algoritmo.</xref:System.Security.Cryptography.TripleDES> </xref:System.Security.Cryptography.DESCryptoServiceProvider> Il primo passaggio consiste nel creare una semplice classe wrapper che incapsula l'algoritmo 3DES e archivia i dati crittografati come una stringa con codifica base 64. Il wrapper viene quindi utilizzato per archiviare in modo sicuro i dati personali dell'utente in un file di testo accessibile pubblicamente.  
  
 È possibile utilizzare la crittografia per proteggere informazioni riservate dell'utente (ad esempio, le password) e per rendere illeggibile le credenziali di utenti non autorizzati. È possibile impedire identità di un utente autorizzato da rubati, che consente di proteggere le risorse dell'utente e consente di non ripudio. La crittografia può inoltre proteggere i dati dell'utente da cui si accede da utenti non autorizzati.  
  
 Per ulteriori informazioni, vedere [servizi di crittografia](http://msdn.microsoft.com/library/f96284bc-7b73-44b5-ac59-fac613ad09f8).  
  
> [!IMPORTANT]
>  Gli algoritmi Triple Data Encryption Standard (3DES) e Rijndael (ora denominato Advanced Encryption Standard [AES]) garantiscono maggiore sicurezza rispetto a DES in quanto più complesse. Per ulteriori informazioni, vedere <xref:System.Security.Cryptography.DES>e <xref:System.Security.Cryptography.Rijndael>.</xref:System.Security.Cryptography.Rijndael> </xref:System.Security.Cryptography.DES>  
  
### <a name="to-create-the-encryption-wrapper"></a>Per creare il wrapper di crittografia  
  
1.  Creare la `Simple3Des` classe per incapsulare i metodi di crittografia e decrittografia.  
  
     [!code-vb[VbVbalrStrings&#38;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_1.vb)]  
  
2.  Aggiungere un'importazione dello spazio dei nomi cryptography all'inizio del file che contiene la `Simple3Des` classe.  
  
     [!code-vb[&#77; VbVbalrStrings](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_2.vb)]  
  
3.  Nella `Simple3Des` classe, aggiungere un campo privato per archiviare il provider del servizio di crittografia 3DES.  
  
     [!code-vb[VbVbalrStrings&#39;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_3.vb)]  
  
4.  Aggiungere un metodo privato che crea una matrice di byte di lunghezza specificata dall'hash della chiave specificata.  
  
     [!code-vb[VbVbalrStrings n.&41;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_4.vb)]  
  
5.  Aggiungere un costruttore per inizializzare il provider del servizio di crittografia 3DES.  
  
     Il `key` parametro controlla il `EncryptData` e `DecryptData` metodi.  
  
     [!code-vb[&#40; VbVbalrStrings](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_5.vb)]  
  
6.  Aggiungere un metodo pubblico che consente di crittografare una stringa.  
  
     [!code-vb[VbVbalrStrings&#42;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_6.vb)]  
  
7.  Aggiungere un metodo pubblico che consente di decrittografare una stringa.  
  
     [!code-vb[VbVbalrStrings&#43;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_7.vb)]  
  
     La classe wrapper ora può essere utilizzata per proteggere risorse utente. In questo esempio, consente di archiviare in modo sicuro i dati personali dell'utente in un file di testo accessibile pubblicamente.  
  
### <a name="to-test-the-encryption-wrapper"></a>Per testare il wrapper di crittografia  
  
1.  In una classe separata, aggiungere un metodo che usa il wrapper `EncryptData` per crittografare una stringa e scriverli all'utente della cartella documenti.  
  
     [!code-vb[VbVbalrStrings&#78;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_8.vb)]  
  
2.  Aggiungere un metodo che legge la stringa crittografata da parte dell'utente della cartella documenti e consente di decrittografare la stringa con il wrapper `DecryptData` metodo.  
  
     [!code-vb[VbVbalrStrings&#79;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_9.vb)]  
  
3.  Aggiungere il codice dell'interfaccia utente di chiamare il `TestEncoding` e `TestDecoding` metodi.  
  
4.  Eseguire l'applicazione.  
  
     Quando si testa l'applicazione, si noti che non è possibile decrittografare i dati se si specifica la password errata.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Security.Cryptography></xref:System.Security.Cryptography>   
 <xref:System.Security.Cryptography.DESCryptoServiceProvider></xref:System.Security.Cryptography.DESCryptoServiceProvider>   
 <xref:System.Security.Cryptography.DES></xref:System.Security.Cryptography.DES>   
 <xref:System.Security.Cryptography.TripleDES></xref:System.Security.Cryptography.TripleDES>   
 <xref:System.Security.Cryptography.Rijndael></xref:System.Security.Cryptography.Rijndael>   
 [Servizi di crittografia](http://msdn.microsoft.com/library/f96284bc-7b73-44b5-ac59-fac613ad09f8)
