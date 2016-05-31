# Switchboard Example

This is a very basic architecture example. The UI has two user controls, one for a list of customers and one for inserting customers.

After inserting a customer an event is fired on the Switchboard. The list control listens for that event and reloads the list.

Customer records inserted. Switchboard event is fired.
```
        private void Insert_Click(object sender, RoutedEventArgs e)
        {
            var factory = new ManagerFactory();
            var customerManager = factory.Create<ICustomerManager>();
            customerManager.Insert(_customer);
            _customer = new Customer();
            RaisePropertyChanged("First");
            RaisePropertyChanged("Last");

            // after we save, lets tell everyone
            Switchboard.FireOnCustomerInserted();
        }
```


```
        private void Switchboard_OnCustomerInserted(object sender, EventArgs e)
        {
            Reload();
        }
```
