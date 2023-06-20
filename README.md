# MOS-Connection

_A part of **[Sofie: The Modern TV News Studio Automation System](https://github.com/nrkno/Sofie-TV-automation/)**_

[![Tests](https://github.com/nrkno/sofie-mos-connection/actions/workflows/node.yaml/badge.svg)](https://github.com/nrkno/sofie-mos-connection/actions/workflows/node.yaml)
[![codecov](https://codecov.io/gh/nrkno/sofie-mos-connection/branch/master/graph/badge.svg?token=LQL02uXajF)](https://codecov.io/gh/nrkno/sofie-mos-connection)

Library for connecting to a MOS device using the [MOS Protocol](http://mosprotocol.com/).

This is a part of the [**Sofie** TV News Studio Automation System](https://github.com/nrkno/Sofie-TV-automation/).

## Getting started

```typescript
import { MosConnection } from '@mos-connection/connector'

let mos = new MosConnection(new ConnectionConfig({
	mosID: 'my.mos.application',
	acceptsConnections: true,
	profiles: {
		'0': true,
        '1': true,
        '2': true,
        '4': true
	},
	openRelay: true
	debug: false
}))
mos.onConnection((device: MosDevice) => { // called whenever there is a new connection to a mos-device
	if (device.hasConnection) { // true if we can send messages to the mos-server
	    device.getMachineInfo().then((lm) => {
			console.log('Machineinfo', lm)
		})
	}
	// Setup callbacks to pipe data:
	device.onRequestMachineInfo(() => {})
	device.onCreateRunningOrder((ro) => {})
	device.onDeleteRunningOrder((RunningOrderID: MosString128) => {})
	device.onReadyToAir(() => {})
	// ...
})
```

## Supported MOS profiles

| Profile   | Status                |
| --------- | --------------------- |
| Profile 0 | Implemented           |
| Profile 1 | Implemented           |
| Profile 2 | Implemented           |
| Profile 3 | Implemented           |
| Profile 4 | Implemented           |
| Profile 5 | Not implemented (yet) |
| Profile 6 | Not implemented (yet) |
| Profile 7 | Not implemented (yet) |

Pull Requests for the remaining profiles would be happily accepted!

## Packages

MOS-connection consists of 3 packages:

- **@mos-connection/connector** is a Node.js library is used to connect to MOS devices or act as a MOS Server/NCS.
  The `helper` and `model` functionality is included in this library as well.
- **@mos-connection/helper** is a library that provides various functions useful for those that prepare/handle data that will be sent to (or has been received by) the MOS-connection.
  The `model` functionality is included in this library as well.
- **@mos-connection/model** is a library that contains types and enums, useful for applications that handles MOS-data.

There is also a helper application **quickMos** designed to be a minimal mock MOS server for testing client applications.
