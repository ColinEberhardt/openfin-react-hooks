# Openfin React Hooks : useOpenFin()

A collection of [React Hooks](https://reactjs.org/docs/hooks-intro.html) built on top of the [Openfin API](https://developers.openfin.co/docs/javascript-api).

## Getting Started

1. `npm install --save openfin-react-hooks`
2. `import {useDockWindow} from "openfin-react-hooks";`
3. Enjoy!

## Motive

Wrapping up the OpenFin API in a higher level hooks abstraction allows developers to share common functionality across React-based OpenFin applications.

Even the simpler hooks bridge across various versions of the OpenFin API, providing a consistent interface around OpenFin regardless of what environment the application resides within.

More complex hooks (e.g. `useDockWindow`) provide functionality that could save hours of development work if the same functionality was written from scratch.

## Hooks

Currently, the collection of hooks consists of the following:

| Name                              | Description                                                                         |
| --------------------------------- | ----------------------------------------------------------------------------------- |
| `useBounds`                       | Subscribe to the bounds of a window changing                                        |
| `useDocked`                       | Detects if the current window is docked                                             |
| `useDockWindow`                   | Dock a window to the edges of a screen                                              |
| `useFocus`                        | Listen to and affect focus of a window                                              |
| `useInterApplicationBusSend`      | Auto-magically send properties on the `InterApplicationBus` whenever they change    |
| `useInterApplicationBusPublish`   | Auto-magically publish properties on the `InterApplicationBus` whenever they change |
| `useInterApplicationBusSubscribe` | Subscribe to a topic on the `InterApplicationBus`                                   |
| `useMaximized`                    | Detects if the current window is maximized                                          |
| `useOptions`                      | Listen to and update window options                                                 |
| `useUserMovement`                 | Listen to and update whether user movement is enabled / disabled for a window       |
| `useZoom`                         | Listen to and update window zoom level                                              |
| `useChannels`                     | Use the Channels API to send/receive messages between windows or applications       |

## Example

The following example demonstrates the usage of the `useInterApplicationBusSubscribe` and `useInterApplicationBusSend` hooks in order to subscribe to the OpenFin [InterApplicationBus](https://cdn.openfin.co/jsdocs/stable/fin.desktop.module_InterApplicationBus.html) and send a message:

```
import {useInterApplicationBusSend, useInterApplicationBusSubscribe} from "openfin-react-hooks";

const IDENTITY = window.fin.Window.me;
const TOPIC = "demo-topic";

const Component = () => {
    const [name, setName] = useState("John Smith");
    const { data } = useInterApplicationBusSubscribe(IDENTITY, TOPIC);
    useInterApplicationBusSend(IDENTITY, TOPIC, name);
    return (
        <div>
            <input type="text" onChange={(e) => setName(e.target.value)} value={name} />
            <div><strong>Received Message:</strong> {data ? data.message : "None"}</div>
        </div>
    )
}
```

Usage examples for all of the hooks can be found in the interactive demo, as detailed below.

## Demo

If you'd like a demo of the current collection of hooks, you can do so by:

- Cloning the repository (e.g. `git clone https://github.com/ScottLogic/openfin-react-hooks.git`)
- Checkout the repository in your command line of choice (e.g. `cd c:/dev/openfin-react-hooks`)
- Run `npm install` and `npm run compile` within the root of the project directory
- Checkout the `demo` directory (e.g. `cd demo`)
- Run `npm install` and `npm run start` within the demo directory
- Once that's finished, execute `npm run launch` to see the demo application in all its glory
