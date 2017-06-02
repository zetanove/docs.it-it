---
title: "Esempio di tecnologia IXmlSerializable dei servizi Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0202d3f1-a50b-427d-a5bb-79208b8f1c22
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Esempio di tecnologia IXmlSerializable dei servizi Web
[Scarica esempio](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/IXmlSerializable.zip.exe)  
  
 In questo esempio viene illustrato come utilizzare l'oggetto <xref:System.Xml.Serialization.IXmlSerializable> per controllare la serializzazione dei tipi personalizzati nei servizi Web ASP.NET.  
  
### Per compilare l'esempio utilizzando Visual Studio  
  
1.  Aprire [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)], quindi scegliere **Nuovo sito Web** dal menu **File**.  
  
2.  Nel riquadro sinistro della finestra **Nuovo sito Web** scegliere il linguaggio di programmazione desiderato, quindi selezionare **Servizio Web ASP.NET** nel riquadro destro.  
  
3.  Digitare **IXmlSerializable** come nome del nuovo servizio Web.  
  
4.  In Esplora soluzioni fare clic con il pulsante destro del mouse sull'icona relativa a Service.asmx, quindi scegliere **Elimina**. Ripetere questa operazione per il file code\-behind Service.asmx.  
  
5.  Fare clic con il pulsante destro del mouse sulla directory del progetto, quindi scegliere **Aggiungi elemento esistente**.Nella finestra di dialogo spostarsi nella sottodirectory Service della directory specifica del linguaggio.  
  
6.  Fare clic su Service.asmx, quindi ripetere questa operazione per il file code\-behind Service.asmx.  
  
7.  Aprire [!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)], quindi passare alla directory contenente la directory IXmlSerializable creata nel passaggio 3 precedente.  
  
8.  Fare clic con il pulsante destro del mouse sull'icona relativa alla directory IXmlSerializable, quindi scegliere **Condivisione e sicurezza**.  
  
9. Nella scheda Condivisione Web selezionare **Condividi cartella** e confermare le impostazioni predefinite, incluso il nome IXmlSerializable.  
  
10. Scegliere **OK**.  
  
### Per eseguire l’esempio  
  
1.  Aprire una finestra del browser, quindi fare clic sulla barra degli indirizzi.  
  
2.  Digitare **http:\/\/localhost\/IXmlSerializable\/Service.asmx**.  
  
## Vedere anche  
 <xref:System.Xml.Serialization.IXmlSerializable>   
 <xref:System.Xml.Serialization>   
 <xref:System.Xml.XmlConvert>   
 <xref:System.Xml.XmlQualifiedName>   
 <xref:System.Xml.XmlReader>   
 <xref:System.Xml.Schema.XmlSchema>   
 <xref:System.Xml.Schema.XmlSchemaSet>   
 <xref:System.Xml.XmlUrlResolver>   
 <xref:System.Xml.XmlWriter>