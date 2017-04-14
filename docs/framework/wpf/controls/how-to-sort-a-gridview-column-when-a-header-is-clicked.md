---
title: "Procedura: ordinare una colonna GridView quando si fa clic su un&#39;intestazione | Microsoft Docs"
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
  - "controlli GridView"
  - "controlli ListView"
  - "Controlli ListView, l'ordinamento di colonne GridView"
  - "Controlli GridView, il controllo ListView"
ms.assetid: 4865d720-d147-40ed-83a7-af7587f8aad8
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Procedura: ordinare una colonna GridView quando si fa clic su un&#39;intestazione
In questo esempio viene illustrato come creare un <xref:System.Windows.Controls.ListView> controllo che implementa un <xref:System.Windows.Controls.GridView> consente di visualizzare la modalità e ordinare il contenuto quando un utente fa clic su un'intestazione di colonna.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente definisce una <xref:System.Windows.Controls.GridView> con tre colonne associate ai <xref:System.DateTime.Year%2A>, <xref:System.DateTime.Month%2A>, e <xref:System.DateTime.Day%2A>, proprietà del <xref:System.DateTime> struttura.  
  
```xaml  
<GridView>  
  <GridViewColumn DisplayMemberBinding="{Binding Path=Year}"   
                  Header="Year"  
                  Width="100"/>  
  <GridViewColumn DisplayMemberBinding="{Binding Path=Month}"   
                  Header="Month"  
                  Width="100"/>  
  <GridViewColumn DisplayMemberBinding="{Binding Path=Day}"   
                  Header="Day"  
                  Width="100"/>  
</GridView>  
```  
  
 L'esempio seguente mostra gli elementi di dati che sono definiti come un <xref:System.Collections.ArrayList> di <xref:System.DateTime> oggetti. Il <xref:System.Collections.ArrayList> è definito come il <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> per il <xref:System.Windows.Controls.ListView> controllo.  
  
```xaml  
<ListView.ItemsSource>  
  <s:ArrayList>  
    <p:DateTime>1993/1/1 12:22:02</p:DateTime>  
    <p:DateTime>1993/1/2 13:2:01</p:DateTime>  
    <p:DateTime>1997/1/3 2:1:6</p:DateTime>  
    <p:DateTime>1997/1/4 13:6:55</p:DateTime>  
    <p:DateTime>1999/2/1 12:22:02</p:DateTime>  
    <p:DateTime>1998/2/2 13:2:01</p:DateTime>  
    <p:DateTime>2000/2/3 2:1:6</p:DateTime>  
    <p:DateTime>2002/2/4 13:6:55</p:DateTime>  
    <p:DateTime>2001/3/1 12:22:02</p:DateTime>  
    <p:DateTime>2006/3/2 13:2:01</p:DateTime>  
    <p:DateTime>2004/3/3 2:1:6</p:DateTime>  
    <p:DateTime>2004/3/4 13:6:55</p:DateTime>  
  </s:ArrayList>  
</ListView.ItemsSource>  
```  
  
 Il `s` e `p` gli identificatori nel [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] tag fanno riferimento a mapping dello spazio dei nomi definiti nei metadati del [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] pagina. Nell'esempio seguente viene illustrata la definizione dei metadati.  
  
```xaml  
<Window        
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    x:Class="ListViewSort.Window1"      
    xmlns:s="clr-namespace:System.Collections;assembly=mscorlib"  
    xmlns:p="clr-namespace:System;assembly=mscorlib">  
```  
  
 Per ordinare i dati in base al contenuto di una colonna, nell'esempio viene definito un gestore eventi per gestire il <xref:System.Windows.Controls.Primitives.ButtonBase.Click> evento che si verifica quando si preme il pulsante dell'intestazione di colonna. Nell'esempio seguente viene illustrato come specificare un gestore eventi per il <xref:System.Windows.Controls.GridViewColumnHeader> controllo.  
  
```xaml  
<ListView x:Name='lv' Height="150" HorizontalAlignment="Center"   
  VerticalAlignment="Center"   
  GridViewColumnHeader.Click="GridViewColumnHeaderClickedHandler"  
 >  
```  
  
 L'esempio definisce il gestore dell'evento in modo che la direzione di ordinamento tra crescente e decrescente ogni volta che si preme il pulsante dell'intestazione di colonna. Nell'esempio seguente viene illustrato il gestore dell'evento.  
  
```csharp  
public partial class Window1 : Window  
{  
    public Window1()  
    {  
        InitializeComponent();  
    }  
  
    GridViewColumnHeader _lastHeaderClicked = null;  
    ListSortDirection _lastDirection = ListSortDirection.Ascending;  
  
    void GridViewColumnHeaderClickedHandler(object sender,  
                                            RoutedEventArgs e)  
    {  
        GridViewColumnHeader headerClicked =  
              e.OriginalSource as GridViewColumnHeader;  
        ListSortDirection direction;  
  
        if (headerClicked != null)  
        {  
            if (headerClicked.Role != GridViewColumnHeaderRole.Padding)  
            {  
                if (headerClicked != _lastHeaderClicked)  
                {  
                    direction = ListSortDirection.Ascending;  
                }  
                else  
                {  
                    if (_lastDirection == ListSortDirection.Ascending)  
                    {  
                        direction = ListSortDirection.Descending;  
                    }  
                    else  
                    {  
                        direction = ListSortDirection.Ascending;  
                    }  
                }  
  
                string header = headerClicked.Column.Header as string;  
                Sort(header, direction);  
  
                if (direction == ListSortDirection.Ascending)  
                {  
                    headerClicked.Column.HeaderTemplate =  
                      Resources["HeaderTemplateArrowUp"] as DataTemplate;  
                }  
                else  
                {  
                    headerClicked.Column.HeaderTemplate =  
                      Resources["HeaderTemplateArrowDown"] as DataTemplate;  
                }  
  
                // Remove arrow from previously sorted header  
                if (_lastHeaderClicked != null && _lastHeaderClicked != headerClicked)  
                {  
                    _lastHeaderClicked.Column.HeaderTemplate = null;  
                }  
  
                _lastHeaderClicked = headerClicked;  
                _lastDirection = direction;  
            }  
        }  
    }  
```  
  
```vb  
Partial Public Class Window1  
        Inherits Window  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        Private _lastHeaderClicked As GridViewColumnHeader = Nothing  
        Private _lastDirection As ListSortDirection = ListSortDirection.Ascending  
  
        Private Sub GridViewColumnHeaderClickedHandler(ByVal sender As Object, ByVal e As RoutedEventArgs)  
            Dim headerClicked As GridViewColumnHeader = TryCast(e.OriginalSource, GridViewColumnHeader)  
            Dim direction As ListSortDirection  
  
            If headerClicked IsNot Nothing Then  
                If headerClicked.Role <> GridViewColumnHeaderRole.Padding Then  
                    If headerClicked IsNot _lastHeaderClicked Then  
                        direction = ListSortDirection.Ascending  
                    Else  
                        If _lastDirection = ListSortDirection.Ascending Then  
                            direction = ListSortDirection.Descending  
                        Else  
                            direction = ListSortDirection.Ascending  
                        End If  
                    End If  
  
                    Dim header As String = TryCast(headerClicked.Column.Header, String)  
                    Sort(header, direction)  
  
                    If direction = ListSortDirection.Ascending Then  
                        headerClicked.Column.HeaderTemplate = TryCast(Resources("HeaderTemplateArrowUp"), DataTemplate)  
                    Else  
                        headerClicked.Column.HeaderTemplate = TryCast(Resources("HeaderTemplateArrowDown"), DataTemplate)  
                    End If  
  
                    ' Remove arrow from previously sorted header  
                    If _lastHeaderClicked IsNot Nothing AndAlso _lastHeaderClicked IsNot headerClicked Then  
                        _lastHeaderClicked.Column.HeaderTemplate = Nothing  
                    End If  
  
                    _lastHeaderClicked = headerClicked  
                    _lastDirection = direction  
                End If  
            End If  
        End Sub  
```  
  
 Nell'esempio seguente viene illustrato l'algoritmo di ordinamento che viene chiamato dal gestore eventi per ordinare i dati. L'ordinamento viene eseguita creando un nuovo <xref:System.ComponentModel.SortDescription> struttura.  
  
```csharp  
private void Sort(string sortBy, ListSortDirection direction)  
{  
    ICollectionView dataView =  
      CollectionViewSource.GetDefaultView(lv.ItemsSource);  
  
    dataView.SortDescriptions.Clear();  
    SortDescription sd = new SortDescription(sortBy, direction);  
    dataView.SortDescriptions.Add(sd);  
    dataView.Refresh();  
}  
  
```  
  
```vb  
Private Sub Sort(ByVal sortBy As String, ByVal direction As ListSortDirection)  
            Dim dataView As ICollectionView = CollectionViewSource.GetDefaultView(lv.ItemsSource)  
  
            dataView.SortDescriptions.Clear()  
            Dim sd As New SortDescription(sortBy, direction)  
            dataView.SortDescriptions.Add(sd)  
            dataView.Refresh()  
        End Sub  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [Panoramica sul controllo ListView](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [Cenni preliminari su GridView](../../../../docs/framework/wpf/controls/gridview-overview.md)   
 [Procedure](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)