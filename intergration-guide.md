# GB/T 28181-2022 Protocol Integration Guide

## 1. Protocol Overview

**GB/T 28181-2022** is the Chinese national standard for public security video surveillance networking systems. It defines the interconnection between platforms and front-end devices.

### Key Points
1. **Signaling Protocol**: Based on SIP (RFC 3261), transported over UDP/TCP/TLS.
2. **Media Protocol**: Based on RTP/RTCP for transmitting audio/video streams (H.264/H.265 video, G.711/AAC audio).
3. **Device Identification**: Uses 20-digit national standard coding (e.g., `34020000001320000001`).
4. **Directory & Business Control**: Commands are sent via SIP MESSAGE in XML format (Catalog, DeviceControl, Alarm, etc.).

### In This Project
- **Device Side (implemented by us)**: They have implemented the complete GB/T 28181-2022 protocol stack (signaling + media).
- **Platform Side (to be implemented by you)**: We are responsible for implementing the platform-side protocol functions to achieve full interconnection and interoperability with their device.

---

## 2. Implementation Checklist

![GB/T 28181-2022 Implementation Checklist - Platform Side vs Device Side](images/implementation-checklist.svg)

*SVG diagram showing Platform Side (our responsibility) and Device Side (already implemented by them) responsibilities with connections and protocols.*

---

## 3. Recommended Architecture

### 3.1 Architecture Diagram Description
The recommended system consists of the following core components:

- **Stream Server**: Receives and forwards media streams (PS over RTP)
- **GB28181.Server**: Core SIP gateway that handles GB/T 28181 protocol (registration, control, alarms, catalog, etc.)
- **Stream Service Camera**: The helmet device pushing streams
- **Config Server**: Centralized configuration management (via RPC)
- **Message Queue**: Asynchronous event reporting

### 3.2 Component Roles & Protocols
- **Stream Server ↔ Device**: PS over RTP
- **GB28181.Server ↔ Stream Server**: RTSP/GRPC for stream scheduling
- **GB28181.Server ↔ Device**: SIP Session (REGISTER, INVITE, MESSAGE, NOTIFY, etc.)
- **GB28181.Server ↔ Config Server**: RPC (GetConfig)
- **GB28181.Server ↔ Message Queue**: Report Message (MQ)

---

## 4. Main Signaling Flows

### 4.1 Device Registration (REGISTER)
**Flow:**
1. Device → Platform: REGISTER (no Authorization)
2. Platform → Device: 401 Unauthorized (with WWW-Authenticate)
3. Device → Platform: REGISTER (with Authorization Digest)
4. Platform → Device: 200 OK

**Notes:**
- `Expires` determines registration lifetime (recommended 3600 seconds).
- Platform must verify device ID and authentication.
- On failure, device should retry after a random delay.

### 4.2 Heartbeat / Keep-alive (OPTIONS / MESSAGE)
- Platform can periodically send OPTIONS or empty MESSAGE.
- Device must reply 200 OK within 5 seconds.
- Alternative: periodic re-REGISTER.

### 4.3 Catalog Query
**Flow:**
- Platform → Device: MESSAGE, `CmdType=Catalog`
- Device → Platform: MESSAGE response with XML containing device/channel list

**Example Request XML:**
```xml
<Message>
  <CmdType>Catalog</CmdType>
  <SN>123456</SN>
  <DeviceID>34020000001320000001</DeviceID>
</Message>
```

### 4.4 Real-time Video On-demand (INVITE)
**Flow:**
- Platform → Device: INVITE (SDP with receive IP/Port/Codec)
- Device → Platform: 200 OK (SDP with send IP/Port/Codec)
- Platform → Device: ACK
- RTP media stream starts

**Stop:** Platform → Device: BYE

### 4.5 Alarm Subscription & Notification
**Flow:**
- Platform → Device: SUBSCRIBE (Event: Alarm)
- Device → Platform: 200 OK
- On alarm: Device → Platform: NOTIFY (XML alarm info)
- Platform → Device: 200 OK

---

## 5. Media Stream Transmission
- Video Encoding: H.264 / H.265 (Payload Type 96/97, etc.)
- Audio Encoding: G.711 A-law/μ-law (Payload Type 98), AAC (optional)
- Transport Protocol: RTP/UDP (default), RTP/TCP supported
- The platform must receive RTP packets and decode/play/store them according to the SDP negotiation.
- Important: Firewall/NAT must open the RTP port range.