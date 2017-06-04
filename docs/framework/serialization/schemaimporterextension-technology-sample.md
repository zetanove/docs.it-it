---
title: "Esempio di tecnologia SchemaImporterExtension | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f5eb78f-0ef6-433a-b095-3a63b1ce0bc9
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Esempio di tecnologia SchemaImporterExtension
[Scarica esempio](http://download.microsoft.com/download/4/7/B/47B2164C-E780-4B10-8DE4-2CB5B886E0A6/Technologies/Serialization/Xml%20Serialization/SchemaImporterExtension.zip.exe)  
  
 In questo esempio viene illustrato un oggetto <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> personalizzato che consente di eseguire un controllo accurato sulla generazione del codice durante l'importazione di uno schema XML.In particolare viene illustrato come compilare, registrare e richiamare tale estensione.  
  
### Per compilare l'esempio utilizzando il prompt dei comandi  
  
1.  Aprire una finestra del prompt dei comandi, quindi spostarsi in una delle sottodirectory specifiche del linguaggio relative all'esempio.  
  
2.  Digitare **msbuild.exe OrderSchemaImporterExtension.sln** dalla riga di comando.  
  
### Per compilare l'esempio utilizzando Visual Studio  
  
1.  Aprire [!INCLUDE[fileExplorer](../../../includes/fileexplorer-md.md)], quindi passare a una delle sottodirectory specifiche del linguaggio relative all'esempio.  
  
2.  Fare doppio clic sull'icona relativa a OrderSchemaImporterExtension.sln per aprire il file in Visual Studio.  
  
3.  Scegliere **Compila soluzione** dal menu **Compila**.  
  
 L'applicazione verrà compilata nella directory predefinita \\bin o \\bin\\Debug.  
  
### Per eseguire l’esempio  
  
1.  Spostarsi nella directory contenente il nuovo eseguibile, utilizzando il prompt dei comandi.  
  
2.  Digitare **\[nome file eseguibile\]** dalla riga di comando.  
  
## Osservazioni  
 Per ulteriori informazioni sulle fasi di registrazione e di creazione di file binari di esempio, vedere i commenti nei file di codice sorgente e build.proj.  
  
## Vedere anche  
 <xref:System.CodeDom.CodeCompileUnit>   
 <xref:System.CodeDom.CodeNamespace>   
 <xref:System.CodeDom.CodeNamespaceImport>   
 <xref:Microsoft.CSharp.CSharpCodeProvider>   
 <xref:System.Xml.Serialization.IXmlSerializable>   
 <xref:System.Xml.Serialization.Advanced.SchemaImporterExtension>   
 <xref:System.CodeDom>   
 <xref:System.CodeDom.Compiler>   
 <xref:System.Web.Services.Description>   
 <xref:System.Web.Services.Discovery>   
 <xref:System.Xml.Serialization>   
 <xref:System.Uri>   
 <xref:Microsoft.VisualBasic.VBCodeProvider>   
 <xref:System.Web.Services.Description.WebReference>   
 <xref:System.Xml.Serialization.XmlSchemaImporter>