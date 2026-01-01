```bash
fly ssh console -a museum-catalog-app -C "/app/bin/catalog4_all remote"
```

```elixir
{:ok, admin} = Catalog4All.Accounts.register_user(%{ name: "Ricardo Trejos", email: "cardotrejos@gmail.com", password: "fluCKE619*", confirmed_at: DateTime.utc_now(), is_onboarded: true, role: :admin })
```

user = Catalog4All.Accounts.get_user!("1effc79c-ca6e-6a12-bea3-39f8e1a51e0e")

Catalog4All.Accounts.update_user_as_admin(user, %{confirmed_at: DateTime.utc_now()})