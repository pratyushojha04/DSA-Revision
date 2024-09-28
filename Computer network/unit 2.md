### **Framing**

**Framing** is a technique used in data link layer protocols to ensure reliable communication over a network by defining the structure and boundaries of the data being transmitted. Framing involves breaking the data stream into manageable units called **frames**. Each frame contains a portion of the original data along with necessary information for successful communication.

#### **Key Components of a Frame**
1. **Header**: Contains control information such as the source and destination addresses, and sometimes sequence numbers, to help identify the frame.
2. **Payload**: The actual data being transmitted.
3. **Trailer**: Contains error detection information, like a **cyclic redundancy check (CRC)**, which is used to verify if the data has been transmitted correctly.

#### **Types of Framing Methods**
1. **Character Count**: Uses a field in the header to indicate the number of characters (bytes) in the frame. The receiver uses this count to determine the end of the frame.
   - **Advantage**: Simple to implement.
   - **Disadvantage**: Errors in the count field can lead to the incorrect identification of frame boundaries.

2. **Byte Stuffing (Character Stuffing)**: Uses special characters to indicate the start and end of a frame, such as the **flag** character. If these special characters appear in the payload, they are "stuffed" (modified) to avoid confusion.
   - Example: The **SLIP** (Serial Line Internet Protocol) uses byte stuffing for framing.
   - **Advantage**: Simple to implement and understand.
   - **Disadvantage**: Inefficient for large data due to increased overhead.

3. **Bit Stuffing**: Inserting non-information bits into the data to differentiate between the actual frame and control sequences. In bit stuffing, a sequence like **01111110** is used to denote the start and end of a frame, and if five consecutive **1s** appear in the data, a **0** is stuffed to avoid misinterpretation.
   - Example: Used in protocols like **HDLC (High-Level Data Link Control)**.
   - **Advantage**: Provides better efficiency in certain cases compared to byte stuffing.
   - **Disadvantage**: Requires more processing to detect and remove the stuffed bits.

4. **Physical Layer Coding Violations**: Used mainly in physical layer protocols like **Ethernet**, where specific code patterns represent the beginning and end of frames. Violations in normal coding are used to indicate frame boundaries.

#### **Framing Challenges**
- **Synchronization**: Ensuring that the sender and receiver agree on frame boundaries.
- **Error Detection and Recovery**: Ensuring frames are delivered without errors by using techniques like **CRC** and requesting retransmissions if errors are detected.

#### **Importance of Framing**
- **Data Integrity**: By adding a header and trailer to each frame, framing helps ensure that data is transferred accurately.
- **Error Control**: Framing helps in detecting and managing errors in data transmission.
- **Efficient Medium Usage**: Framing allows multiple devices to share the same communication channel without interference.

**Framing** is an essential part of the data link layer's responsibilities to ensure that the data sent from the sender reaches the receiver without errors and in an organized manner.



### **Error Detection and Correction**

Error detection and correction are crucial for ensuring reliable data communication in computer networks, as errors can occur due to noise, attenuation, or interference.

#### **Error Detection Methods**
1. **Parity Check**
   - **Single Parity Bit**: Adds a single bit (0 or 1) to make the number of 1s in the data either even (even parity) or odd (odd parity). It helps detect a single-bit error.
   - **Limitation**: Cannot detect multiple errors effectively.

2. **Cyclic Redundancy Check (CRC)**
   - A **polynomial code** that uses a generator polynomial to create a CRC value. The sender appends this value to the message, and the receiver uses it to verify the integrity of the data.
   - **Commonly used** in Ethernet and other data link layer protocols due to its effectiveness in detecting burst errors.

3. **Checksum**
   - The data is divided into segments, and the sum of these segments is sent along with the data. The receiver recalculates the sum and compares it with the received checksum to detect errors.
   - Widely used in **transport layer protocols** like **TCP**.

4. **Hamming Code**
   - **Error Correction**: Detects and corrects single-bit errors by adding redundant bits to the data.
   - **Hamming Distance**: The minimum number of bits that differ between two codewords. Hamming code achieves a distance of 3, allowing the detection of up to 2-bit errors and correction of 1-bit errors.

#### **Error Correction Methods**
1. **Forward Error Correction (FEC)**
   - Adds enough redundancy to allow the receiver to correct errors without retransmission. Useful in situations where retransmission is not possible, such as satellite communication.
   - Examples: **Hamming Code**, **Reed-Solomon Code**.

2. **Automatic Repeat Request (ARQ)**
   - Uses acknowledgments and timeouts to detect and correct errors.
   - **Types of ARQ**:
     - **Stop-and-Wait ARQ**: Sender sends one frame and waits for an acknowledgment (ACK). If a **negative acknowledgment (NAK)** or a timeout occurs, the sender retransmits the frame.
     - **Go-Back-N ARQ**: Uses a sliding window where the sender can transmit multiple frames, but if an error occurs, all frames from the erroneous frame onward are retransmitted.
     - **Selective Repeat ARQ**: Only the frames with errors are retransmitted, improving efficiency compared to Go-Back-N.


### **Flow Control**

Flow control ensures that a sender does not overwhelm a receiver with data faster than it can be processed. It helps maintain proper data flow between devices with different processing capabilities.

#### **Elementary Data Link Protocols**
1. **Stop-and-Wait Protocol**
   - The sender sends a frame and waits for an acknowledgment from the receiver before sending the next frame.
   - **Advantages**: Simple to implement.
   - **Disadvantages**: Inefficient for long-distance communication due to idle time during waiting.

2. **Sliding Window Protocols**
   Sliding window protocols are more efficient for flow control and error control. The idea is that both sender and receiver have a "window" of frames that they can send or receive before requiring an acknowledgment.

   - **Window Size**: Determines the number of frames that can be transmitted before needing an acknowledgment.

#### **Sliding Window Protocol Types**
1. **Go-Back-N**
   - The sender can send multiple frames up to a window size **N** without waiting for an acknowledgment.
   - If an error is detected in a frame, the receiver discards all subsequent frames, and the sender has to retransmit those frames.
   - **Efficiency**: Better than Stop-and-Wait but can be inefficient when a large number of frames are discarded.

2. **Selective Repeat**
   - The sender also sends multiple frames up to a window size **N**, but only frames that are not acknowledged are retransmitted.
   - The receiver stores frames that arrive out of order and waits for the missing frame to arrive to pass them to the upper layer.
   - **Efficiency**: More efficient than Go-Back-N, especially in networks with a high error rate.

#### **Key Components of Sliding Window Protocols**
1. **Window Size**: Affects throughput and performance.
   - The **larger** the window size, the higher the throughput, as more frames can be sent before requiring an acknowledgment.

2. **Acknowledgments (ACKs)**: Sent by the receiver to notify successful receipt of frames.
   - **Cumulative ACKs**: Acknowledge all frames up to a specific point.
   - **Individual ACKs**: Acknowledge each frame separately.

3. **Sequence Numbers**: Used to identify each frame uniquely.
   - Sequence numbers must be large enough to avoid confusion due to wrap-around when the window moves.

### **Summary**
- **Error Detection** methods, like parity, CRC, and checksum, help identify errors in transmitted data, while **error correction** techniques like FEC and ARQ fix errors.
- **Flow Control** prevents data overflow and helps maintain a steady flow between sender and receiver. Protocols like **Stop-and-Wait** and **Sliding Window** (Go-Back-N and Selective Repeat) are used to manage flow and ensure reliable communication.

# Numericals

Sure! Here are some numerical problems related to **Framing, Error Detection, Correction, and Flow Control**:

### Numerical Problems

#### 1. **CRC Calculation (Error Detection)**
**Problem 21**: 
A sender wants to transmit the data **1101011011** using a **Cyclic Redundancy Check (CRC)** with a generator polynomial **x³ + x + 1**. Convert the generator polynomial to binary and determine the transmitted frame after appending the CRC bits.

**Solution**:  
The generator polynomial **x³ + x + 1** is represented as **1011** in binary.  
The original data is **1101011011**. To calculate the CRC, append 3 zeros (since the generator polynomial is of degree 3) to the data: **1101011011000**.

Now, perform the division of **1101011011000** by **1011** using modulo-2 arithmetic, and determine the remainder. Append the remainder to the original data to obtain the transmitted frame.

#### 2. **Window Size in Go-Back-N ARQ**
**Problem 22**: 
In a **Go-Back-N ARQ** protocol, if the sender window size is **4** and the sequence numbers range from **0 to 7**, what will be the next frame number sent if frames **0, 1, 2, 3** are transmitted and an ACK is received for frame **0**?

**Solution**:  
The sender window initially contains frames **0, 1, 2, 3**. Upon receiving an acknowledgment for frame **0**, the window shifts to **1, 2, 3, 4**. Therefore, the next frame to be sent will be **frame 4**.

#### 3. **Efficiency of Stop-and-Wait ARQ**
**Problem 23**: 
In a **Stop-and-Wait ARQ** protocol, the round-trip time (RTT) between the sender and receiver is **30 ms**, and the time required to transmit a frame is **5 ms**. Calculate the efficiency of the protocol.

**Solution**:  
The efficiency (\(\eta\)) of the **Stop-and-Wait ARQ** is given by:

\[
\eta = \frac{\text{Transmission Time}}{\text{Transmission Time} + \text{Round-Trip Time}}
\]

\[
\eta = \frac{5}{5 + 30} = \frac{5}{35} = 0.1429 \approx 14.3\%
\]

#### 4. **Selective Repeat ARQ**
**Problem 24**: 
In a **Selective Repeat ARQ** protocol, the sender window size is **4**, and the sequence numbers range from **0 to 7**. If frames **0, 1, 2, 3** are sent and an ACK is received for frame **1**, which frames will the sender retransmit if frame **2** is lost?

**Solution**:  
In **Selective Repeat ARQ**, only the lost frame is retransmitted. Since frame **2** is lost, only **frame 2** will be retransmitted. Frames **0, 1, 3** are considered successfully received, and frame **4** will be the next new frame to be sent.

#### 5. **Error Detection with Hamming Code**
**Problem 25**: 
A **7-bit Hamming code** is received as **1011011**. Calculate the position of the erroneous bit (if any) using the **Hamming code error detection** method.

**Solution**:  
Calculate the parity bits based on the received code and compare them with the expected parity. If there is a mismatch, the sum of the erroneous parity bits gives the position of the error. For example, if **P1** and **P3** are incorrect, the error position is **P1 + P3 = 1 + 4 = 5**. Therefore, the **5th bit** is erroneous.

#### 6. **Propagation Delay and Efficiency in Sliding Window**
**Problem 26**: 
Consider a **sliding window protocol** with a window size of **4** frames. The propagation delay is **20 ms**, and the transmission time for one frame is **10 ms**. Calculate the efficiency of the sliding window protocol.

**Solution**:  
The efficiency (\(\eta\)) can be calculated as:

\[
\eta = \frac{\text{Transmission Time}}{\text{Transmission Time} + \text{Propagation Delay}}
\]

For a window size of **4**:

\[
\eta = \frac{4 \times 10}{4 \times 10 + 20} = \frac{40}{60} = 0.6667 \approx 66.67\%
\]

#### 7. **Bit Stuffing Example**
**Problem 27**: 
Consider a bitstream **0111111110** that needs to be transmitted using bit stuffing. After bit stuffing, what will be the transmitted bitstream?

**Solution**:  
With **bit stuffing**, a **0** is inserted after every sequence of five **1s** to prevent confusion with the flag sequence. Therefore, the bitstream after bit stuffing will be:

\[
011111\underline{0}1110 = 01111101110
\]

#### 8. **Throughput Calculation in Sliding Window**
**Problem 28**: 
If a **sliding window protocol** has a window size of **8** frames, each of size **1000 bits**, and the bandwidth of the channel is **1 Mbps** with a round-trip time (RTT) of **50 ms**, calculate the throughput of the channel.

**Solution**:  
The throughput (\(T\)) can be calculated as:

\[
T = \frac{\text{Window Size} \times \text{Frame Size}}{\text{RTT}}
\]

\[
T = \frac{8 \times 1000 \, \text{bits}}{50 \, \text{ms}} = \frac{8000 \, \text{bits}}{0.05 \, \text{s}} = 160,000 \, \text{bps} = 160 \, \text{kbps}
\]

#### 9. **Window Size Calculation for Selective Repeat ARQ**
**Problem 29**: 
In a **Selective Repeat ARQ** protocol, if the sequence number field is **3 bits** long, calculate the maximum window size for the sender and the receiver.

**Solution**:  
For **Selective Repeat ARQ**, the window size is at most **(2^(k-1))**, where **k** is the number of bits in the sequence number.

\[
\text{Maximum Window Size} = 2^{3 - 1} = 2^2 = 4
\]

#### 10. **Bandwidth-Delay Product Calculation**
**Problem 30**: 
Calculate the **bandwidth-delay product** for a link with a **bandwidth** of **10 Mbps** and a **round-trip time (RTT)** of **200 ms**. What does this value represent?

**Solution**:  
The **bandwidth-delay product** is given by:

\[
\text{Bandwidth-Delay Product} = \text{Bandwidth} \times \text{RTT}
\]

\[
= 10 \times 10^6 \, \text{bps} \times 0.2 \, \text{s} = 2 \times 10^6 \, \text{bits} = 2 \, \text{Mb}
\]

This value represents the maximum number of bits that can be in transit in the network at any given time.