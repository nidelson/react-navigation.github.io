---
id: stack-actions
title: StackActions reference
sidebar_label: StackActions
---

`StackActions` is an object containing methods for generating actions specific to stack-based navigators. Its methods expand upon the actions available in [`CommonActions`](navigation-actions.md).

The following actions are supported:

### replace

The `replace` action allows to replace a route in the [navigation state](navigation-state.md). It takes the following arguments:

- `name` - _string_ - A destination name of the route that has been registered somewhere.
- `params` - _object_ - Params to pass to the destination route.

<samp id="stack-actions" />

```js
import { StackActions } from '@react-navigation/native';

navigation.dispatch(
  StackActions.replace('Profile', {
    user: 'jane',
  })
);
```

If you want to replace a particular route, you can add a `source` property referring to the route key and `target` property referring to the navigation state key:

<samp id="stack-actions" />

```js
import { StackActions } from '@react-navigation/native';

navigation.dispatch({
  ...StackActions.replace('Profile', {
    user: 'jane',
  }),
  source: route.key,
  target: navigation.getState().key,
});
```

If the `source` property is explicitly set to `undefined`, it'll replace the focused route.

### push

The `push` action adds a route on top of the stack and navigates forward to it. This differs from `navigate` in that `navigate` will pop back to earlier in the stack if a route of the given name is already present there. `push` will always add on top, so a route can be present multiple times.

- `name` - _string_ - Name of the route to push onto the stack.
- `params` - _object_ - Screen params to pass to the destination route.

<samp id="stack-actions" />

```js
import { StackActions } from '@react-navigation/native';

const pushAction = StackActions.push('Profile', { user: 'Wojtek' });

navigation.dispatch(pushAction);
```

### pop

The `pop` action takes you back to a previous screen in the stack. It takes one optional argument (`count`), which allows you to specify how many screens to pop back by.

<samp id="stack-actions" />

```js
import { StackActions } from '@react-navigation/native';

const popAction = StackActions.pop(1);

navigation.dispatch(popAction);
```

### popTo

The `popTo` action takes you back to a previous screen in the stack by the name. It also allows you to pass params to the route.

If a matching screen is not found in the stack, this will pop the current screen and add a new screen with the specified name and params. This behavior is useful when the screen was opened from a deep link etc. and a previous screen with the name may or may not already be in the stack.

The method accepts the following arguments:

- `name` - _string_ - Name of the route to navigate to.
- `params` - _object_ - Screen params to pass to the destination route.

If a matching screen is not found in the stack, this will pop the current screen and add a new screen with the specified name and params. This behavior is useful when the screen was opened from a deep link and a previous screen with the name may or may not already be in the stack.

```js
import { StackActions } from '@react-navigation/native';

const popToAction = StackActions.popTo('Profile', { user: 'jane' });

navigation.dispatch(popToAction);
```

### popToTop

The `popToTop` action takes you back to the first screen in the stack, dismissing all the others. It's functionally identical to `StackActions.pop({n: currentIndex})`.

<samp id="stack-actions" />

```js
import { StackActions } from '@react-navigation/native';

navigation.dispatch(StackActions.popToTop());
```
