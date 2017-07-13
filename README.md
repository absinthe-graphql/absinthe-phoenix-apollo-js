# absinthe-phoenix-apollo

Support for Apollo Client + Absinthe Subscriptions.

The goal of this package is to provide a client that is a drop-in replacement
for the `SubscriptionClient` from [subscriptions-transport-ws](https://www.npmjs.com/package/subscriptions-transport-ws), used in "hybrid"
mode (subscriptions over websocket, queries and mutations over HTTP).

Note: This package is currently non-functional. We're building it!

## Usage

```javascript
import SubscriptionClient from 'absinthe-phoenix-apollo';
import { addGraphQLSubscriptions} from 'subscriptions-transport-ws';
import ApolloClient, {createNetworkInterface} from 'apollo-client';

// Create regular NetworkInterface by using apollo-client's API:
const networkInterface = createNetworkInterface({
  uri: 'http://localhost:3000' // Your GraphQL endpoint
});

// Create WebSocket client
const wsClient = new SubscriptionClient(`ws://localhost:5000/`, {
  // Pass any arguments you want for initialization
});

// Extend the network interface with the WebSocket
const networkInterfaceWithSubscriptions = addGraphQLSubscriptions(
  networkInterface,
  wsClient
);

// Finally, create your ApolloClient instance with the modified network interface
const apolloClient = new ApolloClient({
  networkInterface: networkInterfaceWithSubscriptions
});
```

## Contributing

The code is written in TypeScript (as are many GraphQL projects in the JS
ecosystem). We'd happily accept help refactoring, documenting, and expanding the
code from more experienced TypeScript developers!

## License

See [LICENSE.md](/.LICENSE.md).