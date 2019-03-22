# @Identifier
This annotation signifies that a field is the identifying field of a RestModel. A RestModel can only have one `@Identifier`. Furthermore, the supported Identifier types are String, Long or Integer. 
If no @Identifier is used, Elepy will look for a field with the name 'id', or annotated with `@JsonProperty("id")`