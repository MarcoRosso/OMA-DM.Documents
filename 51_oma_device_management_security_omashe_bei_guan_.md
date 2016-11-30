# 5.1 OMA Device Management Security OMA设备管理安全
## 5.1.1 Credentials OMA设备管理安全
Four examples of suitable credentials exchanged between Devices and Device Management servers are shown in the following list.<br/>

1. A username (AAUTHNAME in [DMSTDOBJ]) that uniquely identifies the Device Management Server [DMTND] to a Device), a password (AAUTHSECRET in [DMSTDOBJ]) – to be coupled with the username, and a nonce (AAUTHDATA in [DMSTDOBJ]) – to prevent replay attacks where hashing algorithms are used with static data.
2. A username (AAUTHNAME in [DMSTDOBJ]) that identifies the Device to the Device Management Server), a password (AAUTHSECRET in [DMSTDOBJ]) – to be coupled with username, and a nonce (AAUTHDATA in [DMSTDOBJ]) – to prevent replay attacks where hashing algorithms are used with static data.
3. A certificate, as specified in [WAP-219-TLS]
4. A network, transport or server specific mechanism, for example WAP.
For the purpose of Server to Device authentication, if a username, password and nonce are used, the Server MUST use a different password for each client it serves, in order that a client (which possesses a shared secret based on this password) cannot pose effectively as this Server in a interaction with another client.
