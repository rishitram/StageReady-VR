# StageReady VR

StageReady VR is a presentation practice room for students, researchers, and anyone getting ready to speak in front of a group. Bring a PDF, step into a room with a small virtual audience, and practice facing the people listening to you.

You can try the room in a regular desktop browser or, with a compatible headset and a secure HTTPS site, in WebXR. The project is still a prototype; headset and optional-service support depend on the setup described below.

## What you can do

- Upload a PDF and move through its pages while you practice. The current file limit is 20 MB.
- Look around a 3D practice room with a board and a seated audience.
- Start, pause, resume, and end a timed practice session.
- Review a summary of how long you faced the audience and the board. It tracks head direction and eye contact.
- Optionally record your practice audio in the browser and download it afterward.
- Optionally talk with a live audience member powered by ElevenLabs.
- Optionally request a written AI coaching summary based on session timing measurements.

## Try it

If you have been given a hosted StageReady VR link, open it in a recent browser and choose your PDF. Your PDF is processed in that browser; uploading it on a computer does not make it available on a separate headset.

To run the project on your computer:

1. Install [Node.js 24](https://nodejs.org/en/download/) (npm is included).
2. Clone this repository, then open a terminal in the project folder.
3. Install the app dependencies and start the local development server:

   ```sh
   cd app
   npm ci
   npm run dev
   ```

4. Open the local address printed by Vite, usually `http://localhost:5173`.
5. Choose a PDF, select **Enter Practice Room**, then choose **Enter Test Mode** to explore the room with your mouse. Use **Enter VR Mode** when you are ready to practice.

Test Mode supports mouse orbit, pan (Shift-drag), and zoom. Use the room controls to navigate PDF pages, start or pause practice, and finish a session. In VR, start from the headset's browser; you can also turn on voice Q&A before entering VR.

### Using a headset

Immersive WebXR needs a compatible browser and a trusted HTTPS connection. `localhost` is secure for desktop testing, but a headset opening your computer's local network address is not the same thing. Publish the app to an HTTPS host or use a trusted HTTPS development tunnel, then open that URL in the headset browser. Upload the PDF from the headset itself.

The desktop preview is useful for trying the room, but it does not verify headset tracking, microphone behavior, or VR performance. Those need to be tested on the actual device.

## Your files and privacy

- PDFs are rendered locally in the browser and are not uploaded to a project backend.
- Optional practice audio is recorded in the browser. You choose whether to enable the microphone and can download the resulting recording.
- Voice Q&A sends microphone audio to ElevenLabs; the audience agent cannot see or read your PDF.
- AI coaching sends timing measurements to AssemblyAI only when that service is configured and a summary is requested.
- Head direction is used for the practice summary. It is not eye tracking, a measure of eye contact, or a score of speaking quality.

## Technical overview

The app is a client-side React and TypeScript application built with Vite. Three.js renders the practice room and WebXR view; PDF.js turns the selected PDF page into a canvas that can be shown on the room's board. The browser keeps the PDF and its rendered pages local.

The optional voice feature uses the ElevenLabs React SDK and WebRTC. AI coaching is provided through a small Vite server middleware route, which keeps the AssemblyAI API key out of the browser. The room also records session timing and head-orientation data for its local summary.

## Team

Built by Rishi Ramachandran, Yuhaen Bhaskaran, and Karl Chen.
