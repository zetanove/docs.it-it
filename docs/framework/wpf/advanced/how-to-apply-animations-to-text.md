---
title: "Procedura: applicare animazioni al testo | Microsoft Docs"
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
  - "animazione, testo"
  - "tipografia, animazioni"
ms.assetid: eec3d26c-0a21-420f-8012-671621c47089
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: applicare animazioni al testo
Le animazioni possono modificare la visualizzazione e l'aspetto del testo nell'applicazione.  Negli esempi seguenti vengono utilizzati tipi diversi di animazioni per influire sulla visualizzazione del testo in un controllo <xref:System.Windows.Controls.TextBlock>.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> per aggiungere un'animazione alla larghezza del blocco di testo.  Il valore di larghezza viene modificato dalla larghezza del blocco di testo a 0 per una durata pari a 10 secondi, quindi inverte i valori di larghezza e continua.  Questo tipo di animazione crea un effetto a comparsa.  
  
 [!code-xml[TextAnimationSample#TextAnimationSample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample1)]  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> per aggiungere un'animazione all'opacità del blocco di testo.  Il valore di opacità viene modificato da 1,0 a 0 per una durata pari a 5 secondi, quindi inverte i valori di opacità e continua.  
  
 [!code-xml[TextAnimationSample#TextAnimationSample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample2)]  
  
 Nel diagramma seguente viene illustrato l'effetto del controllo <xref:System.Windows.Controls.TextBlock> per cui l'opacità viene modificata da `1.00` a `0.00` in un intervallo pari a 5 secondi definito da <xref:System.Windows.Media.Animation.Timeline.Duration%2A>.  
  
 ![Testo con modifica di opacità da 1.00 a 0.00](../../../../docs/framework/wpf/advanced/media/fadedtext01.png "FadedText01")  
Opacità del testo modificata da 1,00 a 0,00  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Animation.ColorAnimation> per aggiungere un'animazione al colore di primo piano del blocco di testo.  Il valore del colore di primo piano viene modificato da un colore a un altro per una durata pari a 5 secondi, quindi inverte i valori del colore e continua.  
  
 [!code-xml[TextAnimationSample#TextAnimationSample3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample3)]  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> per ruotare il blocco di testo.  Il blocco di testo esegue una rotazione completa per una durata pari a 20 secondi, quindi continua a ripetere la rotazione.  
  
 [!code-xml[TextAnimationSample#TextAnimationSample4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextAnimationSample/CS/Window1.xaml#textanimationsample4)]  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)