# Stirling-PDF v1.4.0 – Bypass of URL restrictions in /api/v1/convert/url/pdf leads to Server-Side Request Forgery (SSRF) of Internal Resources

### Summary
A URL validation flaw in the URL→PDF conversion endpoint allows attackers to bypass the SSRF protection in Stirling-PDF v1.4.0 by abusing HTTP redirects. Although the pre-check uses a non-redirecting HEAD request, the downstream WeasyPrint process still follows redirects. An attacker can host a crafted redirector that points to an internal resource (e.g. 127.0.0.1, 169.254.169.254), causing the server to make unintended requests inside its own network or access cloud metadata.

### Details
The endpoint validates that the provided urlInput is reachable and not in a restricted list. The HEAD pre-check does not follow redirects. The validated (but untrusted) URL is then passed verbatim to WeasyPrint, which does follow redirects when fetching remote resources. An attacker can therefore host a site returning 302 Found → http://<internal-url>/<endpoint>. When the server processes this, WeasyPrint follows the redirect internally, effectively performing an SSRF.

### PoC
Observe that the application blocks internal URLs.
<img width="1765" height="428" alt="image" src="https://github.com/user-attachments/assets/e7bf65ae-0963-4e45-859d-11ec4e044b1f" />
Create app.py and host it internally.
<img width="908" height="307" alt="image" src="https://github.com/user-attachments/assets/7109bfa7-7253-427b-8bfc-1cde148889b1" />
<img width="1246" height="338" alt="image" src="https://github.com/user-attachments/assets/202bf41c-a418-4759-bfa5-4915f2f454f6" />
Then, create a public domain and port forwarding.
<img width="1404" height="524" alt="image" src="https://github.com/user-attachments/assets/7065e289-1fd4-407d-9703-5e6b6d38ac3c" />
Enter the URL `https://6157cb207a1e.ngrok-free.app` to the URL to PDF function and observe the response. The backend attempts to access the public domain and get redirected to the internal domain. However, the application is not hosted in AWS environment, hence it couldn't fetch the AWS metadata. 
<img width="1762" height="987" alt="image" src="https://github.com/user-attachments/assets/d7745d36-a8fd-409c-a3bc-ee71c3cf4ba5" />

