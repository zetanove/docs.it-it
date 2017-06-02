---
title: "Cenni preliminari sulla grafica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "grafica, informazioni sulla grafica"
  - "grafica, mediante l'interfaccia gestita"
ms.assetid: a602aef8-a8c8-4c36-9816-74e7bad96a68
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Cenni preliminari sulla grafica
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è un'interfaccia API \(Application Programming Interface\) che costituisce il sottosistema del sistema operativo Microsoft Windows. [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è inoltre preposto alla visualizzazione di informazioni su schermi e stampanti.  Come suggerisce il nome, [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è il successore di [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)], ovvero le Graphics Device Interface incluse nelle versioni precedenti di Windows.  
  
## Interfaccia di classe gestita  
 L'API [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è esposta mediante un set di classi distribuito come codice gestito.  Tale set di classi è detto *interfaccia di classe gestita* di [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)].  Di seguito sono elencati gli spazi dei nomi che costituiscono l'interfaccia di classe gestita:  
  
-   <xref:System.Drawing>  
  
-   <xref:System.Drawing.Drawing2D>  
  
-   <xref:System.Drawing.Imaging>  
  
-   <xref:System.Drawing.Text>  
  
-   <xref:System.Drawing.Printing>  
  
 Con una Graphics Device Interface come [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)], è possibile visualizzare le informazioni su un monitor o una stampante senza preoccuparsi dei dettagli di un particolare dispositivo.  Il programmatore effettua chiamate ai metodi forniti dalle classi [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]. Tali metodi, a loro volta, effettuano le chiamate appropriate a specifici driver di dispositivo.  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] isola l'applicazione dall'hardware grafico. È questo isolamento che consente a un programmatore di creare applicazioni indipendenti dal dispositivo.  
  
## Vedere anche  
 [Cenni preliminari sulla grafica](../../../../docs/framework/winforms/advanced/graphics-overview-windows-forms.md)