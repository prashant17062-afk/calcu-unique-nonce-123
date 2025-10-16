# Academic Captcha Solver

## Summary
This project presents a client-side web application designed for academic grading, showcasing the ability to solve image-based captchas. It dynamically retrieves a captcha image from a URL provided in the query parameters, displays it, and then utilizes the Tesseract.js library for Optical Character Recognition (OCR) to extract and display the embedded text. The application prioritizes clear UI, robust error handling, and performance tracking, making it suitable for educational demonstrations of client-side AI capabilities.

## Features
*   **Dynamic URL Handling:** Captcha image URL is passed via the `?url=` query parameter, allowing for flexible testing. A default sample image is used if no URL is specified.
*   **Interactive Display:** The provided URL and the fetched captcha image are clearly displayed on the webpage.
*   **OCR Integration:** Leverages Tesseract.js, a JavaScript OCR engine, to perform text recognition directly within the user's browser.
*   **Performance Monitoring:** Measures and displays the exact time taken for the OCR recognition process, aiding in performance evaluation.
*   **User Feedback:** Provides real-time loading indicators for Tesseract.js initialization, image loading, and captcha solving, enhancing user experience.
*   **Comprehensive Error Handling:** Gracefully manages potential issues such as invalid image URLs, image loading failures (e.g., CORS restrictions), and OCR processing errors, displaying informative messages.
*   **Client-Side Execution:** The entire recognition process runs in the browser, demonstrating a self-contained web solution without requiring a custom backend server for OCR.
*   **Professional User Interface:** Features a clean, academic-appropriate design with clear separation of content and results.

## Setup
To deploy and run this application:

1.  **Download:** Save the `index.html` file to your local computer.
2.  **Open in Browser:** Navigate to the saved `index.html` file using any modern web browser (e.g., Google Chrome, Mozilla Firefox, Microsoft Edge).

**Important Note on CORS:**
When fetching images from external websites, browsers enforce Cross-Origin Resource Sharing (CORS) policies. If the image server does not explicitly permit requests from your `file://` (local file) origin or your local web server's origin, the image loading will fail. For optimal testing, especially with external URLs, it is recommended to serve `index.html` via a simple local HTTP server (e.g., using Python: `python -m http.server 8000` in the directory containing `index.html`, then accessing `http://localhost:8000`).

## Usage
The application can be used by opening `index.html` directly or by providing a captcha image URL in the browser's address bar.

*   **Default Captcha:** If you open `index.html` without any query parameters, it will automatically load and attempt to solve a predefined sample captcha image.
    *   Example: `file:///path/to/your/index.html` or `http://localhost:8000/index.html`

*   **Custom Captcha (via URL):** To solve a specific captcha image, append the `?url=` parameter followed by the direct link to your image file.
    *   Syntax: `index.html?url=https://example.com/path/to/your/image.png`
    *   **Example:**
        `http://localhost:8000/index.html?url=https://tesseract.projectnaptha.com/img/eng_text.png`
        (This URL is a safe default often used by Tesseract.js for testing. Replace it with your actual captcha image URL.)

Upon loading, the page will display the image URL, the captcha image itself, and then, after processing, the recognized text. A timer will indicate how long the OCR process took, along with any relevant warnings if performance targets (e.g., 15 seconds) are not met.

## Main Code Logic

The entire application is encapsulated within a single `index.html` file, which includes HTML for structure, CSS for styling, and JavaScript for functionality.

1.  **HTML Structure:** Defines the user interface elements, including headings, paragraphs for displaying information (URL, status, results), an `<img>` tag for the captcha image, and areas for loading indicators and error messages.
2.  **CSS Styling:** Provides a clean, modern, and professional aesthetic using Google Fonts (Roboto) and a responsive layout, ensuring a good user experience.
3.  **Tesseract.js Integration:**
    *   The Tesseract.js library is loaded via a CDN (`unpkg.com`), enabling client-side OCR without server-side dependencies.
    *   A Tesseract worker is initialized asynchronously using `Tesseract.createWorker('eng')` as soon as the `DOMContentLoaded` event fires. This proactive initialization is crucial for performance, allowing the heavy OCR engine setup to occur in parallel with other page rendering.
    *   The `'eng'` language pack is specified, instructing Tesseract.js to recognize English characters.
4.  **URL Parameter Handling:** A JavaScript utility function, `getUrlParameter('url')`, parses the browser's URL query string to extract the image URL. A default image URL is provided as a fallback.
5.  **Image Loading and Display:** The extracted URL is assigned to the `src` attribute of the `<img>` tag (`#captchaImage`). `onload` and `onerror` event listeners handle the image's loading state, updating the UI to show or hide the image and placeholder text, and managing error messages if the image fails to load.
6.  **Captcha Recognition Process:**
    *   Once the captcha image has successfully loaded, the `tesseractWorker.recognize(captchaImageElement)` method is invoked.
    *   A high-resolution timer (`performance.now()`) is used to precisely measure the start and end times of the OCR recognition, allowing for accurate performance reporting.
    *   The `loadingIndicator` element provides visual feedback throughout the recognition phase.
7.  **Result and Performance Display:** The `text` property from Tesseract.js's recognition result is extracted, trimmed, and displayed in the `#solvedText` area. The calculated recognition time is presented in the `#performanceMetric` element, accompanied by a warning if the 15-second threshold is exceeded.
8.  **Robust Error Management:** Specific error messages are displayed for common issues such as Tesseract worker initialization failures, image loading problems (including potential CORS warnings), and general OCR exceptions, guiding the user towards troubleshooting.

## License
This project is distributed under the **MIT License**. For complete details, please refer to the license text embedded within the `index.html` file's footer.

## Contact
For any inquiries, feedback, or support regarding this Captcha Solver, please feel free to open an issue on the project's repository (if applicable) or reach out to the developer via [Your Academic Email or Preferred Contact Method].