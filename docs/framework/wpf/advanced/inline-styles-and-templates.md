---
title: "Stili e modelli inline | Microsoft Docs"
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
  - "stili inline"
  - "inline (modelli)"
  - "stili, inline"
  - "modelli, inline"
ms.assetid: 69a1a3f9-acb5-4e2c-9c43-2e376c055ac4
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Stili e modelli inline
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce oggetti <xref:System.Windows.Style> e oggetti modello \(sottoclassi<xref:System.Windows.FrameworkTemplate> \) per definire l'aspetto visivo di un elemento nelle risorse, in modo da renderne possibile il riutilizzo.  Per questa ragione, gli attributi di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che accettano i tipi <xref:System.Windows.Style> e <xref:System.Windows.FrameworkTemplate> creano quasi sempre dei riferimenti alle risorse per gli stili e i modelli esistenti piuttosto che definirne di nuovi inline.  
  
## Limitazioni degli stili e dei modelli inline  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], le proprietà di stili e modelli possono essere impostate tecnicamente in due modi.  È possibile utilizzare la sintassi per attributi per fare riferimento a uno stile definito all'interno di una risorsa, ad esempio `<`*oggetto*`Style="{StaticResource`*myResourceKey*`}" .../>`.  Oppure è possibile utilizzare la sintassi per elementi proprietà per definire uno stile inline, ad esempio:  
  
 `<` *object* `>`  
  
 `<` *object* `.Style>`  
  
 `<` `Style`  `.../>`  
  
 `</` *object* `.Style>`  
  
 `</` *object* `>`  
  
 L'utilizzo dell'attributo è molto più comune.  Uno stile definito inline e non definito nelle risorse è necessariamente limitato unicamente all'elemento contenitore e non può essere utilizzato nuovamente in modo semplice in quanto non dispone di chiavi di risorsa.  In generale, un stile definito nelle risorse è più versatile e utile oltre a essere più conforme al principio di modello di programmazione di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] che prevede la separazione della logica di programma nel codice dalla progettazione nel markup.  
  
 Di solito non esiste alcuna ragione per la quale impostare uno stile o un modello inline, anche se si intende solo utilizzare quello stile o quel modello in quella posizione.  La maggior parte degli elementi che possono accettare un stile o un modello supporta anche una proprietà di contenuto e un modello di contenuto.  Se si utilizza la struttura ad albero logica creata aggiungendo stili o modelli una sola volta, sarà persino più facile riempire semplicemente quella proprietà di contenuto con gli elementi figlio equivalenti nel markup diretto.  In tal modo i meccanismi relativi agli stili e ai modelli verrebbero completamente ignorati.  
  
 Per gli stili e i modelli è inoltre possibile utilizzare altre sintassi abilitate dalle estensioni di markup che restituiscono un oggetto.  Due tra queste estensioni che dispongono di scenari possibili includono [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) e <xref:System.Windows.Data.Binding>.  
  
## Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)