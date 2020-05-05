# ern-navigation

[![ci][1]][2]

## Getting Started

### Prerequisites

- All [prerequisites of Electrode Native][3]
- An Electrode Native [miniapp][4]

### Installation

Install `ern-navigation` as a dependency in your miniapp:

```sh
yarn add ern-navigation
```

Or `npm install --save ern-navigation`

### Integration

First, let's create some components to act as the app's different screens.
Each of these components should extend Electrode Native Navigation's
<a href="#Component">Component</a> class, and will need to define a few class
properties. Here's an example:

```js
import {Component} from 'ern-navigation';

export default class MainScreenComponent extends Component {
  static displayName = 'Main Screen';
  static navigationOptions = {
    title: 'My Application',
    buttons: [{
      icon: Image.resolveAssetSource(exitIcon).uri,
      id: 'exit',
      location: 'right',
      accessibilityLabel: 'Exit this app'
    }]
  };
  onNavButtonPress (buttonId) {
    switch (buttonId) {
      case 'exit':
        this.finish();
        break;
      default:
        console.warn(
          `'${buttonId}' not handled in '${MainScreenComponent.getRegisteredRoute()}'`,
        );
        break;
    }
  }
}
```

Once all screen components have been created, they will need to be registered
using Electrode Native Navigation's <a href="#AppNavigator">AppNavigator</a>
class, like this:

```js
import {AppNavigator} from 'ern-navigation';

new AppNavigator({
  'MainScreen': MainScreenComponent,
  'SecondScreen': SecondScreenComponent,
  // ...
}, {
  initialScreen: 'MainScreen'
}).registerAll('MyMiniApp');
```

In this example, the `MainScreenComponent` and `SecondScreenComponent` are
referred to as `MainScreen` and `SecondScreen`, respectively, whenever any
navigation is performed. From inside any of the screen components, calling
`this.navigateInternal(screenName)` will navigate to the specified registered
screen.

## Example

The [movies-reloaded][5] miniapp outlines the different mechanisms that are
provided to you by Electrode Native Navigation.

## Further Reading

Check out our [Electrode Native Navigation Blog Post][6].

## Documentation

Check the documentation for more information.

&copy; 2019 WalmartLabs

[1]: https://github.com/electrode-io/ern-navigation/workflows/ci/badge.svg
[2]: https://github.com/electrode-io/ern-navigation/actions
[3]: https://native.electrode.io/introduction/what-is-ern/requirements
[4]: https://native.electrode.io/introduction/what-is-ern/what-is-a-miniapp
[5]: https://github.com/electrode-io/movies-reloaded-miniapp
[6]: https://medium.com/walmartlabs/electrode-native-navigation-576297fbcb3d
[7]: https://www.electrode.io/ern-navigation
