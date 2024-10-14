# Active_Directory

## Home.lab

This is my Active Directory lab. It was an exciting one where I created multiple servers of kali unbuntu, Windows server, and Windows 10 using Virtualbox. 

![Screenshot 2024-10-13 060210](https://github.com/user-attachments/assets/75a72af0-cc86-4e76-afb5-138337ae061c)

The plan is to connect both Windows images to Splunk, use Identity Managment tools by creating new users, and by intentionally compromising the account using Crowbar on Kali.


## Initial Set up

I launched an ubuntu server and launched enterprise Splunk onto it. 

![Screenshot 2024-10-13 203449](https://github.com/user-attachments/assets/468f5300-87f3-4110-a208-6b1c571ab646)

Once complete, I launched both windows servers. 

First I loaded Sysmon from Windows, then I launched a config by [Olaf](https://github.com/olafhartong/sysmon-modular) specifically the last file sysmonconfig.xml to ensure events were properly logged.

![Screenshot 2024-10-13 143623](https://github.com/user-attachments/assets/e98b1026-61f6-4db4-92bb-5078e9861446)

Next, I needed to ensure splunk forwarder was on both Windows and Windows server. This was tricky becuase I needed to ensure the inputs were being pulled locally.

To do this, I first opened notepad as admin, then copied MYDFIR'sSplunk local input by [mydfir](https://www.youtube.com/@MyDFIR) in order to pull data into server. I saved the file and conf and put it inthe local folder.![Screenshot 2024-10-13 203113]

(https://github.com/user-attachments/assets/0c837eb5-f0dc-4f14-b5f5-19f94450b981)

We needed to check to see if it was all working so I called up Services and checked. It's working. I ensured they were both using the correct Local Network protocols in order to ensure the forwarding happened correctly.

![Screenshot 2024-10-13 141038](https://github.com/user-attachments/assets/3a143343-c4a7-47a7-8bdd-b7be8dd00328)

I connected the AD server to the target pc. I made more Identities in the AD server. I ensured it was all set up properly.

![Screenshot 2024-10-13 145211](https://github.com/user-attachments/assets/9c693684-1625-41cb-84d5-7face13035a1)

![Screenshot 2024-10-13 151435](https://github.com/user-attachments/assets/f7e996d7-8d30-45b9-ad58-74e19e7c4f5a)

![Screenshot 2024-10-13 150900](https://github.com/user-attachments/assets/012bee5b-4ad0-4279-8f33-8662723fd823)

With all of that set up, the last check was to check via browser to see if the data was being fed.

![Screenshot 2024-10-13 141122](https://github.com/user-attachments/assets/7d69cec4-6ec2-40b5-bb74-26d45404b319)

I logged in and created an event-manager query in splunk so that all the events from either PC would show up on here. I also ensured the 9997 port was open for all 3 devices.

![Screenshot 2024-10-13 141322](https://github.com/user-attachments/assets/0073b645-ed7d-4334-9273-4b3314837ff0)

![Screenshot 2024-10-13 141532](https://github.com/user-attachments/assets/e80ffabd-dfb2-4fde-82bb-2f703b4f2b3b)

![Screenshot 2024-10-13 141645](https://github.com/user-attachments/assets/0b3c196e-2e86-4cf9-a0bb-7c13ef373fbd)

This shows both hosts were operational! We did it!

## Brute-force from the dark

![Screenshot 2024-10-13 155148](https://github.com/user-attachments/assets/57a14b77-c5e0-4c17-8657-3e0d419b0709)

It was time to use Kali. I've used unbuntu before many times. Kali was an interesting change of pace. First, I updated it, then I went right to work: I loaded up Crowbar. Crowbar is a bruteforce machine that will run the most common passwords at you at speed. I added the 'rock you' password file that's already found on Kali to work on breaking the code. I also added my alter ego Jenny Smith's password into that mix for good measure.

![Screenshot 2024-10-13 193108](https://github.com/user-attachments/assets/6a6b7046-64ef-4859-97a7-067d3d53f6e1)

Oh no, it worked. My 'super secure' password was no match! Let's check out Splunk and see if it found anything.

![Screenshot 2024-10-13 205642](https://github.com/user-attachments/assets/d78252c1-6f59-409f-97f3-c22e8db929fb)

25,000 events. It sure did. It sure did.

## Conclusion

This was super interesting. I've worked with Vanguard in the past and this was another with a new SIEM and server set up that I've never encountered before. 

I may add to this with Wazah and Thehive to see if I can make a case management/XDR next time I bruteforce!

