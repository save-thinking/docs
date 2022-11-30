# P2P Syncing with WebRTC framework

Contents:

- [Summary](#summary)
  - [Issue](#issue)
  - [Decision](#decision)
  - [Status](#status)
- [Details](#details)
  - [Constraints](#constraints)
  - [Positions](#positions)
  - [Argument](#argument)
- [Related](#related)
  - [Related decisions](#related-decisions)
- [Notes](#notes)

## Summary

### Issue

We want to use real time communication framework for syncing data between different devices of the user:

- We want user to be able to see consistent data across all devices.

- We want to allow data sharing between different browsers and devices.

### Decision

Decided on webRTC.

### Status

Decided on WebRTC, integration subject to availability of time.

## Details

### Constraints

We wanted to integrate an RPC framework with our app without having to change much of the existing core logic.
We wanted this to be an additional independent layer on top of our application implementation.

### Positions

We considered JSON-RPC. JSON-RPC is a stateless, light-weight remote procedure call (RPC) protocol.
Example with Semantic:

```html
rpc call with positional parameters: --> {"jsonrpc": "2.0", "method":
"subtract", "params": [42, 23], "id": 1} <-- {"jsonrpc": "2.0", "result": 19,
"id": 1} --> {"jsonrpc": "2.0", "method": "subtract", "params": [23, 42], "id":
2} <-- {"jsonrpc": "2.0", "result": -19, "id": 2}
```

We considered webRTC. With WebRTC, we can add real-time communication capabilities to our application that works on top of an open standard.

Example with webRTC:

```html
function sendData() { const data = dataChannelSend.value;
sendChannel.send(data); console.log('Sent Data: ' + data); }
```

### Argument

As above.

Specifically, WebRTC seems a better fit for our usecase. The technologies behind WebRTC are implemented as an open web standard and available as regular JavaScript APIs in all major browsers.

### Related decisions

The framework we choose may affect testability.

## Notes

Any notes here.
