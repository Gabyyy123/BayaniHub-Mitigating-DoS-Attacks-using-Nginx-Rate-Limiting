# BayaniHub: Mitigating DoS-Attacks using Nginx-Rate-Limiting

Tools I Used
Target: My laptop running Zorin OS.
Web Server: Nginx (the software that runs the website).
Attacker: A Kali Linux VM.
Attack Tool: GoldenEye (a tool used to flood websites).
The Website: My project called BayaniHub.

How I Set It Up & Command

Installing the Server (Zorin OS)
First, I installed Nginx on my laptop:

*sudo apt install nginx -y || installing the nginx package
*sudo systemctl start nginx || start the nginx
*sudo systemctl stop nginx || stop the nginx
*sudo systemctl status nginx || to check if it is active running

Installing the Attack Tool (Kali Linux)

Then, I put the attack tool on my Kali machine:

*sudo apt install goldeneye -y || instaling the goldeneye on my KaliVM

Deploy BayaniHub Website

To make the website live, I had to move my project files to the Nginx root directory.
Nginx looks for files in /var/www/html/ by default.

*sudo cp -r /path/your/website/folder/. /var/www/html/

1. Define the Limit Zone:
sudo nano /etc/nginx/nginx.conf
You added this line inside the http block:
limit_req_zone $binary_remote_addr zone=mylimit:10m rate=1r/s;

2. Apply the Limit to the Site:
sudo nano /etc/nginx/sites-available/default
You added this line inside the location / block:
limit_req zone=mylimit;

Executing the Attack (Kali Linux)
You launched the attack against your Zorin IP address.

*goldeneye http://192.168.1.38 -w 50

Checking the Logs (Zorin OS)
While the attack was running, you checked the logs to see the defense in action.

*tail -f /var/log/nginx/error.log

Changing the http{...}
<img width="1356" height="735" alt="ss1" src="https://github.com/user-attachments/assets/54857443-afd5-4503-a428-99b68fc1c883" />

Changing the location /{...}
<img width="1356" height="735" alt="ss2" src="https://github.com/user-attachments/assets/596bcecc-c048-4798-8c7b-70842a1befd1" />

Running [ip a] to check ip
<img width="1356" height="735" alt="ss3" src="https://github.com/user-attachments/assets/d8891e05-55a0-44f2-88a7-a7b76d38ebe2" />

Checking the Status of nginx[active running]
<img width="1356" height="448" alt="nginxstatus_checking" src="https://github.com/user-attachments/assets/4ace12f0-64f5-4408-9bfe-67b928e25d25" />

Checking the http if it is running/live server
<img width="1353" height="693" alt="ss6" src="https://github.com/user-attachments/assets/8ee35981-287a-48a4-b1d5-92a2e8815503" />

Running the [Goldeneye] to test the website
![runningDoS](https://github.com/user-attachments/assets/aa1ac29c-a41c-4ba3-9bf1-70f3716e0863)

Checking the logs [tail -f /var/log/nginx/error.log]
<img width="1356" height="737" alt="ss4" src="https://github.com/user-attachments/assets/8f2df0dc-e3b5-4db9-b034-9d2e00ac5030" />

503 Service Temporary Unavailable[Evidence of Active Mitigation: The server serves a 503 error to protect hardware resources during the flood.]
<img width="1353" height="693" alt="ss5" src="https://github.com/user-attachments/assets/4e140fb2-52e8-4083-b6a5-e8f169b193d4" />

After Execution

I stopped the Goldeneye
![DoSstop](https://github.com/user-attachments/assets/48e0841c-2cda-4580-b0ad-5d7e022bb475)

The site are in good condition
<img width="1363" height="685" alt="afterexeDoS" src="https://github.com/user-attachments/assets/49bf31d1-537f-4c36-92d6-5e339c9f01ed" />

I stopped the nginx
<img width="532" height="37" alt="nginx_stoping" src="https://github.com/user-attachments/assets/96a6c5b2-92f1-43ce-878b-320fb1679177" />

Checking if the nginx is still activate
<img width="1356" height="695" alt="Screenshot from 2026-02-24 16-50-51" src="https://github.com/user-attachments/assets/775f8a3f-a236-4b40-ab03-2fa226e47c27" />

The webserver is already stop running due to the nginx is not activated
<img width="1356" height="695" alt="Screenshot from 2026-02-24 16-50-14" src="https://github.com/user-attachments/assets/0e56451b-bdfa-401a-8bef-44ffd608a12a" />

Conclusion
This project shows how I used a "shield" called Nginx Rate Limiting to protect my website, BayaniHub.  Even though the website showed a 503 error, this was actually a good thing! It proves the server was smart enough to block the bad traffic from my Kali Linux attack tool (GoldenEye) instead of crashing. By doing this, my Zorin OS laptop stayed safe, and its brain (CPU and RAM) did not get overwhelmed or frozen.

I did this project only for school and practice in my own private lab. Please do not use these tools or methods on real websites like Google, Facebook, or any other platform. Attacking websites you don't own is illegal and can get you into big trouble. Always be an ethical student and only practice on your own computers!







