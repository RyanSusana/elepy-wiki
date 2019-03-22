# @Searchable
This annotation signifies that a field is searchable, and should be considered implemented in the `Crud` interface. When you mark a field as searchable, you say that a field should be able to be queried for.

By default, all @Searchable fields can be queried for by specifying a 'q' query parameter in a GET request.