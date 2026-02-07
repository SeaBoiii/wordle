# ATS - Threadle

A Wordle-like word guessing game built with vanilla JavaScript, Tailwind CSS, and Supabase.

## Features

- **Daily Word Challenges**: New word puzzle every day with configurable word length
- **Smart Feedback**: Color-coded tiles showing correct, present, and absent letters
- **Persistent Progress**: Your game progress is saved using Supabase backend
- **Admin Panel**: Manage daily word schedules and view player statistics
- **Responsive Design**: Works seamlessly on desktop and mobile devices
- **Dictionary Validation**: Uses a comprehensive English word dictionary for validation

## Technologies Used

- **Frontend**: Vanilla JavaScript (no framework required)
- **Styling**: Tailwind CSS
- **Backend**: Supabase (for authentication, database, and storage)
- **Dictionary**: English word list from [dwyl/english-words](https://github.com/dwyl/english-words)

## Setup

### Prerequisites

- A [Supabase](https://supabase.com/) account and project
- A web server to serve the HTML file (or just open it locally)

### Supabase Configuration

1. Create a new Supabase project at [supabase.com](https://supabase.com/)

2. Create the following tables in your Supabase database:

   **schedules table:**
   ```sql
   create table schedules (
     date date primary key,
     word text not null
   );
   ```

   **progress table:**
   ```sql
   create table progress (
     client_id text not null,
     date date not null,
     player_name text,
     answer text,
     guesses text[],
     status text,
     primary key (client_id, date)
   );
   ```

   **admins table (optional, for admin panel):**
   ```sql
   create table admins (
     email text primary key
   );
   ```

3. Get your Supabase project credentials:
   - Go to Project Settings > API
   - Copy your `Project URL` and `anon/public` key

4. Create a `config.js` file in the root directory:
   ```javascript
   window.SUPABASE_URL = "your-project-url";
   window.SUPABASE_ANON_KEY = "your-anon-key";
   ```

   **Note**: The `config.js` file is gitignored to protect your credentials.

### Running the Game

1. Clone this repository:
   ```bash
   git clone https://github.com/SeaBoiii/wordle.git
   cd wordle
   ```

2. Create your `config.js` file with Supabase credentials (see above)

3. Open `index.html` in a web browser, or serve it using a local server:
   ```bash
   # Using Python 3
   python -m http.server 8000
   
   # Using Node.js http-server
   npx http-server
   ```

4. Navigate to `http://localhost:8000` in your browser

## Usage

### Playing the Game

1. **Start Guessing**: Type your guess using the on-screen keyboard or your physical keyboard
2. **Submit**: Press Enter to submit your guess
3. **Feedback**: 
   - 🟩 Green: Letter is correct and in the right position
   - 🟨 Yellow: Letter is in the word but in the wrong position
   - ⬜ Gray: Letter is not in the word
4. **Win or Lose**: You have `word length + 1` attempts to guess the word

### Admin Panel

1. Click the "Admin" tab in the navigation
2. Sign in with a Supabase account (email must be in the `admins` table)
3. Schedule daily words and manage the game

## Game Rules

- Number of attempts = word length + 1
- All guesses must be valid English words
- Game progress is automatically saved
- Each player gets one game per day

## Customization

You can customize the game by modifying these variables in `index.html`:

- `window.DICTIONARY_URL`: Change the word dictionary source
- Word length and attempts are dynamically set based on the daily word

## License

© Brought to you by the ATS Engagement Team

## Contributing

Feel free to submit issues and pull requests to improve the game!
