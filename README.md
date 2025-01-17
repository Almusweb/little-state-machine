<div align="center"><a href="https://lrz5wloklm.csb.app/"><img src="https://github.com/bluebill1049/little-state-machine/blob/master/docs/logo.png?raw=true" alt="Little State Machine - React Hooks for state management" width="140px" /></a>
    <h1>Little State Machine</h1>
    
State management made super simple
</div>

<div align="center">

[![npm downloads](https://img.shields.io/npm/dm/little-state-machine.svg?style=for-the-badge)](https://www.npmjs.com/package/little-state-machine)
[![npm](https://img.shields.io/npm/dt/little-state-machine.svg?style=for-the-badge)](https://www.npmjs.com/package/little-state-machine)
[![npm](https://img.shields.io/bundlephobia/minzip/little-state-machine?style=for-the-badge)](https://bundlephobia.com/result?p=little-state-machine)

</div>

<h2>✨ Features</h2>

- Tiny with 0 dependency and simple (715B _gzip_)
- Persist state by default (`sessionStorage` or `localStorage`)
- Build with React Hooks

<h2>📦 Installation</h2>

    $ npm install little-state-machine

<h2>🕹 API</h2>

#### 🔗 `StateMachineProvider`

This is a Provider Component to wrapper around your entire app in order to create context.

```tsx
<StateMachineProvider>
  <App />
</StateMachineProvider>
```

#### 🔗 `createStore`

Function to initialize the global store, invoked at your app root (where `<StateMachineProvider />` lives).

```tsx
function log(store) {
  console.log(store);
  return store;
}

createStore(
  {
    yourDetail: { firstName: '', lastName: '' } // it's an object of your state
  },
  {
     name?: string; // rename the store
     middleWares?: [ log ]; // function to invoke each action
     storageType?: Storage; // session/local storage (default to session)
  },
);
```

#### 🔗 `useStateMachine`

This hook function will return action/actions and state of the app.

```tsx
const { actions, state } = useStateMachine<T>({
  updateYourDetail,
});
```

<h2>💁‍♂️ Tutorial</h2>

Quick video tutorial on little state machine.

<a href="https://scrimba.com/scrim/ceqRebca">
<img src="https://raw.githubusercontent.com/bluebill1049/little-state-machine/master/docs/tutorial.png" />
</a>

<h2>📖 Example</h2>

Check out the <a href="https://codesandbox.io/s/wild-dawn-ud8bq">Demo</a>.

```tsx
import React from 'react';
import {
  StateMachineProvider,
  createStore,
  useStateMachine,
} from 'little-state-machine';

createStore({
  yourDetail: { name: '' },
});

function updateName(state, payload) {
  return {
    ...state,
    yourDetail: {
      ...state.yourDetail,
      ...payload,
    },
  };
}

function YourComponent() {
  const { actions, state } = useStateMachine({ updateName });

  return (
    <div onClick={() => actions.updateName({ name: 'bill' })}>
      {state.yourDetail.name}
    </div>
  );
}

export default () => (
  <StateMachineProvider>
    <YourComponent />
  </StateMachineProvider>
);
```

## ⌨️ Type Safety (TS)

You can create a `global.d.ts` file to declare your GlobalState's type.

Checkout the [example](https://codesandbox.io/s/typescript-forked-xs30h).

```ts
import 'little-state-machine';

declare module 'little-state-machine' {
  interface GlobalState {
    yourDetail: {
      name: string;
    };
  }
}
```

```tsx
import * as React from 'react';
import {
  createStore,
  useStateMachine,
  StateMachineProvider,
  GlobalState,
} from 'little-state-machine';

createStore({
  yourDetail: { name: '' },
});

const updateName = (state: GlobalState, payload: { name: string }) => ({
  ...state,
  yourDetail: {
    ...state.yourDetail,
    ...payload,
  },
});

const YourComponent = () => {
  const { actions, state } = useStateMachine({
    updateName
  });

  return (
    <div onClick={() => actions.updateName({ name: 'Kotaro' })}>
      {state.yourDetail.name}
    </div>
  );
};

const App = () => (
  <StateMachineProvider>
    <YourComponent />
  </StateMachineProvider>
);
```

<h2>⚒ DevTool</h2>

[DevTool](https://github.com/bluebill1049/little-state-machine-dev-tools) component to track your state change and action.

```tsx
import { DevTool } from 'little-state-machine-devtools';

<StateMachineProvider>
  <DevTool />
</StateMachineProvider>;
```

<h2>🖥 Browser Compatibility</h2>
Little State Machine supports all major browsers IE11 include !

If you run into issues, feel free to open an [issue](https://github.com/bluebill1049/little-state-machine/issues).

<h2>📋 Polyfill</h2>

Consider adding `Object.entries()` polyfill if you're wondering to have support for old browsers.
You can weather consider adding snippet below into your code, ideally before your App.js file:

`utils.[js|ts]`

```tsx
if (!Object.entries) {
  Object.entries = function (obj) {
    var ownProps = Object.keys(obj),
      i = ownProps.length,
      resArray = new Array(i); // preallocate the Array
    while (i--) resArray[i] = [ownProps[i], obj[ownProps[i]]];
    return resArray;
  };
}
```

Or you can add [core-js](https://github.com/zloirock/core-js) polyfill into your project and add `core-js/es/object/entries` in your `polyfills.[js|ts]` file.

## Sponsors

Thank you very much for those kind people with their sponsorship to this project.

<p>
    <a href="https://github.com/sayav"
    ><img
            src="https://avatars1.githubusercontent.com/u/42376060?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@sayav"
    /></a>
    <a href="https://github.com/lemcii"
    ><img
            src="https://avatars1.githubusercontent.com/u/35668113?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@lemcii"
    /></a>
    <a href="https://github.com/washingtonsoares"
    ><img
            src="https://avatars.githubusercontent.com/u/5726140?v=4"
            width="45"
            height="45"
            alt="@washingtonsoares"
    /></a>
    <a href="https://github.com/lixunn"
    ><img
            src="https://avatars.githubusercontent.com/u/4017964?v=4"
            width="45"
            height="45"
            alt="@lixunn"
    /></a>
    <a href="https://github.com/SamSamskies"
    ><img
            src="https://avatars2.githubusercontent.com/u/3655410?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@SamSamskies"
    /></a>
    <a href="https://github.com/peaonunes"
    ><img
            src="https://avatars2.githubusercontent.com/u/3356720?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@peaonunes"
    /></a>
    <a href="https://github.com/wilhelmeek"
    ><img
            src="https://avatars2.githubusercontent.com/u/609452?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@wilhelmeek"
    /></a>
    <a href="https://github.com/iwarner"
    ><img
            src="https://avatars2.githubusercontent.com/u/279251?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@iwarner"
    /></a>
    <a href="https://github.com/joejknowles"
    ><img
            src="https://avatars2.githubusercontent.com/u/10728145?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@joejknowles"
    /></a>
    <a href="https://github.com/chris-gunawardena"
    ><img
            src="https://avatars0.githubusercontent.com/u/5763108?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@chris-gunawardena"
    /></a>
    <a href="https://github.com/Tymek"
    ><img
            src="https://avatars1.githubusercontent.com/u/2625371?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@Tymek"
    /></a>
    <a href="https://github.com/Luchanso"
    ><img
            src="https://avatars0.githubusercontent.com/u/2098777?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@Luchanso"
    /></a>
    <a href="https://github.com/vcarel"
    ><img
            src="https://avatars1.githubusercontent.com/u/1541093?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@vcarel"
    /></a>
    <a href="https://github.com/gragland"
    ><img
            src="https://avatars0.githubusercontent.com/u/1481077?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@gragland"
    /></a>
    <a href="https://github.com/tjshipe"
    ><img
            src="https://avatars2.githubusercontent.com/u/1254942?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@tjshipe"
    /></a>
    <a href="https://github.com/krnlde"
    ><img
            src="https://avatars1.githubusercontent.com/u/1087002?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@krnlde"
    /></a>
    <a href="https://github.com/msutkowski"
    ><img
            src="https://avatars2.githubusercontent.com/u/784953?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@msutkowski"
    /></a>
    <a href="https://github.com/mlukaszczyk"
    ><img
            src="https://avatars3.githubusercontent.com/u/599247?s=60&amp;v=4"
            width="45"
            height="45"
            alt="@mlukaszczyk"
    /></a>
    <a href="https://github.com/susshma"
    ><img
            src="https://avatars0.githubusercontent.com/u/2566818?s=460&u=754ee26b96e321ff28dbc4a2744132015f534fe0&v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/MatiasCiccone"
    ><img
            src="https://avatars3.githubusercontent.com/u/32602795?s=460&u=6a0c4dbe23c4f9a5628dc8867842b75989ecc4aa&v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/ghostwriternr"
    ><img
            src="https://avatars0.githubusercontent.com/u/10023615?s=460&u=3ec1e4ba991699762fd22a9d9ef47a0599f937dc&v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/neighborhood999"
    ><img
            src="https://avatars3.githubusercontent.com/u/10325111?s=450&u=f60c932f81d95a60f77f5c7f2eab4590e07c29af&v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/yjp20"
    ><img
            src="https://avatars3.githubusercontent.com/u/44457064?s=460&u=a55119c84e0167f6a3f830dbad3133b28f0c0a8f&v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/samantha-wong"
    ><img
            src="https://avatars.githubusercontent.com/u/19571028?s=460&u=7421a02f600646b5836d5973359a257950cae8c4&v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/msc-insure"
    ><img
            src="https://avatars.githubusercontent.com/u/44406870?s=200&v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/ccheney"
    ><img
            src="https://avatars.githubusercontent.com/u/302437?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/artischockee"
    ><img
            src="https://avatars.githubusercontent.com/u/22125223?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/tsongas"
    ><img
            src="https://avatars.githubusercontent.com/u/2079598?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/knoefel"
    ><img
            src="https://avatars.githubusercontent.com/u/2396344?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/JGibel"
    ><img
            src="https://avatars.githubusercontent.com/u/1953965?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/gpalrepo"
    ><img
            src="https://avatars.githubusercontent.com/u/41862257?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/pjsachdev"
    ><img
            src="https://avatars.githubusercontent.com/u/43356139?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/svict4"
    ><img
            src="https://avatars.githubusercontent.com/u/1137112?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/raisiqueira"
    ><img
            src="https://avatars.githubusercontent.com/u/2914170?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/pashtet422"
    ><img
            src="https://avatars.githubusercontent.com/u/45594821?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/ozywuli"
    ><img
            src="https://avatars.githubusercontent.com/u/5769153?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/monkey0722"
    ><img
            src="https://avatars.githubusercontent.com/u/12868063?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/KATT"
    ><img
            src="https://avatars.githubusercontent.com/u/459267?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/jeroenvisser101"
    ><img
            src="https://avatars.githubusercontent.com/u/1941348?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/sainu"
    ><img
            src="https://avatars.githubusercontent.com/u/12888685?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/bkincart"
    ><img
            src="https://avatars.githubusercontent.com/u/22803185?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/37108"
    ><img
            src="https://avatars.githubusercontent.com/u/36793907?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/TadejPolajnar"
    ><img
            src="https://avatars.githubusercontent.com/u/40028548?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/hahnlee"
    ><img
            src="https://avatars.githubusercontent.com/u/16930958?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/ACPK"
    ><img
            src="https://avatars.githubusercontent.com/u/2019893?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/alex-semenyuk"
    ><img
            src="https://avatars.githubusercontent.com/u/5480441?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/Peter-AMD"
    ><img
            src="https://avatars.githubusercontent.com/u/28400709?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/hjaber"
    ><img
            src="https://avatars.githubusercontent.com/u/41503068?v=4"
            width="45"
            height="45"
    /></a>
    <a href="https://github.com/jprosevear"
    ><img
            src="https://avatars.githubusercontent.com/u/699616?v=4"
            width="45"
            height="45"
    /></a>
</p>
