---
title: "Tre categorie di servizi grafici | Microsoft Docs"
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
  - "grafica vettoriale bidimensionale"
  - "grafica, categorie"
  - "creazione di immagini"
  - "tipografia"
  - "immagini vettoriali"
ms.assetid: 068c0ef3-f6ee-4d58-a7b6-eb2531ead408
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Tre categorie di servizi grafici
I servizi grafici disponibili in Windows Form rientrano nelle tre ampie categorie descritte di seguito:  
  
-   Grafica vettoriale bidimensionale \(2D\)  
  
-   Immagini  
  
-   Opzioni tipografiche  
  
## Grafica vettoriale bidimensionale  
 La grafica vettoriale bidimensionale è composta da primitive, quali linee, curve e figure, specificate da un insieme di punti in un sistema di coordinate.  Ad esempio una linea retta è specificata tramite i due relativi punti finali e un rettangolo è specificato tramite un punto che ne rappresenta la posizione dell'angolo superiore sinistro e tramite un paio di numeri che ne indicano la larghezza e l'altezza.  Un percorso semplice è specificato tramite una matrice di punti da connettere con linee rette.  Una curva spline Bézier è una curva complessa, specificata tramite quattro punti di controllo.  
  
 In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] sono disponibili classi e strutture che consentono di memorizzare informazioni sulle primitive stesse, classi che consentono di memorizzare informazioni sulle procedure per tracciarle e classi che consentono di creare effettivamente il disegno.  Nella struttura <xref:System.Drawing.Rectangle>, ad esempio, sono memorizzate la posizione e le dimensioni di un rettangolo, nella classe <xref:System.Drawing.Pen> sono disponibili informazioni sul colore, lo spessore e lo stile della linea e nella classe <xref:System.Drawing.Graphics> sono infine memorizzati i metodi per tracciare linee, rettangoli, percorsi e altre figure.  Sono inoltre disponibili numerose classi <xref:System.Drawing.Brush> in cui vengono memorizzate informazioni relative alla modalità di riempimento di figure o percorsi chiusi con colori o motivi.  
  
 È possibile registrare un'immagine vettoriale \(una sequenza di comandi grafici\) in un metafile.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è fornita la classe <xref:System.Drawing.Imaging.Metafile> che consente la registrazione, la visualizzazione e il salvataggio di metafile.  Le classi <xref:System.Drawing.Imaging.MetafileHeader> e <xref:System.Drawing.Imaging.MetaHeader> consentono di esaminare i dati memorizzati nell'intestazione di un metafile.  
  
## Immagini  
 La visualizzazione di determinati tipi di immagini tramite le tecniche della grafica vettoriale risulta difficile o impossibile.  È ad esempio difficile specificare come raccolte di linee e curve le immagini dei pulsanti della barra degli strumenti e le immagini visualizzate come icone.  La creazione di una fotografia digitale ad alta risoluzione di uno stadio affollato tramite le tecniche vettoriali risulta ancora più complessa.  Le immagini di questo tipo vengono memorizzate come bitmap, matrici di numeri che rappresentano i colori di singoli punti sullo schermo.  In [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è fornita la classe <xref:System.Drawing.Bitmap> che consente la visualizzazione, la modifica e il salvataggio di bitmap.  
  
## Opzioni tipografiche  
 Le opzioni tipografiche riguardano la visualizzazione di testo in svariati tipi di carattere, dimensioni e stili.  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è disponibile un supporto completo per questa attività complessa.  Una delle nuove funzionalità offerte da [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] è l'anti\-aliasing dei subpixel, che conferisce un aspetto più uniforme al testo visualizzato su uno schermo a cristalli liquidi.  
  
 Inoltre, con Windows Form è possibile creare un testo con le funzionalità di [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] incluse nella classe <xref:System.Windows.Forms.TextRenderer>.  
  
## Vedere anche  
 [Cenni preliminari sulla grafica](../../../../docs/framework/winforms/advanced/graphics-overview-windows-forms.md)   
 [Informazioni sul codice gestito GDI\+](../../../../docs/framework/winforms/advanced/about-gdi-managed-code.md)   
 [Utilizzo di classi grafiche gestite](../../../../docs/framework/winforms/advanced/using-managed-graphics-classes.md)