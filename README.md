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
### Create a table
Say we are creating a users table, where users have a column for name, age, list of foods they like, and whether or not they are using Phoenix, where the default is true. We'd fill fill out the migration file as such:
```elixir
defmodule MyApp.Repo.Migrations.CreateCriteria do
  use Ecto.Migration

  def change do
    create table(:users) do
      add :name, :string
      add :age, :integer
      add :liked_foods, {:array, :string}
      add :using_phoenix, :boolean, default: true

      timestamps
    end

  end
end
```
To create this table in our database, we simply run:
```bash
mix ecto.migrate
```
