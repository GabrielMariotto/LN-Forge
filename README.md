# LN Forge - Your AI-Powered Light Novel Idea Lab

Yo! Welcome to LN Forge, the ultimate web app for brainstorming, outlining, and generating chapters for your next banger Light Novel, all powered by your own story blueprint and some AI magic (Gemini API).

This ain't just a fancy notepad; it's an interactive environment to bring your story to life, from a spark of an idea to full-blown chapters.

## Wtf is this thing? 

LN Forge takes your Light Novel blueprint (a `.md` file you create), uses AI to understand its structure (characters, world, plot, etc.), and then helps you:

* **Visualize Your Story:** See your blueprint's core concepts, character profiles, world-building notes, and plot structure all neatly laid out.
* **Generate Chapters:** Get the AI to write new chapters based on your blueprint and the story so far.
* **Manage Your Work:** Save, read, edit, and delete chapters as you go.
* **Get Inspired:** Use AI-powered "character whispers" to get quick, in-character thoughts.
* **Make It Yours:** Upload new blueprints or update your API key in the settings.

Basically, you drop your master plan, and this app helps you build the damn thing.

## Key Features 

* **Blueprint-First Design:** The app is a blank slate until you upload your `.md` blueprint.
* **AI-Powered Blueprint Parsing:** Gemini API reads your blueprint and structures its content to display in dedicated sections (Overview, Characters, World, Plot).
* **Dynamic Content Display:** The app's informational sections adapt to the content parsed from *your* blueprint.
* **AI Chapter Generation:**
    * Uses Gemini API to write new chapters.
    * Takes your **full raw blueprint** and the **full text of all previously saved chapters** as context for maximum continuity.
    * You can guide the AI on chapter length in the prompt (current default aims for 1000-1500 words, but adjustable in code).
* **Chapter Management (with Firebase Firestore):**
    * Save generated chapters.
    * List, read, and select saved chapters.
    * **Edit** chapter titles and content.
    * **Delete** chapters (with a custom confirmation, so no accidents!).
* **Character Whispers:** Get short, AI-generated in-character thoughts for your parsed characters.
* **Settings Panel:**
    * Input and save your personal Gemini API Key (stored in browser's localStorage).
    * Upload a new blueprint file at any time to switch projects or update your current one.
    * Option to re-parse the current blueprint with the AI (useful after API key update).
* **Responsive Design:** Built with Tailwind CSS to look good on different screens.

## How to Use This Bad Boy 

1.  **Get the Code:**
    * If you're just checking out the demo in a special environment (like a shared Canvas), it might just work!
    * To run it yourself (e.g., locally or host it), grab the single `index.html` (or whatever you named it) file.

2.  **Open in Browser:** Just open the `.html` file in your web browser.

3.  **Initial Setup (CRITICAL FOR EXPORTED VERSION):**
    * **Upload Your Blueprint:** The app will greet you with an upload screen. Select your `.md` blueprint file.
        * **Blueprint Format:** For the AI to parse your blueprint effectively and populate the app sections, your markdown file should be well-structured with clear headings (e.g., `## 1. Core Concept`, `### Logline:`, `## 2. Protagonist (MC)`, `**Name & Aliases:**`, etc.). The more detailed and organized it is (kinda like the `blueprint_template` you might have), the better the AI can understand it.
    * **API Key (IMPORTANT!):**
        * The app uses the Gemini API for parsing your blueprint and generating content.
        * When running the exported HTML file locally or self-hosting, **you NEED to provide your own Gemini API Key.**
        * Go to the **Settings** section in the app and paste your key there. Without it, AI features (blueprint parsing, chapter generation, whispers) will fail with an error.
    * **Firebase Firestore (For Saving Chapters):**
        * This app is coded to save your chapters to Google's Firebase Firestore (a cloud database).
        * For the *exported version* to save chapters persistently, you'd need to:
            1.  Create your own Firebase project at [firebase.google.com](https://firebase.google.com/).
            2.  Enable Firestore (Native mode).
            3.  Set up Authentication (Anonymous sign-in should be enabled for ease of use if you don't want user accounts).
            4.  Get your Firebase project's configuration details (apiKey, authDomain, projectId, etc.).
            5.  **Replace the placeholder `firebaseConfig` in the HTML file's `<script type="module">` section with your actual project config.**
        * If you don't do this Firebase setup for the exported version, chapter saving/loading **will not work**.

4.  **Explore & Create:**
    * Once your blueprint is loaded (and API key set), check out the Overview, Characters, World, and Plot sections.
    * Head to "LN Chapters" to generate your first chapter!
    * Edit, delete, and keep building your masterpiece.

## Tech Stack 

* **HTML5**
* **Tailwind CSS** (for styling and responsiveness)
* **Vanilla JavaScript (ES6 Modules)** (for all the logic, no big frameworks)
* **Chart.js** (for that one example pacing chart, could be expanded)
* **Google Gemini API** (for AI blueprint parsing, chapter generation, character whispers)
* **Firebase Firestore** (for cloud-based storage of your LN chapters)

## Blueprint Parsing & Accuracy 

The app now uses the Gemini AI to parse your uploaded `.md` blueprint based on a detailed schema (inspired by common LN outlining templates). The goal is to automatically populate the "Overview," "Characters," "World," and "Plot" sections of the app.

* **How it works:** You upload your blueprint, the app sends it to Gemini with specific instructions and a schema, and Gemini sends back structured data.
* **Accuracy:** The AI is pretty smart, but it's not perfect. The accuracy of the parsed content heavily depends on:
    * **The clarity and structure of your blueprint.md file.** Use clear headings (like `## Section Title`, `**Field Name:** Content`), lists, and consistent formatting. The closer your blueprint matches a well-defined structure (like the template you based this on), the better.
    * **The complexity of your blueprint.**
    * The AI's current understanding capabilities.
* **What if it's not perfect?**
    * The raw text of your blueprint is *always* used as the primary guide for **chapter generation**, so even if the display sections aren't 100% accurate from the parsing, the chapter writing AI gets the full raw truth.
    * You can always re-upload a revised blueprint or use the "Re-Parse Current Blueprint" button in Settings (especially if you update your API key or think the AI can do better with the current raw file).

## Known Issues & Limitations 

* **AI Parsing Imperfections:** As mentioned, the AI parsing of the blueprint might not always be 100% perfect for display in the app's sections. The more structured your `.md` file, the better.
* **Exported Version Dependencies:** Running the exported HTML file requires you to set up your own Gemini API Key and Firebase project for full functionality (AI features and chapter saving).
* **No Local File Saving for Chapters (Yet):** Chapters are saved to Firestore. There's no local file download/upload for chapters built-in.
* **Large Blueprint/Chapter Context:** Sending very large blueprints or many long previous chapters to the AI for chapter generation could hit API limits or slow down generation. The AI will try its best, but super long contexts can be challenging.
* **Theme:** The visual theme is currently fixed (dark mode with yellow accents). It doesn't dynamically change based on the blueprint content.

## Future Ideas? (Maybe... if you're feelin it)

* More advanced blueprint parsing error handling/feedback.
* Local chapter import/export.
* Deeper theme customization.
* ...your awesome ideas!

## Peace Out 

Hope this LN Forge helps you cook up some fire stories! If you dig it, give it a star!
