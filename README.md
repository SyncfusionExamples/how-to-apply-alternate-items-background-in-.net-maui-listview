# How to apply different background for alternate items in .NET MAUI ListView?
This example demonstrates how to apply different background for alternate items in .NET MAUI ListView.

**[View document in Syncfusion .NET MAUI Knowledge Base](https://www.syncfusion.com/kb/13079/how-to-apply-alternate-item-background-in-net-maui-listview-sflistview)**

## Sample

```xaml
<ContentPage.Resources>
    <ResourceDictionary>
        <local:IndexToColorConverter x:Key="IndexToColorConverter"/>
    </ResourceDictionary>
</ContentPage.Resources>

<syncfusion:SfListView x:Name="listView"
                ItemSpacing="1" ItemSize="60"
                ItemsSource="{Binding ContactsInfo}">
    <syncfusion:SfListView.ItemTemplate >
        <DataTemplate>
            <code>
            . . .
            . . .
            <code>
        </DataTemplate>
    </syncfusion:SfListView.ItemTemplate>
</syncfusion:SfListView>

C#:

ListView.SelectionChanging += ListView_SelectionChanging;

private void ListView_SelectionChanging(object sender, ItemSelectionChangingEventArgs e)
{
    for (int i = 0; i < e.AddedItems.Count; i++)
    {
        var item = e.AddedItems[i] as Contacts;
        item.IsSelected = true;
    }

    for (int i = 0; i < e.RemovedItems.Count; i++)
    {
        var item = e.RemovedItems[i] as Contacts;
        item.IsSelected = false;
    }
}

public class IndexToColorConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        var listview = parameter as SfListView;
        return listview.DataSource.DisplayItems.IndexOf(value) % 2 == 0 ? Colors.Lavender : Colors.AliceBlue;
    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```
