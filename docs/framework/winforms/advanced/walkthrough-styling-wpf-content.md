---
title: "Procedura dettagliata: applicazione di stili al contenuto WPF | Microsoft Docs"
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
  - "interoperabilità [WDF]"
  - "stili, contenuto WPF"
  - "WPF (finestra di progettazione), applicazione di stili a contenuti WPF"
ms.assetid: e574aac7-7ea4-4cdb-8034-bab541f000df
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura dettagliata: applicazione di stili al contenuto WPF
Questa procedura dettagliata mostra come applicare uno stile a un controllo Windows Presentation Foundation \(WPF\) incluso in un Windows Form.  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   Creare il progetto.  
  
-   Creare il tipo di controllo WPF.  
  
-   Applicare uno stile al controllo WPF.  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma.  Per modificare le impostazioni, scegliere **Importa\/Esporta impostazioni** dal menu **Strumenti**.  Per altre informazioni, vedere [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/it-it/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## Prerequisiti  
 Per completare la procedura dettagliata, è necessario disporre dei componenti seguenti:  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)].  
  
## Creazione del progetto  
 Il primo passaggio consiste nella creazione del progetto Windows Form.  
  
> [!NOTE]
>  Con il contenuto WPF sono supportati solo progetti C\# e Visual Basic.  
  
#### Per creare il progetto  
  
-   Creare un nuovo progetto Windows Forms Application in Visual Basic o Visual C\# denominato `StylingWpfContent`.  
  
## Creazione di tipi di controllo WPF  
 Dopo avere aggiunto un tipo di controllo WPF al progetto, è possibile inserirlo in un controllo <xref:System.Windows.Forms.Integration.ElementHost>.  
  
#### Per creare i tipi di controllo WPF  
  
1.  Aggiungere un nuovo progetto WPF <xref:System.Windows.Controls.UserControl> alla soluzione.  Usare il nome predefinito per il tipo di controllo, `UserControl1.xaml`.  Per altre informazioni, vedere [Procedura dettagliata: creazione di nuovo contenuto WPF in Windows Form in fase di progettazione](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md).  
  
2.  In visualizzazione Progettazione verificare che `UserControl1` sia selezionato.  Per altre informazioni, vedere [Procedura: selezionare e spostare elementi sull'area di progettazione](http://msdn.microsoft.com/it-it/54cb70b6-b35b-46e4-a0cc-65189399c474).  
  
3.  Nella finestra **Proprietà** impostare il valore delle proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> su `200`.  
  
4.  Aggiungere un controllo <xref:System.Windows.Controls.Button?displayProperty=fullName> a <xref:System.Windows.Controls.UserControl> e impostare il valore della proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> su Cancel.  
  
5.  Aggiungere un secondo controllo <xref:System.Windows.Controls.Button?displayProperty=fullName> a <xref:System.Windows.Controls.UserControl> e impostare il valore della proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> su OK.  
  
6.  Compilare il progetto.  
  
## Applicazione di uno stile a un controllo WPF  
 È possibile applicare uno stile diverso a un controllo WPF per modificarne l'aspetto e il comportamento.  
  
#### Per applicare uno stile a un controllo WPF  
  
1.  Aprire `Form1` in Progettazione Windows Form.  
  
2.  Nella **Casella degli strumenti** fare doppio clic su `UserControl1` per creare un'istanza di `UserControl1` nel form.  
  
     L'istanza di `UserControl1` viene inclusa in un nuovo controllo <xref:System.Windows.Forms.Integration.ElementHost> denominato `elementHost1`.  
  
3.  Nel pannello smart tag per `elementHost1` fare clic su **Modifica contenuto ospitato** nell'elenco a discesa.  
  
     `UserControl1` si apre in [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
4.  Nella visualizzazione XAML inserire il seguente codice XAML dopo il tag di apertura `<UserControl>`.  
  
     Questo codice XAML crea una sfumatura con un bordo sfumato a contrasto.  Quando si fa clic sul controllo, le sfumature vengono modificate per generare l'aspetto di un pulsante premuto.  Per altre informazioni, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
```xaml  
<UserControl.Resources>  
    <LinearGradientBrush x:Key="NormalBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#FFF" Offset="0.0"/>  
        <GradientStop Color="#CCC" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="PressedBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#BBB" Offset="0.0"/>  
        <GradientStop Color="#EEE" Offset="0.1"/>  
        <GradientStop Color="#EEE" Offset="0.9"/>  
        <GradientStop Color="#FFF" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="NormalBorderBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#CCC" Offset="0.0"/>  
        <GradientStop Color="#444" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="BorderBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#CCC" Offset="0.0"/>  
        <GradientStop Color="#444" Offset="1.0"/>  
    </LinearGradientBrush>  
    <LinearGradientBrush x:Key="PressedBorderBrush" EndPoint="0,1" StartPoint="0,0">  
        <GradientStop Color="#444" Offset="0.0"/>  
        <GradientStop Color="#888" Offset="1.0"/>  
    </LinearGradientBrush>  
  
    <Style x:Key="SimpleButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">  
        <Setter Property="Background" Value="{StaticResource NormalBrush}"/>  
        <Setter Property="BorderBrush" Value="{StaticResource NormalBorderBrush}"/>  
        <Setter Property="Template">  
            <Setter.Value>  
                <ControlTemplate TargetType="{x:Type Button}">  
                    <Grid x:Name="Grid">  
                        <Border x:Name="Border" Background="{TemplateBinding Background}" BorderBrush="{TemplateBinding BorderBrush}" BorderThickness="{TemplateBinding BorderThickness}" Padding="{TemplateBinding Padding}"/>  
                        <ContentPresenter HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="{TemplateBinding Padding}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}" RecognizesAccessKey="True"/>  
                    </Grid>  
                    <ControlTemplate.Triggers>  
                        <Trigger Property="IsPressed" Value="true">  
                            <Setter Property="Background" Value="{StaticResource PressedBrush}" TargetName="Border"/>  
                            <Setter Property="BorderBrush" Value="{StaticResource PressedBorderBrush}" TargetName="Border"/>  
                        </Trigger>  
                    </ControlTemplate.Triggers>  
                </ControlTemplate>  
            </Setter.Value>  
        </Setter>  
    </Style>  
</UserControl.Resources>  
```  
  
1.  Applicare al pulsante Cancel lo stile `SimpleButton` definito nel passaggio precedente inserendo il seguente codice XAML nel tag `<Button>` del pulsante Cancel.  
  
    ```  
    Style="{StaticResource SimpleButton}  
    ```  
  
     La dichiarazione del pulsante sarà simile al seguente codice XAML.  
  
```xaml  
<Button Height="23" Margin="41,52,98,0" Name="button1" VerticalAlignment="Top"  
                Style="{StaticResource SimpleButton}">Cancel</Button>  
```  
  
1.  Compilare il progetto.  
  
2.  Aprire `Form1` in Progettazione Windows Form.  
  
3.  Il nuovo stile viene applicato al pulsante.  
  
4.  Per eseguire l'applicazione, scegliere **Avvia debug** dal menu **Debug**.  
  
5.  Fare clic sui pulsanti OK e Cancel e visualizzare le differenze.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Migrazione e interoperabilità](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [Utilizzo di controlli WPF](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)