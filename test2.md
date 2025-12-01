# Stirling-PDF v1.3.2 - Cross Site Scripting (XSS)

### Summary
Cross-Site Scripting (XSS) in Stirling-PDF v1.3.2. An attacker can inject JavaScript into the pdf metadata that is not correctly escaped before being included in an HTML response. This allows execution of arbitrary script in the context of users’ browsers who view the crafted page.

### PoC
Use add metadata function to add metadata to a pdf file. Then, navigate to get info on pdf to retrieve the modified pdf file.

The title and author parameters are not correctly escaped, lead to the execution of arbitrary script.
<img width="940" height="625" alt="image" src="https://github.com/user-attachments/assets/fea0f54f-046a-4a8e-8382-08c7b624b64a" />

<img width="940" height="650" alt="image" src="https://github.com/user-attachments/assets/25e42838-a458-4585-b7d8-a4d57d1abb24" />

<img width="940" height="588" alt="image" src="https://github.com/user-attachments/assets/23351768-c1bf-48f3-ab16-550cbbda2e6d" />

<img width="940" height="799" alt="image" src="https://github.com/user-attachments/assets/47d90426-fd1c-43ae-b5e1-cdadd1994f66" />
