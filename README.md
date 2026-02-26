# Voice-Tracked Teleprompter

A simple, self-contained HTML-based teleprompter that automatically scrolls and highlights text as you speak. Built with the Web Speech API, it tracks your progress in real-time, allowing for a natural and hands-free presentation experience.

## Key Features

- **Voice-Tracked Scrolling**: Automatically advances the script and highlights the current word in yellow as you speak, using the browser's built-in Web Speech API.
- **Adjustable Font Size**: Easily increase or decrease the text size during your presentation for optimal readability.
- **Configurable Skip-Ahead Window**: Includes a slider to adjust the "lookahead" sensitivity (3 to 30 words). Lower it for noisy environments or increase it if you tend to skip lines.
- **Manual Navigation**: Click any word in the script to instantly jump the prompter to that position.
- **Clean, Responsive UI**: A modern interface built with Tailwind CSS and Lucide Icons, featuring a distraction-free dark mode for the prompter view.

## How to Use

1. **Open the App**: Open `teleprompter.html` in a web browser that supports the Web Speech API (best experienced in **Google Chrome** or **Safari**).
2. **Input Your Script**: Paste or type your presentation script into the text area on the setup screen.
3. **Configure Settings**:
    - Use the **Skip-Ahead Window** slider to adjust how aggressively the prompter searches for spoken words.
    - If you need to clear the script, use the **Clear** button.
4. **Start the Prompter**: Click the **Start Prompter** button.
5. **Grant Microphone Access**: The browser will request permission to use your microphone for speech recognition.
6. **Present**: Speak naturally. The prompter will highlight the current word in yellow and scroll automatically to keep your place centered in the view.
7. **On-the-fly Adjustments**:
    - Use the **Font Size** buttons in the top right to adjust text scale.
    - Click any word to manually jump the prompter to that part of the script.
    - Click **Stop & Edit** to return to the setup screen.

## Technical Details

- **Frontend**: HTML5, JavaScript (ES6+)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) (via CDN)
- **Icons**: [Lucide Icons](https://lucide.dev/)
- **Voice Tracking**: [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API)

## Browser Compatibility

This application requires the Web Speech API, which is most reliably supported in:
- Google Chrome (Desktop)
- Safari (Desktop & iOS)
- Microsoft Edge

*Note: Microphone access is required for the auto-scrolling feature to work.*
