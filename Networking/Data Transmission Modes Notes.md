# Data Transmission Modes

## Definition
- **Transmission Mode**: The method by which data is transferred between devices, also known as communication mode or directional mode.
- **Purpose**: Determines the direction and flow of data over communication channels.

## Types of Transmission Modes
- Three main modes: Simplex, Half-Duplex, Full-Duplex.

### Simplex Mode
- **Description**: One-way communication where only the sender transmits, and the receiver only receives.
- **Characteristics**:
  - Data flows in a single direction.
  - Receiver cannot send data back to the sender.
- **Examples**:
  - Radio station (transmits to listeners, no feedback).
  - Keyboard (inputs data) and monitor (displays data).
- **Advantages**:
  - Utilizes full bandwidth for transmission, allowing more data transfer at once.
- **Disadvantages**:
  - Unidirectional; no inter-communication between devices.

### Half-Duplex Mode
- **Description**: Two-way communication, but only one direction at a time.
- **Characteristics**:
  - Devices can both send and receive, but not simultaneously.
  - Full bandwidth used for one direction at a time.
  - Supports error detection; receiver can request retransmission if errors occur.
- **Example**: Walkie-talkie (one party speaks, the other listens; simultaneous speaking causes distortion).
- **Advantages**:
  - Both devices can send/receive data.
  - Full bandwidth used during transmission.
- **Disadvantages**:
  - Delay occurs as one device must wait while the other transmits.

### Full-Duplex Mode
- **Description**: Simultaneous two-way communication.
- **Characteristics**:
  - Data flows in both directions at the same time.
  - Uses two simplex channels: one for each direction.
  - Fastest mode of communication.
- **Example**: Telephone (both parties talk and listen simultaneously).
- **Advantages**:
  - Simultaneous sending and receiving improves efficiency.
- **Disadvantages**:
  - Without a dedicated path, channel capacity splits, reducing bandwidth per direction.