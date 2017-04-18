---
title: Valore checksum non valido, le cifre esadecimali non o un numero dispari di cifre esadecimali | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc42033
- vbc42033
dev_langs:
- VB
helpviewer_keywords:
- BC42033
ms.assetid: 4575554d-3615-46e4-9c6a-18e9c338e4ed
caps.latest.revision: 10
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
ms.openlocfilehash: bacb392b680bd236583ef6374f135678ed3304f3
ms.lasthandoff: 03/13/2017

---
# <a name="bad-checksum-value-non-hex-digits-or-odd-number-of-hex-digits"></a>Valore checksum non valido. Cifre esadecimali non presenti o in numero dispari
Un valore di checksum include cifre esadecimali non valide o un numero di cifre dispari.  
  
 Quando ASP.NET genera un file di origine Visual Basic, con estensione vb, calcola un checksum e lo colloca in un file di origine nascosto identificato da `#externalchecksum`. Anche un utente può generare un file con estensione vb per lo stesso scopo, ma questo processo è più adatto per essere usato internamente.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42033  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Se il file di origine Visual Basic viene generato da ASP.NET, riavviare la compilazione del progetto.  
  
2.  Se l'avviso persiste dopo il riavvio, reinstallare ASP.NET e riprovare a eseguire la compilazione.  
  
3.  Se l'avviso persiste ancora o non si usa ASP.NET, raccogliere informazioni sulla situazione contingente e informare il Servizio Supporto Tecnico Clienti Microsoft.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di ASP.NET](https://msdn.microsoft.com/library/4w3ex9c2.aspx)   
 [Comunicazioni con Microsoft](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
