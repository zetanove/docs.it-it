---
title: "Sicurezza dei controlli WebBrowser | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "sicurezza [Windows Form], WebBrowser (controllo)"
  - "WebBrowser (controllo) [Windows Form], sicurezza"
ms.assetid: 0968846e-48ee-485a-9797-65b5b9a622f8
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Sicurezza dei controlli WebBrowser
Il controllo <xref:System.Windows.Forms.WebBrowser> è progettato per il funzionamento nelle sole condizioni di attendibilità totale.  Il contenuto HTML visualizzato nel controllo può provenire da server Web esterni e può contenere codice non gestito sotto forma di script o controlli Web.  In questa situazione, il controllo <xref:System.Windows.Forms.WebBrowser> offre la stessa sicurezza di Internet Explorer. Tuttavia, il controllo <xref:System.Windows.Forms.WebBrowser> gestito non impedisce l'esecuzione di tale codice non gestito.  
  
 Per ulteriori informazioni sui problemi di sicurezza relativi al controllo ActiveX `WebBrowser` sottostante, vedere [Controllo WebBrowser](http://go.microsoft.com/fwlink/?LinkId=198812).  
  
## Vedere anche  
 <xref:System.Windows.Forms.WebBrowser>   
 [Cenni preliminari sul controllo WebBrowser](../../../../docs/framework/winforms/controls/webbrowser-control-overview.md)   
 [Controllo WebBrowser](http://go.microsoft.com/fwlink/?LinkId=198812)