Step 1 Check connectivity first
The initial terminal capture records successful ping replies from the target and the gateway, establishing that both were reachable before the traffic inspection
<img width="1253" height="773" alt="image" src="https://github.com/user-attachments/assets/83a64896-d8be-4843-ad0e-0f28bdd1f55d" />



Step 2 Turn on forwarding
IP forwarding was enabled on Kali so it could pass packets along while observing the traffic. The separate screenshot records the enabled setting.

<img width="549" height="152" alt="image" src="https://github.com/user-attachments/assets/12494811-491e-4492-99a0-826908c9a7c5" />



Step 3 Redirect the local exchange with ARP spoofing
The two terminal views show spoofed ARP replies addressed toward the target and toward the gateway. Both directions are needed for the illustrated interception path.
<img width="911" height="550" alt="image" src="https://github.com/user-attachments/assets/d2addcf3-5a45-43da-8343-32e6ad425d71" />
<img width="941" height="307" alt="image" src="https://github.com/user-attachments/assets/a842730a-80ef-48e8-bdf2-2597d547aacc" />



Step 4 Observe packets at Kali
A Wireshark capture filtered for traffic involving the target shows network packets passing during the exercise. On the Metasploitable terminal, a ping to the gateway completes while the capture is running.
<img width="1653" height="762" alt="image" src="https://github.com/user-attachments/assets/2429534a-631f-45e4-9ea5-e9b70eac4af6" />
<img width="815" height="409" alt="image" src="https://github.com/user-attachments/assets/53c9cab0-73c8-4f4a-b2ef-d616f4ed98c1" />



Step 5 Inspect the web exchange and outcome
The filtered capture lists a POST /dvwa/login.php request using HTTP. The final browser view shows the DVWA page after login, confirming that the test session was authenticated.
<img width="1670" height="842" alt="image" src="https://github.com/user-attachments/assets/7ffd3773-237c-43ee-98f2-5fd34368ae91" />
<img width="1658" height="865" alt="image" src="https://github.com/user-attachments/assets/ae5a1266-cdaf-4c1a-b4cf-22ab3415ae06" />
