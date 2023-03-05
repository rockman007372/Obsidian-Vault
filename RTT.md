RTT stands for Round-Trip Time, which is the time it takes for a small packet of data to **travel from a sender to a receiver and back again**. RTT is commonly used as a measure of the latency or delay in a network connection.

RTT is an important metric in networking, as it can affect the performance of applications that rely on low latency, such as online gaming, video conferencing, and real-time communication. High RTT can cause delays and poor performance in these applications, while low RTT can improve responsiveness and user experience.

Network protocols and applications often use RTT measurements to optimize their performance. For example, TCP uses RTT measurements to adjust its retransmission timer and congestion window size, while video conferencing applications may adjust their video quality based on RTT measurements to improve user experience.

Non-persistent HTTP response time = 2 * RTT + **file transmission time**.

![[Pasted image 20220817020108.png]]