---
id: graphql-api-update-mutation-plugin
title: Update Mutation Plugin
---

## Source Code
> [gqlify/src/plugins/update.ts](https://github.com/Canner/gqlify/blob/master/packages/gqlify/src/plugins/update.ts)

## GraphQL Schema
For datamodel below
```graphql
type User @GQLifyModel(dataSource: "memory", key: "users") {
  id: ID! @unique @autoGen
  username: String!
  email: String
}
```

You'll get following mutations appended to GraphQL schema using this plugin.
```graphql
type Mutation {
  updateUser(where: UserWhereUniqueInput, data: UserUpdateInput!): UserUpdateResponse
}


input UserUpdateInput {
  username: String
  email: String
}

type UserUpdateResponse {
  id: ID
}

# NOTICE: UserWhereUniqueInput is generated by `WhereInputPlugin`
input UserWhereUniqueInput {
  id: ID
}
```

## Resolvers
In `update` mutation, GQLify will call `update` method of `DataSource` to update a record.
> [Learn more about `DataSource` methods](/docs/create-own-data-source)
