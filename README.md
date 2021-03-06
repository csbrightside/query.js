# query.js
Super simple GraphQL query function for Shopify storefront API.

## About
Query.js is a simple function that performs a GraphQL query without the extra bloat of dependencies like Apollo or urql, though they're recommended if you need more features (such as error handling or caching).

It supports arguments, aliases, and nested fields in GraphQL fragments, but does not support passing query variables to the fragments.

## Usage

First update the `store`, `token`, and `version` variables in _query.js_. See [Shopify's documentation](https://shopify.dev/api/storefront) to see how you setup a private app with storefront API permissions.

The below usage expects you to have a build tool setup to import and compile your GraphQL and JS files such as Webpack.

```js
import product from 'product.gql'
import Query from 'query'

try {
  const response = await Query({
    locale: 'en',
    query: product,
    variables: {
      country: 'GB',
      handle: 'product-handle',
    },
  })

  // Format response and use

} catch (error) {
  throw new Error('Failed to load product', error)
}
```

The response you receive will be an object with all the usual edges and nodes you'd expect from a GraphQL response.

It's recommended that you use Liquid to define the `locale` and `country` values using `{{ localization.language.iso_code | json }}` and `{{ localization.country.iso_code | json }}` respectively and pass them to JS.

> You should never use this to access the Admin API as your credentials will be publicly accessible.
