# IMA_Forensics

Image Metadata Analyzer – A Digital Forensic Tool

v2.7.0 Pro Stable Release

Submitted by:

Rhythm (Roll No. 590018178)

Harshit (Roll No. 590016614)

Tushar Arora (Roll No. 590017995)

Under the Guidance of: Mr. Kunwar Pankaj Siddhant School of Computer Science, UPES, Dehradun

📌 Abstract

The Image Metadata Analyzer is a web-based digital forensic tool designed to extract, analyze, and interpret hidden metadata from digital images. In the modern era, digital images serve as primary evidence in criminal and civil investigations. This tool automates the extraction of EXIF, GPS, and TIFF data to verify authenticity, detect tampering via software signatures (e.g., Photoshop), and reconstruct timelines.

🚀 Key Features

1. Advanced Metadata Extraction

Universal Support: Instantly processes JPEG, PNG, WEBP, TIFF, and HEIC formats.

Deep Scanning: Extracts extensive tag sets including Camera Model, Shutter Speed, Aperture, Software version, and Modification dates.

Search & Filter: Includes a real-time search bar to filter through hundreds of metadata tags instantly.

2. Digital Forensics & Security

Anomaly Detection Engine: Automatically flags suspicious files by detecting:

Editing software traces (Adobe Photoshop, GIMP, Lightroom).

Missing original creation timestamps.

Inconsistencies in GPS data.

Integrity Hashing: Calculates the unique SHA-256 Hash of the file to establish a chain of custody and prove the file hasn't been altered.

Thumbnail Recovery: Extracts and displays embedded thumbnails which often persist even if the main image is edited/cropped.

3. Geolocation Intelligence

Interactive Map: Plots the exact GPS coordinates on a dark-mode Leaflet map.

Google Maps Integration: Provides a direct link to open coordinates in Google Maps for Street View and satellite analysis.

4. Session Management & Input Options

Smart Drag-and-Drop: Interactive drag zone with visual feedback.

Clipboard Support: Paste images directly from your clipboard (Ctrl+V) without saving them first.

URL Analysis: Fetch images directly from web links. Includes a CORS Proxy toggle to bypass browser security restrictions on strict websites.

Session History: Keeps a log of all files analyzed in the current session with their risk status.

5. Reporting

Forensic Report Generation: Converts the dashboard into a clean, printable PDF report suitable for case files. (Hides UI buttons, expands all data tables).

Data Export: Download raw metadata as .json or copy to clipboard for external logging.

🛠️ Technology Stack

Frontend: HTML5, CSS3, Tailwind CSS (Responsive UI).

Logic: Modern JavaScript (ES6+).

Libraries:

exifr: For fast and robust metadata parsing.

Leaflet.js: For mapping and geolocation visualization.

Lucide: For iconography.

Privacy: 100% Client-Side. No images are uploaded to any server; all processing happens locally in the browser.

📖 Usage Guide

Step 1: Input Evidence

Option A: Drag and drop an image file into the dashed box.

Option B: Click the box to browse your device files.

Option C: Paste an image URL and click "Fetch Image". Use the "CORS Proxy" checkbox if the link fails to load.

Option D: Copy an image (screenshot/web) and press Ctrl+V anywhere on the page.

Step 2: Analyze Results

Preview Panel: Check the image, file size, format, and SHA-256 hash.

Anomaly Report: Look at the "Risk Score" (Green/Red) to see if tampering is detected.

Map: If GPS data exists, view the location on the map.

Step 3: Generate Output

Search: Use the search bar above the table to find specific tags (e.g., "Date").

Report: Click the "Report" button to print or save as PDF.

Export: Click "JSON" to save the raw data structure.

🔮 Future Scope

Integration of AI-based Deepfake detection.

Support for Video and Audio metadata extraction.

Cloud-based collaborative forensic analysis.

📄 License

Submitted in partial fulfillment of the requirements for the award of the degree of Master of Computer Applications.
