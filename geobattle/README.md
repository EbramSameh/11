# GeoBattle Arena — Live Classroom Edition

GeoBattle is a single-page geography quiz for a teacher-led class. Students join from their own phones or laptops with a room PIN, answer timed multiple-choice questions, see an explanation after each round, and follow a shared leaderboard.

## Features

- 30 geography questions covering river systems, river processes, river landforms, topographic maps, and drainage patterns.
- Randomized question order for each game.
- 10, 20, or 30-question sessions and adjustable 10–30 second timers.
- PIN-based classroom rooms and a copyable invitation link.
- Realtime student joining, answer submissions, speed bonuses, answer streaks, and leaderboard updates.
- Short explanations after each answer to support learning, not only competition.
- Final class leaderboard and CSV export with per-question answers and accuracy.

## Publish with GitHub Pages

The files are in the `geobattle/` folder of this repository. If GitHub Pages is enabled for the repository, the expected project-site path is:

`https://ebramsameh.github.io/11/geobattle/`

If the link does not load, open the repository's **Settings → Pages** and publish from the `main` branch. The repository's existing root page is not replaced by this project.

## One-time Firebase setup for live multiplayer

GitHub Pages serves the interface, but it does not synchronize separate devices by itself. Live rooms use Firebase Authentication (anonymous sign-in) and Firebase Realtime Database.

1. Create a Firebase project at [Firebase Console](https://console.firebase.google.com/).
2. Add a **Web app** to the project and copy its Firebase configuration object.
3. In **Authentication → Sign-in method**, enable **Anonymous**.
4. In **Build → Realtime Database**, create a database and copy the database URL.
5. Open `database.rules.json` in this folder. Copy its JSON into **Realtime Database → Rules**, then publish the rules.
6. Open GeoBattle, expand **One-time setup for live multiplayer**, paste the Web App config as JSON, and choose **Save config on this device**.
7. Choose **Host a live class**. Copy the invite link and share it with students. The invitation link contains the public web configuration and room PIN, so students do not need to configure Firebase themselves.

The Firebase web config identifies the project; it is not a database password. Keep the database rules in place. Do not replace them with public read/write test rules. The app uses anonymous accounts and gives students permission to create their own nickname and submit one answer per question, while score updates are written by the host.

## Classroom workflow

1. The teacher creates a room and shares its invite link or six-digit PIN.
2. Students enter a nickname and join before the quiz begins.
3. The teacher chooses the question count and timer, then starts the quiz.
4. Each student submits one answer per question. Correct answers earn points, with a speed bonus and streak bonus.
5. The teacher reveals the answer and explanation, then advances to the next question.
6. At the end, the teacher downloads the CSV and uses the final leaderboard to review class progress.

## Notes and limitations

- Live multiplayer requires a correctly configured Firebase project and database rules. The solo static website cannot act as a shared database on its own.
- Room and score data remain in the configured Firebase database until you remove them from the Firebase Console. Avoid using real student sensitive information; nicknames are sufficient.
- The score system is designed for friendly classroom competition, not secure high-stakes assessment. It should not be used as the sole basis for grades.
- Question content is an editable starter bank; review it against your class syllabus before teaching with it.
