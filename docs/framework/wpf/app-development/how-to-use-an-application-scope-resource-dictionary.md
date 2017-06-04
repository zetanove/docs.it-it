---
title: "Procedura: utilizzare un dizionario risorse relativo all&#39;ambito dell&#39;applicazione | Microsoft Docs"
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
  - "dizionari di risorse dell'ambito dell'applicazione"
  - "dizionari, risorsa"
  - "dizionari di risorse, ambito dell'applicazione"
ms.assetid: 53857682-bd2c-4f2c-8f25-1307d0b451a2
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: utilizzare un dizionario risorse relativo all&#39;ambito dell&#39;applicazione
In questo esempio viene illustrato come definire e utilizzare un dizionario risorse personalizzato relativo all'ambito dell'applicazione.  
  
## Esempio  
 <xref:System.Windows.Application> espone un archivio relativo all'ambito dell'applicazione per le risorse condivise: <xref:System.Windows.Application.Resources%2A>.  Per impostazione predefinita, la proprietà <xref:System.Windows.Application.Resources%2A> viene inizializzata con un'istanza del tipo <xref:System.Windows.ResourceDictionary>.  Utilizzare questa istanza quando si ottengono e si impostano proprietà relative all'ambito dell'applicazione utilizzando <xref:System.Windows.Application.Resources%2A>.  Per ulteriori informazioni, vedere [How to: Get and Set an Application\-Scope Resource](http://msdn.microsoft.com/it-it/39e0420c-c9fc-47dc-8956-fdd95b214095).  
  
 Se si dispone di più risorse impostate tramite la proprietà <xref:System.Windows.Application.Resources%2A>, è invece possibile utilizzare un dizionario risorse personalizzato per archiviare tali risorse e impostare con esso <xref:System.Windows.Application.Resources%2A>.  Di seguito viene illustrato come dichiarare un dizionario risorse personalizzato utilizzando XAML.  
  
 [!code-xml[HOWTOResourceDictionaries#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MyResourceDictionary.xaml#1)]  
  
 Lo scambio di interi dizionari risorse tramite <xref:System.Windows.Application.Resources%2A> consente di supportare temi relativi all'ambito dell'applicazione, dove ogni tema è incapsulato da un singolo dizionario risorse.  Nell'esempio riportato di seguito viene illustrato come impostare l'oggetto <xref:System.Windows.ResourceDictionary>.  
  
 [!code-xml[HOWTOResourceDictionaries#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/App.xaml#2)]  
  
 Di seguito viene illustrato come è possibile ottenere risorse relative all'ambito dell'applicazione dal dizionario risorse esposto da <xref:System.Windows.Application.Resources%2A> nel codice XAML.  
  
 [!code-xml[HOWTOResourceDictionaries#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MainWindow.xaml#4)]  
  
 Di seguito viene illustrato come è inoltre possibile ottenere le risorse nel codice.  
  
 [!code-csharp[HOWTOResourceDictionaries#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToResourceDictionaries/CSharp/MainWindow.xaml.cs#3)]
 [!code-vb[HOWTOResourceDictionaries#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToResourceDictionaries/VB/MainWindow.xaml.vb#3)]  
  
 Quando si utilizza la proprietà <xref:System.Windows.Application.Resources%2A>, è necessario considerare due aspetti.  Innanzitutto, la *chiave* del dizionario è un oggetto, pertanto è necessario utilizzare esattamente la stessa istanza dell'oggetto sia quando si imposta un valore di proprietà, sia quando lo si ottiene.  Si noti che la chiave rileva la differenza tra maiuscole e minuscole quando si utilizza una stringa. Secondariamente, il *valore* del dizionario è un oggetto, pertanto sarà necessario convertire il valore nel tipo desiderato quando si ottiene un valore di proprietà.  
  
## Vedere anche  
 <xref:System.Windows.ResourceDictionary>   
 <xref:System.Windows.Application.Resources%2A>   
 [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [Dizionari risorse uniti](../../../../docs/framework/wpf/advanced/merged-resource-dictionaries.md)