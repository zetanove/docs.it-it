---
title: "Procedura dettagliata: creazione di un pulsante tramite XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pulsanti"
ms.assetid: 138c41c4-1759-4bbf-8d77-77031a06a8a0
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura dettagliata: creazione di un pulsante tramite XAML
L'obiettivo di questa procedura dettagliata è quello di imparare a creare un pulsante animato per un'applicazione [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)].  In questa procedura dettagliata vengono utilizzati stili e un modello per creare una risorsa pulsante personalizzato per riutilizzare il codice e separare la logica del pulsante dalla dichiarazione dello stesso.  Questa procedura dettagliata è scritta interamente in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
> [!IMPORTANT]
>  In questa procedura dettagliata vengono illustrati i passaggi da eseguire per creare l'applicazione digitando oppure copiando e incollando [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] in Microsoft [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  Se si desidera imparare a utilizzare uno strumento di progettazione \(Microsoft Expression Blend\) per creare la stessa applicazione, vedere la [Creare un pulsante tramite Microsoft Expression Blend](../../../../docs/framework/wpf/controls/walkthrough-create-a-button-by-using-microsoft-expression-blend.md).  
  
 Nella figura riportata di seguito vengono illustrati i pulsanti finiti.  
  
 ![Pulsanti personalizzati creati usando XAML](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-5.png "custom\_button\_AnimatedButton\_5")  
  
## Creare i pulsanti di base  
 Creare innanzitutto un nuovo progetto e aggiungere alcuni pulsanti alla finestra.  
  
#### Per creare un nuovo progetto WPF e aggiungere pulsanti alla finestra  
  
1.  Avviare[!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  
  
2.  **Creare un nuovo progetto WPF:** scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  Tovare il modello Find the **Applicazione Windows \(WPF\)** e aasegnare al progetto il nome "AnimatedButton".  In questo modo, si crea la struttura base dell'applicazione.  
  
3.  **Aggiungere i pulsanti predefiniti di base:** tutti i file necessari per questa procedura dettagliata vengono forniti dal modello.  Aprire il file Window1.xaml facendo doppio clic su di esso in Esplora soluzioni.  Per impostazione predefinita, è presente un elemento <xref:System.Windows.Controls.Grid> in Window1.xaml.  Rimuovere l'elemento <xref:System.Windows.Controls.Grid> e aggiungere alcuni pulsanti alla pagina [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] digitando oppure copiando e incollando il codice evidenziato seguente in Window1.xaml:  
  
    ```  
    <Window x:Class="AnimatedButton.Window1"  
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
      Title="AnimatedButton" Height="300" Width="300"   
      Background="Black">  
  
      <!-- Buttons arranged vertically inside a StackPanel. -->  
      <StackPanel HorizontalAlignment="Left">  
        <Button>Button 1</Button>  
        <Button>Button 2</Button>  
        <Button>Button 3</Button>  
      </StackPanel>  
  
    </Window>  
    ```  
  
     Premere F5 per eseguire l'applicazione. Dovrebbero essere visibili i pulsanti simili a quelli illustrati nella figura riportata di seguito.  
  
     ![Tre pulsanti di base](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-1.png "custom\_button\_AnimatedButton\_1")  
  
     Dopo avere creato i pulsanti di base, il file Window1.xaml non è più necessario.  Il resto della procedura dettagliata richiede l'utilizzo del file app.xaml per la definizione di stili e di un modello per i pulsanti.  
  
## Impostare le proprietà di base  
 È a questo punto necessario impostare alcune proprietà su questi pulsanti per controllarne l'aspetto e il layout.  Anziché impostare le proprietà per i singoli pulsanti, si utilizzeranno le risorse per definire le proprietà dei pulsanti per l'intera applicazione.  Le risorse dell'applicazione sono concettualmente simili al [!INCLUDE[TLA#tla_css](../../../../includes/tlasharptla-css-md.md)] esterno per le pagine Web; esse sono, tuttavia, molto più funzionali rispetto al [!INCLUDE[TLA#tla_css](../../../../includes/tlasharptla-css-md.md)], come si vedrà verso la fine di questa procedura dettagliata.  Per ulteriori informazioni sulle risorse, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
#### Per utilizzare gli stili per impostare le proprietà di base per i pulsanti  
  
1.  **Definire un blocco Application.Resources:** aprire app.xaml e aggiungere il markup evidenziato seguente se non ancora presente:  
  
    ```  
    <Application x:Class="AnimatedButton.App"  
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
      StartupUri="Window1.xaml"  
      >  
      <Application.Resources>  
  
        <!-- Resources for the entire application can be   
             defined here. -->  
  
      </Application.Resources>  
    </Application>  
    ```  
  
     L'ambito di una risorsa dipende dalla posizione in cui la stessa viene definita.  La definizione delle risorse nel blocco `Application.Resoureses` del file app.xaml consente di utilizzare la risorsa da qualsiasi punto dell'applicazione.  Per ulteriori informazioni sulla definizione dell'ambito delle risorse, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
2.  **Creare uno stile e definire i valori delle proprietà di base:** aggiungere il markup seguente al blocco `Application.Resources`.  Questo markup consente di creare un oggetto <xref:System.Windows.Style> da applicare a tutti i pulsanti dell'applicazione, impostando la proprietà <xref:System.Windows.FrameworkElement.Width%2A> dei pulsanti su 90 e la proprietà <xref:System.Windows.FrameworkElement.Margin%2A> su 10:  
  
    ```  
    <Application.Resources>  
  
      <Style TargetType="Button">  
        <Setter Property="Width" Value="90" />  
        <Setter Property="Margin" Value="10" />  
      </Style>  
  
    </Application.Resources>  
    ```  
  
     La proprietà <xref:System.Windows.Style.TargetType%2A> consente di specificare che lo stile è applicabile a tutti gli oggetti di tipo <xref:System.Windows.Controls.Button>.  Ogni oggetto <xref:System.Windows.Setter> imposta un valore di proprietà diverso per l'oggetto <xref:System.Windows.Style>.  Pertanto, ogni pulsante dell'applicazione presenta una larghezza di 90 e un margine di 10.  Se si preme F5 per eseguire l'applicazione, verrà visualizzata la finestra seguente.  
  
     ![Pulsanti con una larghezza di 90 e un margine di 10](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-2.png "custom\_button\_AnimatedButton\_2")  
  
     Gli stili possono rivelarsi utili in molti altri contesti, ad esempio possono essere utilizzati per definire gli oggetti di destinazione, specificando valori di proprietà complessi, ed essere utilizzati come input di altri stili.  Per ulteriori informazioni, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
3.  **Impostare un valore di una proprietà di stile su una risorsa:** le risorse consentono di riutilizzare con facilità valori e oggetti comunemente definiti.  È particolarmente utile definire valori complessi utilizzando le risorse per rendere il codice più modulare.  Aggiungere il markup evidenziato seguente al file app.xaml.  
  
    ```  
    <Application.Resources>  
  
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"   
        StartPoint="0,0" EndPoint="1,1">  
        <GradientStop Color="DarkGray" Offset="0" />  
        <GradientStop Color="#CCCCFF" Offset="0.5" />  
        <GradientStop Color="DarkGray" Offset="1" />  
      </LinearGradientBrush>  
  
      <Style TargetType="{x:Type Button}">  
        <Setter Property="Background"   
          Value="{StaticResource GrayBlueGradientBrush}" />  
        <Setter Property="Width" Value="80" />  
        <Setter Property="Margin" Value="10" />  
      </Style>  
  
    </Application.Resources>  
    ```  
  
     Direttamente sotto il blocco `Application.Resources`, è stata creata una risorsa denominata "GrayBlueGradientBrush".  Questa risorsa definisce una sfumatura orizzontale.  Questa risorsa può essere utilizzata come un valore di proprietà da qualsiasi punto dell'applicazione, anche all'interno del metodo di impostazione dello stile del pulsante per la proprietà <xref:System.Windows.Controls.Control.Background%2A>.  Tutti i pulsanti presentano ora un valore della proprietà <xref:System.Windows.Controls.Control.Background%2A> di questa sfumatura.  
  
     ‎Premere F5 per eseguire l'applicazione.  Dovrebbe essere analoga alla seguente.  
  
     ![Pulsanti con uno sfondo sfumato](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-3.png "custom\_button\_AnimatedButton\_3")  
  
## Creare un modello che definisca l'aspetto di un pulsante  
 In questa sezione viene creato un modello per la personalizzazione dell'aspetto \(presentazione\) del pulsante.  La presentazione del pulsante è composta da diversi oggetti, inclusi i rettangoli e altri componenti per conferire al pulsante un aspetto unico.  
  
 Finora, il controllo dell'aspetto dei pulsanti dell'applicazione è stato limitato alla modifica delle relative proprietà.  È tuttavia possibile apportare modifiche più radicali all'aspetto dei pulsanti.  I modelli consentono un controllo maggiore sulla presentazione di un oggetto.  Poiché possono essere utilizzati all'interno degli stili, è possibile applicare i modelli a tutti gli oggetti a cui si applica lo stile \(in questa procedura dettagliata, il pulsante\).  
  
#### Per utilizzare il modello per definire l'aspetto del pulsante  
  
1.  **Impostare il modello:** poiché i controlli come <xref:System.Windows.Controls.Button> presentano una proprietà <xref:System.Windows.Controls.Control.Template%2A>, è possibile definire il valore della proprietà del modello proprio come gli altri valori di proprietà impostati in un oggetto <xref:System.Windows.Style> utilizzando <xref:System.Windows.Setter>.  Aggiungere il markup evidenziato seguente allo stile del pulsante.  
  
    ```  
    <Application.Resources>  
  
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"   
        StartPoint="0,0" EndPoint="1,1">  
        <GradientStop Color="DarkGray" Offset="0" />  
        <GradientStop Color="#CCCCFF" Offset="0.5" />  
        <GradientStop Color="DarkGray" Offset="1" />  
      </LinearGradientBrush>  
  
      <Style TargetType="{x:Type Button}">  
      <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />  
        <Setter Property="Width" Value="80" />  
        <Setter Property="Margin" Value="10" />  
        <Setter Property="Template">  
          <Setter.Value>  
            <!-- The button template is defined here. -->  
          </Setter.Value>  
        </Setter>  
      </Style>  
  
    </Application.Resources>  
    ```  
  
2.  **Alterare la presentazione del pulsante:** a questo punto, è necessario definire il modello.  Aggiungere il markup evidenziato riportato di seguito.  Questo markup specifica due elementi <xref:System.Windows.Shapes.Rectangle> con bordi arrotondati, seguiti da un <xref:System.Windows.Controls.DockPanel>.  L'oggetto <xref:System.Windows.Controls.DockPanel> viene utilizzato per ospitare l'oggetto <xref:System.Windows.Controls.ContentPresenter> del pulsante.  L'oggetto <xref:System.Windows.Controls.ContentPresenter> consente di visualizzare il contenuto del pulsante.  In questa procedura dettagliata il contenuto è costituito da testo \("Button 1", "Button 2", "Button 3"\).  Tutti i componenti del modello, ovvero il rettangolo e l'oggetto <xref:System.Windows.Controls.DockPanel>, vengono disposti all'interno di un oggetto <xref:System.Windows.Controls.Grid>.  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="Button">  
        <Grid Width="{TemplateBinding Width}"   
         Height="{TemplateBinding Height}" ClipToBounds="True">  
  
          <!-- Outer Rectangle with rounded corners. -->  
          <Rectangle x:Name="outerRectangle"   
            HorizontalAlignment="Stretch"   
            VerticalAlignment="Stretch"   
            Stroke="{TemplateBinding Background}"   
            RadiusX="20" RadiusY="20" StrokeThickness="5"   
            Fill="Transparent" />  
  
          <!-- Inner Rectangle with rounded corners. -->  
          <Rectangle x:Name="innerRectangle"   
            HorizontalAlignment="Stretch"   
            VerticalAlignment="Stretch" Stroke="Transparent"   
            StrokeThickness="20"   
            Fill="{TemplateBinding Background}"   
            RadiusX="20" RadiusY="20"   />  
  
          <!-- Present Content (text) of the button. -->  
          <DockPanel Name="myContentPresenterDockPanel">  
            <ContentPresenter x:Name="myContentPresenter" Margin="20"   
              Content="{TemplateBinding  Content}"   
              TextBlock.Foreground="Black" />  
          </DockPanel>  
        </Grid>  
      </ControlTemplate>  
    </Setter.Value>  
    ```  
  
     ‎Premere F5 per eseguire l'applicazione.  Dovrebbe essere analoga alla seguente.  
  
     ![](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-4.gif "custom\_button\_AnimatedButton\_4")  
  
3.  **Aggiungere un effetto cristallo al modello:** in seguito verrà aggiunto il cristallo.  Innanzitutto vengono create alcune risorse per la creazione di un effetto cristallo.  Aggiungere queste risorse sfumatura in qualsiasi punto del blocco `Application.Resources`:  
  
    ```  
    <Application.Resources>  
      <GradientStopCollection x:Key="MyGlassGradientStopsResource">  
        <GradientStop Color="WhiteSmoke" Offset="0.2" />  
        <GradientStop Color="Transparent" Offset="0.4" />  
        <GradientStop Color="WhiteSmoke" Offset="0.5" />  
        <GradientStop Color="Transparent" Offset="0.75" />  
        <GradientStop Color="WhiteSmoke" Offset="0.9" />  
        <GradientStop Color="Transparent" Offset="1" />  
      </GradientStopCollection>  
  
      <LinearGradientBrush x:Key="MyGlassBrushResource"   
       StartPoint="0,0" EndPoint="1,1" Opacity="0.75"   
       GradientStops="{StaticResource MyGlassGradientStopsResource}" />  
    <!-- Styles and other resources below here. -->  
    ```  
  
     Queste risorse vengono utilizzate come proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> per un rettangolo da inserire nell'oggetto <xref:System.Windows.Controls.Grid> del modello del pulsante.  Aggiungere il seguente markup evidenziato al modello.  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="{x:Type Button}">  
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}"  
    ClipToBounds="True">  
  
        <!-- Outer Rectangle with rounded corners. -->  
        <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"   
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />  
  
        <!-- Inner Rectangle with rounded corners. -->  
        <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20"   
          Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />  
  
        <!-- Glass Rectangle -->  
        <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"  
          VerticalAlignment="Stretch"  
          StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"  
          Fill="{StaticResource MyGlassBrushResource}"  
          RenderTransformOrigin="0.5,0.5">  
          <Rectangle.Stroke>  
            <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">  
              <LinearGradientBrush.GradientStops>  
                <GradientStop Offset="0.0" Color="LightBlue" />  
                <GradientStop Offset="1.0" Color="Gray" />  
              </LinearGradientBrush.GradientStops>  
            </LinearGradientBrush>  
          </Rectangle.Stroke>  
  
          <!-- These transforms have no effect as they are declared here.   
               The reason the transforms are included is to be targets   
               for animation (see later). -->  
          <Rectangle.RenderTransform>  
            <TransformGroup>  
              <ScaleTransform />  
              <RotateTransform />  
            </TransformGroup>  
          </Rectangle.RenderTransform>  
  
          <!-- A BevelBitmapEffect is applied to give the button a   
               "Beveled" look. -->  
          <Rectangle.BitmapEffect>  
            <BevelBitmapEffect />  
          </Rectangle.BitmapEffect>  
        </Rectangle>  
  
        <!-- Present Text of the button. -->  
        <DockPanel Name="myContentPresenterDockPanel">  
          <ContentPresenter x:Name="myContentPresenter" Margin="20"   
            Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />  
        </DockPanel>  
      </Grid>  
    </ControlTemplate>  
    </Setter.Value>  
    ```  
  
     Poiché la proprietà <xref:System.Windows.UIElement.Opacity%2A> del rettangolo con la proprietà `x:Name` di "glassCube" è 0, quando si esegue l'esempio, il rettangolo con effetto cristallo non sarà visibile.  In seguito verranno aggiunti dei trigger al modello per l'interazione dell'utente con il pulsante.  Tuttavia, è ora possibile avere un'idea dell'aspetto del pulsante impostando il valore <xref:System.Windows.UIElement.Opacity%2A> su 1 ed eseguendo l'applicazione.  Vedere la figura riportata di seguito.  Prima di procedere al passaggio successivo, impostare di nuovo <xref:System.Windows.UIElement.Opacity%2A> su 0.  
  
     ![Pulsanti personalizzati creati usando XAML](../../../../docs/framework/wpf/controls/media/custom-button-animatedbutton-5.png "custom\_button\_AnimatedButton\_5")  
  
## Creare l'interattività del pulsante  
 In questa sezione, verranno creati i trigger delle proprietà e degli eventi per modificare i valori delle proprietà ed eseguire animazioni in risposta alle azioni dell'utente, ad esempio spostamento del puntatore del mouse su un pulsante e successivo clic.  
  
 Un modo semplice per creare interattività \(passaggio del mouse, spostamento del mouse all'esterno, clic e così via\) consiste nel definire trigger all'interno del modello o dello stile.  Per creare un <xref:System.Windows.Trigger>, definire una "condizione" della proprietà, ad esempio: Il valore della proprietà <xref:System.Windows.UIElement.IsMouseOver%2A> del pulsante è uguale a `true`.  Definire quindi i metodi di impostazione \(azioni\) che si verificano quando la condizione del trigger è vera.  
  
#### Per creare l'interattività del pulsante  
  
1.  **Aggiungere trigger di modelli:** aggiungere il markup evidenziato al modello.  
  
    ```  
    <Setter.Value>  
      <ControlTemplate TargetType="{x:Type Button}">  
        <Grid Width="{TemplateBinding Width}"   
          Height="{TemplateBinding Height}" ClipToBounds="True">  
  
          <!-- Outer Rectangle with rounded corners. -->  
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"   
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"   
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />  
  
          <!-- Inner Rectangle with rounded corners. -->  
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"   
            VerticalAlignment="Stretch" Stroke="Transparent"   
            StrokeThickness="20"   
            Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20"   
          />  
  
          <!-- Glass Rectangle -->  
          <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"  
            VerticalAlignment="Stretch"  
            StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"  
            Fill="{StaticResource MyGlassBrushResource}"  
            RenderTransformOrigin="0.5,0.5">  
            <Rectangle.Stroke>  
              <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">  
                <LinearGradientBrush.GradientStops>  
                  <GradientStop Offset="0.0" Color="LightBlue" />  
                  <GradientStop Offset="1.0" Color="Gray" />  
                </LinearGradientBrush.GradientStops>  
              </LinearGradientBrush>  
            </Rectangle.Stroke>  
  
            <!-- These transforms have no effect as they   
                 are declared here.   
                 The reason the transforms are included is to be targets   
                 for animation (see later). -->  
            <Rectangle.RenderTransform>  
              <TransformGroup>  
                <ScaleTransform />  
                <RotateTransform />  
              </TransformGroup>  
            </Rectangle.RenderTransform>  
  
              <!-- A BevelBitmapEffect is applied to give the button a   
                   "Beveled" look. -->  
            <Rectangle.BitmapEffect>  
              <BevelBitmapEffect />  
            </Rectangle.BitmapEffect>  
          </Rectangle>  
  
          <!-- Present Text of the button. -->  
          <DockPanel Name="myContentPresenterDockPanel">  
            <ContentPresenter x:Name="myContentPresenter" Margin="20"   
              Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />  
          </DockPanel>  
        </Grid>  
  
        <ControlTemplate.Triggers>  
          <!-- Set action triggers for the buttons and define  
               what the button does in response to those triggers. -->  
        </ControlTemplate.Triggers>  
      </ControlTemplate>  
    </Setter.Value>  
    ```  
  
2.  **Aggiungere trigger di proprietà:** aggiungere il markup evidenziato al blocco `ControlTemplate.Triggers`:  
  
    ```  
    <ControlTemplate.Triggers>  
  
      <!-- Set properties when mouse pointer is over the button. -->  
      <Trigger Property="IsMouseOver" Value="True">  
  
        <!-- Below are three property settings that occur when the   
             condition is met (user mouses over button).  -->  
        <!-- Change the color of the outer rectangle when user   
             mouses over it. -->  
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"  
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />  
  
        <!-- Sets the glass opacity to 1, therefore, the   
             glass "appears" when user mouses over it. -->  
        <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />  
  
        <!-- Makes the text slightly blurry as though you   
             were looking at it through blurry glass. -->  
        <Setter Property="ContentPresenter.BitmapEffect"   
          TargetName="myContentPresenter">  
          <Setter.Value>  
            <BlurBitmapEffect Radius="1" />  
          </Setter.Value>  
        </Setter>  
      </Trigger>  
  
    <ControlTemplate.Triggers/>  
    ```  
  
     Premere F5 per eseguire l'applicazione e osservare l'effetto mentre si sposta il puntatore del mouse sui pulsanti.  
  
3.  **Aggiungere un trigger dello stato attivo:** in seguito verranno aggiunti alcuni metodi di impostazione per gestire i casi in cui il pulsante presenta lo stato attivo, ad esempio dopo un clic dell'utente.  
  
    ```  
    <ControlTemplate.Triggers>  
  
      <!-- Set properties when mouse pointer is over the button. -->  
      <Trigger Property="IsMouseOver" Value="True">  
  
        <!-- Below are three property settings that occur when the   
             condition is met (user mouses over button).  -->  
        <!-- Change the color of the outer rectangle when user          mouses over it. -->  
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"  
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />  
  
        <!-- Sets the glass opacity to 1, therefore, the          glass "appears" when user mouses over it. -->  
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />  
  
        <!-- Makes the text slightly blurry as though you were          looking at it through blurry glass. -->  
        <Setter Property="ContentPresenter.BitmapEffect"       TargetName="myContentPresenter">  
          <Setter.Value>  
            <BlurBitmapEffect Radius="1" />  
          </Setter.Value>  
        </Setter>  
      </Trigger>  
      <!-- Set properties when button has focus. -->  
      <Trigger Property="IsFocused" Value="true">  
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />  
        <Setter Property="Rectangle.Stroke" TargetName="outerRectangle"  
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />  
        <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />  
      </Trigger>  
  
    </ControlTemplate.Triggers>  
    ```  
  
     Premere F5 per eseguire l'applicazione e fare clic su uno dei pulsanti.  Il pulsante rimane evidenziato dopo avere fatto clic su di esso perché presenta ancora lo stato attivo.  Se si fa clic su un altro pulsante, il nuovo pulsante ottiene lo stato attivo mentre quello precedente lo perde.  
  
4.  **Aggiungere animazioni per**  <xref:System.Windows.UIElement.MouseEnter> **e** <xref:System.Windows.UIElement.MouseLeave>**:** A questo punto verranno aggiunte alcune animazioni ai trigger.  Aggiungere il markup seguente in qualsiasi punto del blocco `ControlTemplate.Triggers`.  
  
    ```  
  
                    <!-- Animations that start when mouse enters and leaves button. -->  
    <EventTrigger RoutedEvent="Mouse.MouseEnter">  
      <EventTrigger.Actions>  
        <BeginStoryboard Name="mouseEnterBeginStoryboard">  
          <Storyboard>  
  
          <!-- This animation makes the glass rectangle shrink in the X direction. -->  
            <DoubleAnimation Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)"  
              By="-0.1" Duration="0:0:0.5" />  
  
            <!-- This animation makes the glass rectangle shrink in the Y direction. -->  
            <DoubleAnimation  
            Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)"   
              By="-0.1" Duration="0:0:0.5" />  
          </Storyboard>  
        </BeginStoryboard>  
      </EventTrigger.Actions>  
    </EventTrigger>  
    <EventTrigger RoutedEvent="Mouse.MouseLeave">  
      <EventTrigger.Actions>  
  
        <!-- Stopping the storyboard sets all animated properties back to default. -->  
        <StopStoryboard BeginStoryboardName="mouseEnterBeginStoryboard" />  
      </EventTrigger.Actions>  
    </EventTrigger>  
    ```  
  
     Il rettangolo con effetto cristallo si riduce quando il puntatore del mouse viene spostato sul pulsante e torna nuovamente alle dimensioni normali quando viene spostato all'esterno.  
  
     Quando il puntatore viene spostato sul pulsante vengono attivate due animazioni \(viene generato l'evento <xref:System.Windows.UIElement.MouseEnter>\).  Queste animazioni riducono il rettangolo con effetto cristallo lungo gli assi X e Y.  Si notino le proprietà sugli elementi <xref:System.Windows.Media.Animation.DoubleAnimation>, ovvero <xref:System.Windows.Media.Animation.Timeline.Duration%2A> e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>.  Tramite la proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> si specifica che l'animazione viene eseguita per mezzo secondo, mentre <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> specifica che l'effetto cristallo viene ridotto del 10%.  
  
     Il secondo trigger di evento \(<xref:System.Windows.UIElement.MouseLeave>\) interrompe semplicemente il primo.  Quando si interrompe un oggetto <xref:System.Windows.Media.Animation.Storyboard>, vengono ripristinati i valori predefiniti di tutte le proprietà animate.  Pertanto, quando l'utente allontana il puntatore dal pulsante, quest'ultimo assume nuovamente lo stato che presentava prima che il puntatore del mouse fosse spostato sul pulsante.  Per ulteriori informazioni sulle animazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
5.  **Aggiungere un'animazione per il clic del mouse sul pulsante:** il passaggio finale consiste nell'aggiungere un trigger per il clic del mouse sul pulsante.  Aggiungere il markup seguente in qualsiasi punto del blocco `ControlTemplate.Triggers`:  
  
    ```  
  
                    <!-- Animation fires when button is clicked, causing glass to spin.  -->  
    <EventTrigger RoutedEvent="Button.Click">  
      <EventTrigger.Actions>  
        <BeginStoryboard>  
          <Storyboard>  
            <DoubleAnimation Storyboard.TargetName="glassCube"   
              Storyboard.TargetProperty=  
              "(Rectangle.RenderTransform).(TransformGroup.Children)[1].(RotateTransform.Angle)"   
              By="360" Duration="0:0:0.5" />  
          </Storyboard>  
        </BeginStoryboard>  
      </EventTrigger.Actions>  
    </EventTrigger>  
    ```  
  
     Premere F5 per eseguire l'applicazione e fare clic su uno dei pulsanti.  Quando si fa clic su un pulsante, il rettangolo con effetto cristallo ruota.  
  
## Riepilogo  
 In questa procedura dettagliata, sono stati eseguiti i seguenti esercizi:  
  
-   <xref:System.Windows.Style> destinato a un tipo di oggetto \(<xref:System.Windows.Controls.Button>\).  
  
-   Controllate le proprietà di base dei pulsanti dell'intera applicazione tramite <xref:System.Windows.Style>.  
  
-   Create risorse quali sfumature da utilizzare per i valori di proprietà dei metodi di impostazione di <xref:System.Windows.Style>.  
  
-   Personalizzato l'aspetto dei pulsanti dell'intera applicazione applicando un modello ai pulsanti.  
  
-   Personalizzato il comportamento dei pulsanti in risposta alle azioni dell'utente \(ad esempio <xref:System.Windows.UIElement.MouseEnter>, <xref:System.Windows.UIElement.MouseLeave>e <xref:System.Windows.Controls.Primitives.ButtonBase.Click>\) che includevano effetti animazione.  
  
## Vedere anche  
 [Creare un pulsante tramite Microsoft Expression Blend](../../../../docs/framework/wpf/controls/walkthrough-create-a-button-by-using-microsoft-expression-blend.md)   
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Cenni preliminari sugli effetti bitmap](../../../../docs/framework/wpf/graphics-multimedia/bitmap-effects-overview.md)