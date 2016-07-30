# Phoenix Notes

## Migrations:

### Create a migration
```bash
mix ecto.gen.migration your_migration_file_name
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

      timestamps # Default Phoenix thing
    end
  end
end
```
To create this table, we simply migrate our database by running:
```bash
mix ecto.migrate
```

### Add a column
In the case we decided to add a column for the user's birthday, we would create another migration:
```bash
mix ecto.gen.migration add_birthday_to_to_users
```
Then open up the fresh migration file in ```priv/repo/migrations``` and fill it out like so:
```elixir
defmodule MyApp.Repo.Migrations.AddBirthdayToUsers do
  use Ecto.Migration

  def change do
    alter table(:users) do
      add :birthda, :string
    end
  end
end
```
And as always, we need to migrate our changes:
```bash
mix ecto.migrate
```
Oh no! We mispelled ```birthday```, and we already migrated! No worries, we'll just create a migration to rename the column!
Generate that migration file!
```bash
mix ecto.gen.migration change_birthda_to_birthday
```
Fill out that bad boy like this:
```elixir
defmodule MyApp.Repo.Migrations.ChangeBirthdaToBirthday do
  use Ecto.Migration
  # Notice def change no longer has a do block within it, unlike the previous examples
  def change do
    rename table(:criterias), :birthda, to: :birthday
  end
end
```
