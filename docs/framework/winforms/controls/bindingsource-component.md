---
title: "Il componente BindingSource | Microsoft Docs"
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
  - "BindingSource (componente) [Windows Form]"
  - "associazione dati, Windows Form"
  - "Windows Form, associazione di controlli a dati"
ms.assetid: 3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Il componente BindingSource
Encapsulates a data source for binding to controls.  
  
 Il componente <xref:System.Windows.Forms.BindingSource> ha due scopi.  Innanzitutto fornisce un livello di riferimento indiretto durante il binding dei controlli di un form ai dati.  Questo si ottiene associando il componente <xref:System.Windows.Forms.BindingSource> all'origine dati e quindi associando i controlli del form al componente <xref:System.Windows.Forms.BindingSource>.  Tutte le altre interazioni con i dati, tra cui l'esplorazione, l'ordinamento, il filtro e l'aggiornamento, vengono eseguite mediante chiamate al componente <xref:System.Windows.Forms.BindingSource>.  
  
 In secondo luogo, il componente <xref:System.Windows.Forms.BindingSource> può fungere da origine dati fortemente tipizzata.  Aggiungendo un tipo al componente <xref:System.Windows.Forms.BindingSource> con il metodo <xref:System.Windows.Forms.BindingSource.Add%2A>, viene creato un elenco di tale tipo.  
  
## In questa sezione  
 [Cenni preliminari sul componente BindingSource](../../../../docs/framework/winforms/controls/bindingsource-component-overview.md)  
 Introduce i concetti generali del componente <xref:System.Windows.Forms.BindingSource>, che consente di associare un'origine dati a un controllo.  
  
 [Procedura: associare controlli Windows Form a valori di database DBNull](../../../../docs/framework/winforms/controls/how-to-bind-windows-forms-controls-to-dbnull-database-values.md)  
 Mostra come gestire un valore <xref:System.DBNull> dell'origine dati con il componente <xref:System.Windows.Forms.BindingSource>.  
  
 [Procedura: ordinare e filtrare i dati ADO.NET con il componente BindingSource Windows Form](../../../../docs/framework/winforms/controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)  
 Illustra l'uso del componente <xref:System.Windows.Forms.BindingSource> per applicare criteri di ordinamento e filtri ai dati visualizzati.  
  
 [Procedura: eseguire l'associazione a un servizio Web utilizzando il BindingSource Windows Form](../../../../docs/framework/winforms/controls/how-to-bind-to-a-web-service-using-the-windows-forms-bindingsource.md)  
 Mostra come usare il componente <xref:System.Windows.Forms.BindingSource> per eseguire il binding a un servizio Web.  
  
 [Procedura: gestire gli errori e le eccezioni che si verificano con l'associazione dati](../../../../docs/framework/winforms/controls/how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)  
 Illustra l'uso del componente <xref:System.Windows.Forms.BindingSource> per gestire normalmente gli errori che si verificano in un'operazione di data binding.  
  
 [Procedura: associare un controllo Windows Form a un tipo](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)  
 Illustra l'uso di un componente <xref:System.Windows.Forms.BindingSource> per eseguire il binding a un tipo.  
  
 [Procedura: associare un controllo Windows Form a un oggetto Factory](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-factory-object.md)  
 Illustra l'uso di un componente <xref:System.Windows.Forms.BindingSource> per eseguire il binding a un oggetto o metodo factory.  
  
 [Procedura: personalizzare l'aggiunta di elementi con BindingSource Windows Form](../../../../docs/framework/winforms/controls/how-to-customize-item-addition-with-the-windows-forms-bindingsource.md)  
 Illustra l'uso di un componente <xref:System.Windows.Forms.BindingSource> per creare nuovi elementi e aggiungerli a un'origine dati.  
  
 [Procedura: generare notifiche di modifica utilizzando il metodo ResetItem di BindingSource](../../../../docs/framework/winforms/controls/how-to-raise-change-notifications-using-the-bindingsource-resetitem-method.md)  
 Illustra l'uso di un componente <xref:System.Windows.Forms.BindingSource> per generare eventi di notifica di modifica per le origini dati che non supportano la notifica di modifica.  
  
 [Procedura: generare notifiche di modifica utilizzando un BindingSource e l'interfaccia INotifyPropertyChanged](../../../../docs/framework/winforms/controls/raise-change-notifications--bindingsource.md)  
 Illustra come usare un tipo che eredita da <xref:System.ComponentModel.INotifyPropertyChanged> con un controllo <xref:System.Windows.Forms.BindingSource>.  
  
 [Procedura: riflettere gli aggiornamenti dell'origine dati in un controllo Windows Form con BindingSource](../../../../docs/framework/winforms/controls/reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)  
 Illustra come rispondere alle modifiche nell'origine dati con il componente <xref:System.Windows.Forms.BindingSource>.  
  
 [Procedura: condividere dati associati tra form tramite il componente BindingSource](../../../../docs/framework/winforms/controls/how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)  
 Mostra come usare <xref:System.Windows.Forms.BindingSource> per associare più form alla stessa origine dati.  
  
## Riferimenti  
 <xref:System.Windows.Forms.BindingSource>  
 Fornisce la documentazione di riferimento per il componente <xref:System.Windows.Forms.BindingSource>.  
  
 <xref:System.Windows.Forms.BindingNavigator>  
 Fornisce la documentazione di riferimento per il controllo <xref:System.Windows.Forms.BindingNavigator>.  
  
## Sezioni correlate  
 [Associazione ai dati di Windows Form](../../../../docs/framework/winforms/windows-forms-data-binding.md)  
 Contiene i collegamenti agli argomenti che descrivono l'architettura di data binding di Windows Form.  
  
 Vedere anche [Associazione di controlli ai dati in Visual Studio](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)