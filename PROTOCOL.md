# WispNet Protocol

Version 2.0.0 Draft 1 written by @FoxMoss and @r58playz

## Wisp Changes
WispNet maintains backwards compatibility with any standard Wisp server, except parsing hostnames on CONNECT packets. If a connection is made for the `wispnet` hostname open a TCP stream to your own internal WispNet server as defined above. If the hostname ends with `.wisp` then interpret the beginning section as a base64 encoded WispNet device ID.

WispNet has its own endpoint on the server for clients that want to listen for connections from others. It is not necessary to connect to this endpoint if you are only connecting to other WispNet clients. Currently the endpoint is `WISP_PREFIX/?net`.

Once the client connects to the WispNet endpoint, it must act as a Wisp server with only the WispNet protocol extension supported and required. The WispNet server must act as a Wisp client with only the WispNet protocol extension supported and required.

## Protocol Extension ID `0xF1` - WispNet
This protocol extension should only be used on the WispNet endpoint.

### Server (WispNet Client) Message
| Field Name | Field Type | Notes                                                                                                  |
|------------|------------|--------------------------------------------------------------------------------------------------------|
| Private    | `uint8_t`  | A boolean that specifies whether the WispNet client should be hidden from any probes by other clients. |

### Client (WispNet Server) Message
| Field Name | Field Type | Notes                                  |
|------------|------------|----------------------------------------|
| Client ID  | `uint32_t` | The WispNet client's unique device ID. |

### Packet Type `0xF1` - PROBE
This packet allows for a WispNet client to probe for other WispNet clients that are connected. This packet must always be sent with stream ID 0.

#### WispNet Client Message
The WispNet client does not need to send anything for this packet.

### WispNet Server Message
| Field Name | Field Type   | Notes                         |
|------------|--------------|-------------------------------|
| Client IDs | `uint32_t[]` | A list of WispNet device IDs. |
