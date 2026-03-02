# Development Plan for Platform Engineering Team

**Goal**  
Build a fully functional GB/T 28181 platform that can successfully register the TK-SURY01 smart helmet, receive live 1080P video streaming, handle various alarms (SOS, fall, collision, gas, etc.), support voice intercom/PTT, and provide stream distribution to web clients and third-party systems.

## Phase 1: Foundation
- Set up core **GB28181.Server** using **ZLMediaKit** <[Github](https://github.com/ZLMediaKit/ZLMediaKit)> (strongly recommended) or PJSIP + custom RTP layer.
- Implement basic SIP stack: REGISTER + Digest authentication + keep-alive (OPTIONS / MESSAGE).
- Set up Media Server to receive and decode RTP/RTCP streams (H.264/H.265 + G.711/AAC).
- Basic device registration and online status management.
- **Deliverable**: Helmet can successfully register and stay online with our platform.

## Phase 2: Core Features
- Catalog Query (MESSAGE + XML response).
- Real-time video on-demand (INVITE + SDP negotiation + RTP stream reception).
- Alarm subscription and notification (SUBSCRIBE + NOTIFY for SOS, fall, collision, etc.).
- **Deliverable**: Live video streaming + real-time alarm notifications working end-to-end.

## Phase 3: Advanced Features
- Voice broadcast and two-way intercom (PTT / group talk).
- Device control commands (configuration, image capture, etc.).
- Stream distribution: WebRTC / HLS / RTSP output for web frontend and third-party platforms.
- **Deliverable**: Full feature parity with Cloudwinner’s platform for the helmet.

## Phase 4: Testing, Optimization & Handover
- Integration testing with real device.
- Performance & load testing (multiple helmets simultaneously).
- Security hardening (TLS, authentication, rate limiting).
- **Deliverable**: Production-ready GB/T 28181 platform with full test cases.