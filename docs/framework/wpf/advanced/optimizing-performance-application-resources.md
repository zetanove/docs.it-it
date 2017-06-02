---
title: "Ottimizzazione delle prestazioni: risorse di applicazioni | Microsoft Docs"
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
  - "risorse delle applicazioni, prestazioni"
  - "pennelli, prestazioni"
  - "risorse, prestazioni"
  - "condivisione di pennelli senza copia"
  - "condivisione di risorse"
  - "risorse statiche"
ms.assetid: 62b88488-c08e-4804-b7de-a1c34fbe929c
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Ottimizzazione delle prestazioni: risorse di applicazioni
In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è possibile condividere risorse di applicazioni per garantire un aspetto o un comportamento coerente in elementi di tipi simili.  In questo argomento vengono forniti alcuni consigli che possono agevolare il miglioramento delle prestazioni delle applicazioni.  
  
 Per ulteriori informazioni sulle risorse, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
## Condivisione delle risorse  
 Se nell'applicazione vengono utilizzati controlli personalizzati e vengono definite risorse in un oggetto <xref:System.Windows.ResourceDictionary> \(o nodo di risorse XAML\), è consigliabile definire le risorse a livello dell'oggetto <xref:System.Windows.Application> o <xref:System.Windows.Window> oppure definirle nel tema predefinito per i controlli personalizzati.  La definizione delle risorse nell'oggetto <xref:System.Windows.ResourceDictionary> di un controllo personalizzato comporta un impatto sulle prestazioni per ogni istanza di tale controllo.  Ad esempio, se sono presenti operazioni di pennello che richiedono prestazioni elevate definite come parte della definizione delle risorse di un controllo personalizzato e numerose istanze del controllo personalizzato, il working set dell'applicazione aumenta in misura significativa.  
  
 Per illustrare questo punto, si consideri quanto segue.  Si supponga di sviluppare un gioco di carte tramite [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Nella maggior parte dei giochi di carte, sono necessarie 52 carte con 52 facce diverse.  Si decide di implementare un controllo personalizzato delle carte e si definiscono 52 pennelli \(ognuno dei quali rappresenta una faccia delle carte\) nelle risorse del controllo personalizzato delle carte.  Nell'applicazione principale, si creano inizialmente 52 istanze di tale controllo personalizzato.  Ogni istanza del controllo personalizzato delle carte genera 52 istanze di oggetti <xref:System.Windows.Media.Brush>, per un totale di 52 \* 52 oggetti <xref:System.Windows.Media.Brush> nell'applicazione.  Spostando i pennelli all'esterno delle risorse del controllo personalizzato delle carte, a livello dell'oggetto <xref:System.Windows.Application> o <xref:System.Windows.Window>, oppure definendole nel tema predefinito del controllo personalizzato, si riduce il working set dell'applicazione, poiché si condividono i 52 pennelli tra 52 istanze del controllo delle carte.  
  
## Condivisione di un pennello senza copia  
 Se sono presenti più elementi che utilizzano lo stesso oggetto <xref:System.Windows.Media.Brush>, definire il pennello come risorsa e fare riferimento a esso, anziché definire il pennello inline in [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)].  Con questo metodo viene creata un'istanza che è possibile riutilizzare, mentre con la definizione di pennelli inline in [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] viene creata una nuova istanza per ogni elemento.  
  
 Nell'esempio di markup riportato di seguito viene illustrato questo punto:  
  
 [!code-xml[Performance#PerformanceSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/BrushResource.xaml#performancesnippet7)]  
  
## Utilizzare risorse statiche quando possibile  
 Una risorsa statica fornisce un valore per qualsiasi attributo di proprietà XAML eseguendo la ricerca di un riferimento a una risorsa già definita.  Il comportamento di ricerca per tale risorsa è analogo alla ricerca in fase di compilazione.  
  
 Con una risorsa dinamica, invece, viene creata un'espressione temporanea durante la compilazione iniziale, e la ricerca delle risorse viene rinviata finché il valore della risorsa richiesta non risulta effettivamente necessario per costruire un oggetto.  Il comportamento di ricerca per tale risorsa è analogo alla ricerca in fase di esecuzione, che comporta un impatto sulle prestazioni.  Quando possibile, utilizzare risorse statiche nell'applicazione, limitando l'utilizzo delle risorse dinamiche solo ai casi in cui è necessario.  
  
 Nell'esempio di markup riportato di seguito viene illustrato l'utilizzo di entrambi i tipi di risorse:  
  
 [!code-xml[Performance#PerformanceSnippet8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/DynamicResource.xaml#performancesnippet8)]  
  
## Vedere anche  
 [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Pianificazione delle prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Sfruttare appieno l'hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Comportamento dell'oggetto](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)