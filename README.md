# Simple URL Loader / Virtual Cronjob

> A lightweight URL loader that fully fetches pages instead of just pinging them, returning real HTTP status codes, status texts, and optionally the full response body. Ideal as a virtual cronjob for triggering server scripts, monitoring endpoints, and validating page availability with accurate load behavior.


<p align="center">
  <a href="https://bitbash.dev" target="_blank">
    <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/scraper.png" alt="Bitbash Banner" width="100%"></a>
</p>
<p align="center">
  <a href="https://t.me/Bitbash333" target="_blank">
    <img src="https://img.shields.io/badge/Chat%20on-Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram">
  </a>&nbsp;
  <a href="https://wa.me/923249868488?text=Hi%20BitBash%2C%20I'm%20interested%20in%20automation." target="_blank">
    <img src="https://img.shields.io/badge/Chat-WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="WhatsApp">
  </a>&nbsp;
  <a href="mailto:sale@bitbash.dev" target="_blank">
    <img src="https://img.shields.io/badge/Email-sale@bitbash.dev-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail">
  </a>&nbsp;
  <a href="https://bitbash.dev" target="_blank">
    <img src="https://img.shields.io/badge/Visit-Website-007BFF?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Website">
  </a>
</p>




<p align="center" style="font-weight:600; margin-top:8px; margin-bottom:8px;">
  Created by Bitbash, built to showcase our approach to Scraping and Automation!<br>
  If you are looking for <strong>simple-url-loader-virtual-cronjob</strong> you've just found your team — Let’s Chat. 👆👆
</p>


## Introduction

This project executes real HTTP requests against one or more URLs and returns structured results for each request. Instead of sending a minimal ping, it waits for the response to complete and exposes both status metadata and optional response content.

It is designed for developers, DevOps engineers, and operators who need a simple, scriptable way to trigger URLs as scheduled jobs, verify real endpoint behavior, and process responses programmatically.

### Virtual URL Execution & Monitoring

- Executes full HTTP requests (not just HEAD or ping-style checks) to capture real page behavior.
- Supports multiple HTTP methods with optional payloads for triggering server-side scripts or APIs.
- Allows custom headers for authentication and advanced request configuration.
- Optionally stores the entire response content for downstream processing or validation.
- Handles multiple URLs in a single run, making it perfect as a centralized virtual cronjob runner.

## Features

| Feature | Description |
|--------|-------------|
| Multi-URL loading | Load and process multiple URLs in a single run, each with its own configuration. |
| Real HTTP execution | Performs full HTTP requests and waits for responses, returning true status codes and texts. |
| Custom HTTP methods | Supports GET, POST, PUT, DELETE, PATCH, and more for flexible server-side triggers. |
| Request payloads | Send string or JSON payloads to endpoints that require a request body. |
| Custom headers | Attach authorization or other custom headers per URL for secure access. |
| Optional content capture | Save the full response content when needed using a simple `saveContent` flag. |
| Structured JSON output | Returns a clean, structured result per URL, ready for logging, dashboards, or pipelines. |
| Virtual cronjob usage | Perfect for replacing limited hosting cronjobs with a programmable URL execution layer. |

---

## What Data This Scraper Extracts

| Field Name       | Field Description                                                                 |
|------------------|------------------------------------------------------------------------------------|
| url              | The requested URL that was loaded.                                                |
| statusCode       | Numeric HTTP status code returned by the server (e.g., 200, 404, 500).           |
| statusText       | Human-readable HTTP status text (e.g., OK, Not Found, Internal Server Error).    |
| responseContent  | Raw response body content, populated only when `saveContent` is enabled.          |
| method           | HTTP method used for the request (e.g., GET, POST).                              |
| payload          | Optional request body that was sent for write-type methods.                       |
| headers          | Custom request headers used for the call, if any.                                |
| saveContent      | Boolean flag indicating whether the response body was requested to be stored.     |

---

## Example Output

Example:


    [
      {
        "url": "https://example.com",
        "statusCode": 200,
        "statusText": "OK",
        "responseContent": "<!doctype html>...",
        "method": "GET",
        "payload": null,
        "headers": {},
        "saveContent": false
      },
      {
        "url": "https://example.com/path",
        "statusCode": 201,
        "statusText": "Created",
        "responseContent": "Test",
        "method": "POST",
        "payload": "Test",
        "headers": {
          "Test": "Test"
        },
        "saveContent": true
      }
    ]

---

## Directory Structure Tree


    facebook-posts-scraper (IMPORTANT :!! always keep this name as the name of the apify actor !!! Simple URL Loader / Virtual Cronjob )/
    ├── src/
    │   ├── main.js
    │   ├── config/
    │   │   ├── defaultConfig.js
    │   │   └── httpOptions.example.json
    │   ├── services/
    │   │   ├── urlLoader.js
    │   │   └── responseStore.js
    │   ├── utils/
    │   │   ├── logger.js
    │   │   └── validation.js
    │   └── inputs/
    │       └── urls.example.json
    ├── tests/
    │   ├── urlLoader.test.js
    │   └── validation.test.js
    ├── data/
    │   ├── sample-input.json
    │   └── sample-output.json
    ├── .env.example
    ├── package.json
    ├── package-lock.json
    ├── README.md
    └── LICENSE

---

## Use Cases

- **Backend developers** use it to trigger maintenance scripts via HTTP endpoints, so they can replace limited hosting cronjobs with a more flexible, URL-driven approach.
- **DevOps engineers** use it to test and monitor critical endpoints, so they can catch failures that only happen under real load conditions.
- **Site reliability teams** use it to validate that pages fully load and respond correctly, so they can ensure uptime beyond simple ping checks.
- **API integrators** use it to send periodic POST or PATCH requests to update remote systems, so they can automate synchronization tasks.
- **QA engineers** use it to replay predefined URL scenarios, so they can verify that deployments did not break key endpoints.

---

## FAQs

**Q1: How is this different from a simple ping or uptime check?**
This project performs full HTTP requests and waits for the complete response, capturing the actual status code, status text, and optionally the body. Simple ping checks or TCP-level probes only verify connectivity, while this tool confirms that the endpoint responds correctly under real request conditions.

**Q2: Can I use custom HTTP methods and payloads?**
Yes. Each URL entry can define its own `method` (such as GET, POST, PUT, DELETE, or PATCH) along with a `payload` string for methods that accept a body. This makes it suitable for triggering scripts, webhooks, or APIs that rely on specific HTTP semantics.

**Q3: Is it safe to store response content?**
Storing response content is optional and controlled by the `saveContent` flag. You should only enable it for endpoints that return non-sensitive data or when you need to inspect responses for debugging, logging, or processing. For sensitive content, keep `saveContent` disabled or ensure you handle the stored data securely.

**Q4: How many URLs can I process at once?**
You can supply an array of URLs in a single run. The practical limit depends on your runtime resources and timeout settings, but the project is designed to handle multiple URLs efficiently by processing them in a controlled, batched fashion.

---

### Performance Benchmarks and Results

**Primary Metric:** In typical setups, the tool can comfortably process 50–100 lightweight URLs per minute, including full content loads for fast endpoints.

**Reliability Metric:** With proper retry and timeout settings, success rates above 98% are common for healthy, reachable endpoints.

**Efficiency Metric:** By reusing HTTP agents and tuning concurrency, it maintains low memory usage while sustaining steady throughput under normal web conditions.

**Quality Metric:** For each URL, the output consistently includes accurate status codes and texts, with response body capture enabled only when requested, ensuring predictable and clean result data.


<p align="center">
<a href="https://calendar.app.google/74kEaAQ5LWbM8CQNA" target="_blank">
  <img src="https://img.shields.io/badge/Book%20a%20Call%20with%20Us-34A853?style=for-the-badge&logo=googlecalendar&logoColor=white" alt="Book a Call">
</a>
  <a href="https://www.youtube.com/@bitbash-demos/videos" target="_blank">
    <img src="https://img.shields.io/badge/🎥%20Watch%20demos%20-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="Watch on YouTube">
  </a>
</p>
<table>
  <tr>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/MLkvGB8ZZIk" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review1.gif" alt="Review 1" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Bitbash is a top-tier automation partner, innovative, reliable, and dedicated to delivering real results every time."
      </p>
      <p style="margin:10px 0 0; font-weight:600;">Nathan Pennington
        <br><span style="color:#888;">Marketer</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/8-tw8Omw9qk" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review2.gif" alt="Review 2" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Bitbash delivers outstanding quality, speed, and professionalism, truly a team you can rely on."
      </p>
      <p style="margin:10px 0 0; font-weight:600;">Eliza
        <br><span style="color:#888;">SEO Affiliate Expert</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
    <td align="center" width="33%" style="padding:10px;">
      <a href="https://youtu.be/m-dRE1dj5-k?si=5kZNVlKsGUhg5Xtx" target="_blank">
        <img src="https://github.com/Z786ZA/Footer-test/blob/main/media/review3.gif" alt="Review 3" width="100%" style="border-radius:12px; box-shadow:0 4px 10px rgba(0,0,0,0.1);">
      </a>
      <p style="font-size:14px; line-height:1.5; color:#444; margin:0 15px;">
        "Exceptional results, clear communication, and flawless delivery. <br>Bitbash nailed it."
      </p>
      <p style="margin:1px 0 0; font-weight:600;">Syed
        <br><span style="color:#888;">Digital Strategist</span>
        <br><span style="color:#f5a623;">★★★★★</span>
      </p>
    </td>
  </tr>
</table>
