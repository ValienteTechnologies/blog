![Logo](/assets/img/2026-03-05/ghostbadger.png)

## The Last Mile

The hard work is done. You’ve successfully breached the perimeter, pivoted through the internal network, and demonstrated the critical impact of your findings. The data is all there, neatly organized within **Ghostwriter**, but now you face the most tedious part of any engagement: **The Delivery.**

For a penetration testing or red team consultancy, the report isn’t just a document, it’s the primary product. At our core, we are a **PDF-centric company**. Our clients expect polished, professional, and, most importantly, **secure** deliverables.

However, the "last mile" of reporting, moving from a collaborative database to a client-ready, password-protected PDF, is often fraught with manual friction. Standard workflows frequently rely on insecure methods for handling PDF passwords or require consultants to jump through hoops to ensure encryption matches the secrets stored in the firm's vault.

We realized that to maintain a high-velocity, high-security pipeline, we needed a dedicated bridge. We needed a tool that could respect the collaborative power of Ghostwriter while leveraging the programmatic security of **Vaultwarden** (Bitwarden) to handle sensitive PDF credentials.

That bridge is **Ghostbadger**.

## The Origin

As our team at **Valiente Technologies** scaled its operations, we found ourselves hitting a consistent bottleneck. We rely heavily on **Ghostwriter** to manage our findings, evidence, and collaborative drafting. It is an industry-standard tool for a reason, but every organization has its own unique output requirements.

For us, those requirements were non-negotiable:

1. **PDF-First Delivery:** Our clients expect high-fidelity, polished PDF reports that reflect the quality of the technical work performed.
2. **Zero-Knowledge Password Management:** We needed a way to handle PDF encryption passwords without consultants manually generating, storing, or (worst of all) emailing them in plaintext.

We were already using **Vaultwarden** (the lightweight, self-hosted Bitwarden implementation) to manage our internal secrets. It occurred to us: why not bridge the two?

### From Internal Script to Open Source Tool

What started as a collection of internal Python scripts eventually evolved into a cohesive rendering engine. We realized that the "friction" we were feeling, the gap between the reporting platform and the secure delivery platform, was likely a shared pain point across the industry.

We decided to polish the code, modularize the integration, and release it to the community. **Ghostbadger** was born from the idea that offensive security tools shouldn't just be about the "hack"; they should also support the professional, secure, and automated delivery of the results.

![Logo](/assets/img/2026-03-05/base.png)

## Key Features

Ghostbadger isn't just a simple conversion script; it’s a specialized engine designed to handle the nuances of professional security reporting. Here are the core features that help bridge the gap between data and delivery:

* **Native Ghostwriter Integration:** Ghostbadger hooks directly into the Ghostwriter API, pulling your findings, evidence, and project metadata without requiring manual exports or data manipulation.
* **Programmatic Vaultwarden Interaction:** Instead of manually setting PDF passwords, Ghostbadger communicates with your Vaultwarden instance. It can automatically retrieve or generate secure passwords, ensuring that your delivery security is as robust as your internal secret management.
* **High-Fidelity PDF Rendering:** We built this for a "PDF-centric" workflow. The engine produces clean, stakeholder-ready documents that maintain the formatting and professional look required for executive-level debriefs.
* **Automated Encryption Pipeline:** The entire process of securing the PDF is baked into the rendering flow. By the time the document is "finished," it is already encrypted and paired with its corresponding secret in your vault.
* **Open Source & Extensible:** Built with the community in mind, Ghostbadger is designed to be modular. Whether you want to tweak the rendering templates or integrate a different secret backend, the code is open for you to build upon.

![Logo](/assets/img/2026-03-05/vw.png)

## How it Works

Under the hood, Ghostbadger operates as a specialized Flask application that acts as a bridge between your reporting data and your secure delivery platform. Here is the technical flow of how a report moves through the pipeline:

1. **Authentication & Data Retrieval:** Using a Ghostwriter JWT token, the application connects to your instance via GraphQL. It fetches the complete report data, including findings, project metadata, and evidence.
2. **The Rendering Pipeline:** Ghostbadger utilizes a sophisticated rendering stack. It leverages a headless **Chromium** instance (via Playwright) combined with **WeasyPrint**. This allows us to use modern web technologies (HTML/CSS) to design complex report layouts that are then converted into pixel-perfect PDFs.
3. **Vaultwarden & Bitwarden Integration:** If enabled, the engine interfaces with the **Bitwarden CLI**. It doesn't just password-protect the PDF; it can automatically store those passwords in a specific Vaultwarden Organization or Collection and even generate **Bitwarden Send** links for secure, time-limited delivery to the client.
4. **Local Processing:** To ensure security and speed, the application handles evidence caching and template rendering locally, ensuring that sensitive engagement data is processed efficiently before the final encrypted output is generated.

## Getting Started

For detailed, step-by-step commands and environment variable configurations, head over to the **[Ghostbadger GitHub repository](https://github.com/ValienteTechnologies/ghostbadger)**. We’ve included a comprehensive README to get you up and running in minutes.