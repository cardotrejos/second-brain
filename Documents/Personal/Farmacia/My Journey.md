PETAL PRO - Prescriptions App

The problem
Seeds on production environment, the solution was creating the admin through console 

```bash
fly ssh console -a prescriptions-app -C "/app/bin/prescriptions_app remote"
```

There I have to create the user with a command like this


```bash
alias PrescriptionsApp.Repo

{:ok, admin} = PrescriptionsApp.Accounts.register_user(%{ name: "Ricardo Trejos", email: "cardotrejos@gmail.com", password: "fluCKE619*", confirmed_at: DateTime.utc_now(), is_onboarded: true, role: :admin })
```

```
alias PrescriptionsApp.Repo

{:ok, admin} = PrescriptionsApp.Accounts.register_user(%{ name: "Farmacia 1", email: "farmacia@gmail.com", password: "password", confirmed_at: DateTime.utc_now(), is_onboarded: true, role: :user })
```

```
{:ok, admin} = PrescriptionsApp.Accounts.register_user(%{ name: "Medico 1", email: "medico@gmail.com", password: "password", confirmed_at: DateTime.utc_now(), is_onboarded: true, role: :user })
```

PrescriptionsApp.Accounts.update_user_as_admin(user, %{confirmed_at: DateTime.utc_now()})


{:ok, admin} = PrescriptionsApp.Accounts.register_user(%{ name: "Paciente 1", email: "paciente1@gmail.com", password: "password", confirmed_at: DateTime.utc_now(), is_onboarded: true, role: :user })

{:ok, admin} = PrescriptionsApp.Accounts.register_user(%{ name: "Paciente 2", email: "paciente2@gmail.com", password: "password", confirmed_at: DateTime.utc_now(), is_onboarded: true, role: :user })

user = PrescriptionsApp.Accounts.get_user!(4)


```
# Import aliases 
alias PrescriptionsApp.Accounts alias PrescriptionsApp.Accounts.Patient 

# Create a patient with required fields 
patient_params = %{ name: "John Doe 2", email: "john.doe2@example.com", phone_number: "1234567890", shipping_address: "456 Main St, City, Country" } 

# Create the patient using Accounts context Accounts.create_patient(patient_params)
```








