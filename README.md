# Flipbox Builder

A Flipbox Builder application built with Vue and TipTap. Users can create front and back content, apply rich-text formatting, and see their changes immediately in a live preview.

## Features

- Edit Front and Back flipbox content
- Bold formatting
- Italic formatting
- Bulleted lists
- Undo and Redo
- Live preview while editing
- Flip between Front and Back
- Save flipbox content
- Saved content persists after page refresh
- Keyboard-accessible flipbox interaction

## Technologies Used

- Vue.js
- Vite
- TipTap
- JavaScript
- HTML
- CSS

## Installation

Clone the repository:

git clone <YOUR-GITHUB-REPOSITORY-URL>

Go to the project folder:

cd flipbox-builder

Install dependencies:

npm install

## Run the Application

Start the development server:

npm run dev

Open the local URL displayed in the terminal, typically:

http://localhost:5173/

## How to Use

1. Enter content in the Front and Back editors.
2. Use the toolbar to apply Bold, Italic, or List formatting.
3. Changes appear immediately in the Preview.
4. Click the preview card to flip between Front and Back.
5. Click "Save Flipbox" to save the content.
6. Refresh the page to verify that saved content persists.

## Author

Sumathi Gottipati

## Project structure

```tree
src/
  App.vue                        # top-level layout (builder + preview)
  main.js
  style.css
  components/
    FlipboxBuilder.vue           # TODO: front/back editing, persistence
    FlipboxPreview.vue           # TODO: flip interaction, state communication
    RichTextEditor.vue           # TipTap wiring; TODO: formatting toolbar
  composables/
    usePersistence.js            # generic localStorage save/load helper

