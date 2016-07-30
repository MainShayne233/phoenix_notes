# Phoenix Notes

## Migrations:

### Create a migration
```bash
mix ecto.gen.migration <your_migration_file_name>
```
The migration file will show up in ```priv/repo/migrations``` and look something like this:
```elixir
defmodule MyApp.Repo.Migrations.YourMigrationFileName do
  use Ecto.Migration

  def change do
  end
end
```
