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
* Binding Example
```xaml
        <ListView x:Name="customerListView" Grid.Row="1" Margin="10 0 10 10">
            <ListViewItem>Julia</ListViewItem>
            <ListViewItem>Alex</ListViewItem>
            <ListViewItem>Thomas</ListViewItem>
        </ListView>
        <StackPanel Grid.Column="1" Margin="10">
            <Label>Firstname:</Label>
            <TextBox Text="{Binding ElementName=customerListView,
            Mode=TwoWay,
            UpdateSourceTrigger=PropertyChanged,
            Path=SelectedItem.Content}"/>
            <Label>Lastname:</Label>
            <TextBox/>
            <CheckBox Margin="0 10 0 0">
                Is developer
            </CheckBox>
        </StackPanel>
```
* view
```xaml
        <ListView Grid.Row="1" x:Name="customerListView"
                          ItemsSource="{Binding Path=Customers}"
                          DisplayMemberPath="FirstName"
                          SelectedItem="{Binding Path=SelectedCustomer, Mode=TwoWay}"
                          Margin="10 0 10 10" />
                          
            <StackPanel Grid.Column="1" Margin="10">
                <Label>Firstname:</Label>
                <TextBox Text="{Binding ElementName=customerListView,
                Path=SelectedItem.FirstName,
                Mode=TwoWay,
                UpdateSourceTrigger=PropertyChanged}"/>
                <Label>Lastname:</Label>
                <TextBox/>
                <CheckBox Margin="0 10 0 0">
                    Is developer
                </CheckBox>
            </StackPanel>                 
```
* view cs file
```cs
        private readonly CustomersViewModel _viewModel;

        public CustomersView()
        {
            InitializeComponent();
            _viewModel = new CustomersViewModel(new CustomerDataProvider());
            DataContext = _viewModel;
            Loaded += CustomersView_Loaded;
        }

        private async void CustomersView_Loaded(object sender, RoutedEventArgs e)
        {
            await _viewModel.LoadAsync();
        }
```
* viewModel

```cs
    public class CustomersViewModel
    {
        private readonly ICustomerDataProvider _customerDataProvider;

        public CustomersViewModel(ICustomerDataProvider customerDataProvider)
        {
            _customerDataProvider = customerDataProvider;
        }
        public ObservableCollection<Customer> Customers { get; } = new ObservableCollection<Customer>();
        public Customer? SelectedCustomer { get; set; }
        public async Task LoadAsync()
        {
            if (Customers.Any())
            {
                return;
            }
            var customers = await _customerDataProvider.GetAllAsync();
            if (customers is not null)
            {
                foreach (var customer in customers)
                {
                    Customers.Add(customer);
                }
            }
        }
    }
```
* using selectedCustomer ie giving more power to viewModel
```cs
                </StackPanel>
                <ListView Grid.Row="1"
                          ItemsSource="{Binding Path=Customers}"
                          DisplayMemberPath="FirstName"
                          SelectedItem="{Binding Path=SelectedCustomer, Mode=TwoWay}"
                          Margin="10 0 10 10" />
            </Grid>

            <!-- Customer detail -->
            <StackPanel Grid.Column="1" Margin="10">
                <Label>Firstname:</Label>
                <TextBox Text="{Binding
                Path=SelectedCustomer.FirstName,
                Mode=TwoWay,
                UpdateSourceTrigger=PropertyChanged}"/>
                <Label>Lastname:</Label>
                <TextBox Text="{Binding
                Path=SelectedCustomer.LastName,
                Mode=TwoWay,
                UpdateSourceTrigger=PropertyChanged}"/>
                <CheckBox IsChecked="{Binding
                Path=SelectedCustomer.IsDeveloper,
                Mode=TwoWay,
                UpdateSourceTrigger=PropertyChanged}" Margin="0 10 0 0">
                    Is developer
                </CheckBox>
            </StackPanel>
```
