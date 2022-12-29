# WPF

```xaml
        <StackPanel Orientation="Vertical">
            <Rectangle Height="20" Margin="2" Fill="CadetBlue"></Rectangle>
            <Rectangle Heighty="20" Margin="2" Fill="CadetBlue"></Rectangle>
        </StackPanel>
        <StackPanel Orientation="Horizontal">
            <Rectangle Width="20" Margin="2" Fill="CadetBlue"></Rectangle>
            <Rectangle Width="20" Margin="2" Fill="CadetBlue"></Rectangle>
        </StackPanel>
```
```xaml
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition></RowDefinition>
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="40"/>
            <ColumnDefinition />
        </Grid.ColumnDefinitions>

        <Rectangle Fill="LightBlue" Grid.Column="1" Grid.Row="1"/>
        <StackPanel Grid.Column="1"/>
    </Grid>
```
```xaml
    <Canvas>
        <Rectangle Fill="LightBlue" Height="50" Width="50" Canvas.Top="100" Canvas.Left="100" Panel.ZIndex="1"/>
        <Rectangle Fill="Red" Height="50" Width="50" Canvas.Top ="130" Canvas.Left="130"/>
    </Canvas>
```
```xaml
        <ListView x:Name="customerListView" Grid.Row="1" Margin="10 0 10 10">
            <ListViewItem>Julia</ListViewItem>
            <ListViewItem>Alex</ListViewItem>
            <ListViewItem>Thomas</ListViewItem>
        </ListView>
        <StackPanel Grid.Column="1" Margin="10">
            <Label>Firstname:</Label>
            <TextBox Text="{Binding ElementName=customerListView, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged, Path=SelectedItem.Content}"/>
            <Label>Lastname:</Label>
            <TextBox/>
            <CheckBox Margin="0 10 0 0">
                Is developer
            </CheckBox>
        </StackPanel>
```
