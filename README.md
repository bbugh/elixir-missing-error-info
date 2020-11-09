This is a reproduction for the empty `UndefinedFunctionError`:

1. `mix deps.get`
2. `mix ecto.setup`
2. `mix phx.server`
3. Visit [http://localhost:4000/graphiql](http://localhost:4000/graphiql)
4. Run the following query:
    ```
    query Search($term: String!) {
      search(matching: $term) {
        __typename
        ... on MenuItem {
          name
        }
        ... on Category {
          name
          items {
            name
          }
        }
      }
    }
    ```
5. ✅ Observe that it successfully returns a list of menu items/categories
6. Comment out line 13 in `lib/plate_slate_web/schema/menu_types.ex`:
    ```
    diff --git a/lib/plate_slate_web/schema/menu_types.ex b/lib/plate_slate_web/schema/menu_types.ex
    index d965f71..76df21c 100644
    --- a/lib/plate_slate_web/schema/menu_types.ex
    +++ b/lib/plate_slate_web/schema/menu_types.ex
    @@ -9,7 +9,7 @@
    defmodule PlateSlateWeb.Schema.MenuTypes do
      use Absinthe.Schema.Notation

    -  alias PlateSlateWeb.Resolvers
    +  # alias PlateSlateWeb.Resolvers

      object :category do
        field(:name, :string)
    ```
7. Return to the browser and run the query again
8. ❌ Observe the unexpected function call error with no info:
    ```
    [error] #PID<0.477.0> running PlateSlateWeb.Endpoint terminated
    Server: localhost:4000 (http)
    Request: POST /graphiql
    ** (exit) {%UndefinedFunctionError{arity: nil, function: nil, message: nil, module: nil, reason: nil}, []}
    ```


### Copyright

The code in this repository is taken from the [freely available sample code](https://pragprog.com/titles/wwgraphql/craft-graphql-apis-in-elixir-with-absinthe/) for the book *Craft GraphQL APIs in Elixir with Absinthe*.
