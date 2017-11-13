# absinthe-phoenix-apollo

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

(OLD) Support for Apollo Client + Absinthe Subscriptions.

## DEPRECATED

Superseded by [@absinthe/socket-apollo-link](https://github.com/absinthe-graphql/absinthe-socket/tree/master/packages/socket-apollo-link).

## Usage

```javascript
import SubscriptionClient from 'absinthe-phoenix-apollo';
import { addGraphQLSubscriptions} from 'subscriptions-transport-ws';
import ApolloClient, {createNetworkInterface} from 'apollo-client';

// Create regular NetworkInterface by using apollo-client's API:
const networkInterface = createNetworkInterface({
  uri: 'http://localhost:4000' // Your GraphQL endpoint
});

// Create WebSocket client
const wsClient = new SubscriptionClient(`ws://localhost:4000/socket`, {
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

See [LICENSE.md](./LICENSE.md).
