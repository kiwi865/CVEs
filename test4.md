# Stirling-PDF v1.3.2 - Server Side Request Forgery (SSRF)

### Summary
Stirling-PDF v1.3.2 uses WeasyPrint to convert HTML to PDF and does not sufficiently restrict remote resource fetching. An attacker-supplied URL inside submitted HTML img tag is fetched by the WeasyPrint URL fetcher, allowing the Stirling-PDF server to make HTTP requests to attacker-controlled or internal URLs. Because the underlying fetching is performed by WeasyPrint, this is an SSRF originating from unvalidated external resource loading in the HTML→PDF pipeline.

### PoC
Navigate to the URL to PDF function.
<img width="1161" height="545" alt="image" src="https://github.com/user-attachments/assets/467457c7-4d1c-4a4b-b18e-68eec940e703" />
Prepare the HTML file and host it.
<img width="888" height="287" alt="image" src="https://github.com/user-attachments/assets/63070429-683c-46c6-a1f7-042e824891f7" />
Upload to the server.
<img width="1617" height="591" alt="image" src="https://github.com/user-attachments/assets/4d5b7d1d-6145-44c6-bcc8-510ddfd3628c" />
Observed that there remote server connects to the attacker-supplied URLs.
<img width="1217" height="381" alt="image" src="https://github.com/user-attachments/assets/09f3eb77-e359-4749-ac74-fb43d7968864" />

