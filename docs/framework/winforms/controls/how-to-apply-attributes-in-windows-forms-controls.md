---
title: "Procedura: applicare attributi nei controlli Windows Form | Microsoft Docs"
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
  - "attributi [Windows Form], applicazione"
  - "controlli [Windows Form], applicazione di attributi"
  - "controlli Windows Form, applicazione di attributi"
ms.assetid: af0a3f7f-155b-4ba1-83c4-9cf721331a06
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: applicare attributi nei controlli Windows Form
Per sviluppare componenti e controlli che interagiscano con l'ambiente di progettazione e vengano eseguiti correttamente, è necessario applicare gli attributi correttamente alle classi e ai membri.  
  
## Esempio  
 Nel codice di esempio seguente viene illustrato come utilizzare diversi attributi con un controllo personalizzato.  Il controllo rappresenta una funzionalità di registrazione semplice.  Quando il controllo è associato a un'origine dati, visualizza i valori inviati dall'origine in un controllo <xref:System.Windows.Forms.DataGridView>.  Se un valore eccede quello specificato dalla proprietà `Threshold`, viene generato un evento `ThresholdExceeded`.  
  
 `AttributesDemoControl` registra i valori con una classe `LogEntry`.  La classe `LogEntry` è una classe template, ovvero contiene parametri per il tipo che registra.  Ad esempio, se `AttributesDemoControl` registra valori di tipo `float`, ciascuna istanza `LogEntry` viene dichiarata e utilizzata nel modo seguente.  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/form1.cs#110)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/form1.vb#110)]  
  
> [!NOTE]
>  Poiché la classe `LogEntry` contiene parametri per un tipo arbitrario, deve utilizzare la reflection per funzionare con il tipo di parametro.  Affinché la funzionalità di soglia funzioni, il tipo di parametro `T` deve implementare l'interfaccia <xref:System.IComparable>.  
  
 Il form che contiene `AttributesDemoControl` interroga un contatore delle prestazioni regolarmente.  Ogni valore viene inserito in una classe `LogEntry` del tipo appropriato e aggiunto alla classe <xref:System.Windows.Forms.BindingSource> del form.  `AttributesDemoControl` riceve il valore tramite l'associazione dati e lo visualizza in un controllo <xref:System.Windows.Forms.DataGridView>.  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#1)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#1)]  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/form1.cs#100)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/form1.vb#100)]  
  
 Il primo esempio di codice è l'implementazione di `AttributesDemoControl`.  Nel secondo esempio di codice viene illustrato un form che utilizza `AttributesDemoControl`.  
  
## Attributi a livello di classe  
 Alcuni attributi vengono applicati a livello di classe.  Nell'esempio di codice seguente vengono illustrati gli attributi comunemente applicati a un controllo Windows Form.  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#20)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#20)]  
  
### Attributo TypeConverter  
 <xref:System.ComponentModel.TypeConverterAttribute> è un altro attributo a livello di classe di uso comune.  Nell'esempio di codice seguente viene illustrato l'utilizzo della classe `LogEntry`.  In questo esempio viene descritta l'implementazione di una classe <xref:System.ComponentModel.TypeConverter> per il tipo `LogEntry`, detta `LogEntryTypeConverter`.  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#5)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#5)]  
  
## Attributi a livello di membro  
 Alcuni attributi vengono applicati a livello di membro.  Negli esempi di codice seguenti vengono illustrati alcuni attributi comunemente applicati alle proprietà dei controlli Windows Form.  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#21)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#21)]  
  
### Attributo AmbientValue  
 Nell'esempio seguente vengono illustrati la classe <xref:System.ComponentModel.AmbientValueAttribute> e il codice che ne supporta l'interazione con l'ambiente di progettazione.  Tale interazione è detta *ambiente*.  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#23)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#23)]  
  
### Attributi Databinding  
 Negli esempi seguenti viene illustrata l'implementazione dell'associazione dati complessa.  La classe <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>, illustrata precedentemente, specifica le proprietà `DataSource` e `DataMember` da utilizzare per l'associazione dati.  La classe <xref:System.ComponentModel.AttributeProviderAttribute> specifica il tipo a cui verrà associata la proprietà `DataSource`.  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#25](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#25)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#25](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#25)]  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#26](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#26)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#26](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#26)]  
  
## Compilazione del codice  
  
-   Il form che contiene `AttributesDemoControl` richiede un riferimento all'assembly `AttributesDemoControl` per la compilazione.  
  
## Vedere anche  
 <xref:System.IComparable>   
 <xref:System.Windows.Forms.DataGridView>   
 [Sviluppo di controlli Windows Form personalizzati con .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [Attributi nei controlli Windows Form](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)   
 [How to: Serialize Collections of Standard Types with the DesignerSerializationVisibilityAttribute](../Topic/How%20to:%20Serialize%20Collections%20of%20Standard%20Types%20with%20the%20DesignerSerializationVisibilityAttribute.md)