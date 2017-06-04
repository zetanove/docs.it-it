---
title: "Procedura: determinare la versione installata di WPF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "versione, ricerca"
ms.assetid: 99971cef-e218-4f9f-a4c1-350332741860
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# Procedura: determinare la versione installata di WPF
Il numero di versione della versione corrente installata di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] si trova nel **Registro di sistema**.  
  
 Per individuare il numero di versione:  
  
1.  Fare clic sul pulsante **Start** e scegliere **Esegui**.  
  
2.  In **Apri**, digitare **regedit.exe**.  
  
3.  Aprire la chiave seguente:  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v3.0\Setup\Windows Presentation Foundation`  
  
 Il numero di versione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è archiviato nel valore **Versione**.