# Requirements Document

## Introduction

A reusable Kiro skill that captures quiz results from teaching workspaces. It provides a lightweight local HTTP server that serves lesson HTML files, intercepts quiz answer submissions via runtime injection, and writes structured results to the filesystem — enabling the teaching agent to incorporate quiz performance data into learning records and zone-of-proximal-development calculations. The deliverable is a standalone skill folder (SKILL.md + server.mjs) that can be dropped into any teaching workspace.

## Glossary

- **Skill_Server**: The Node.js HTTP server (server.mjs) that serves lesson files and receives quiz result submissions
- **Injected_Snippet**: A JavaScript fragment inserted into served HTML responses at runtime that intercepts checkAnswer calls and reports results back to the Skill_Server
- **Quiz_Result**: A structured JSON object capturing a single quiz answer event (quiz ID, lesson file, selected answer, correct answer, correctness, timestamp)
- **Results_Directory**: The `./quiz-results/` directory in the workspace root where quiz result files are stored
- **Result_File**: A JSON file in the Results_Directory named `<lesson-name>_<YYYY-MM-DD>.json` containing an array of Quiz_Result objects
- **Lesson_File**: A self-contained HTML file in `./lessons/` containing inline CSS, JS, and quiz elements
- **Teaching_Agent**: The Kiro agent that reads quiz results to inform learning records and ZPD calculations
- **checkAnswer_Function**: The existing client-side function in lesson files that handles quiz answer feedback (button styling, feedback text)

## Requirements

### Requirement 1: Serve Lesson Files Over HTTP

**User Story:** As a learner, I want to access lessons through a local HTTP server, so that quiz results can be automatically captured without modifying lesson files on disk.

#### Acceptance Criteria

1. WHEN the Skill_Server is started with a workspace path, THE Skill_Server SHALL serve all files in the `./lessons/` directory over HTTP with correct MIME types (text/html, text/css, application/javascript)
2. THE Skill_Server SHALL listen on port 3333 by default
3. WHERE a custom port is specified via a `--port` CLI argument or `PORT` environment variable, THE Skill_Server SHALL listen on the specified port instead of the default, with the CLI argument taking precedence over the environment variable
4. WHEN a request is received for a path that resolves outside the `./lessons/` directory (including directory traversal attempts using `..` segments), THE Skill_Server SHALL respond with HTTP 404 and not serve the requested resource
5. WHEN a request is received for a file within the `./lessons/` directory that does not exist on disk, THE Skill_Server SHALL respond with HTTP 404
6. THE Skill_Server SHALL use only Node.js standard library modules (http, fs, path) with zero external dependencies
7. WHEN a request is received for a registered API route (such as `/api/results`), THE Skill_Server SHALL route the request to the appropriate handler rather than treating it as a lessons directory file request

### Requirement 2: Inject Quiz Result Reporting

**User Story:** As a skill developer, I want quiz result reporting injected at serve-time, so that lesson files on disk remain unmodified while quiz answers are automatically captured.

#### Acceptance Criteria

1. WHEN serving a Lesson_File with Content-Type text/html, THE Skill_Server SHALL inject the Injected_Snippet as a `<script>` block immediately before the closing `</body>` tag in the HTTP response without modifying the file on disk
2. THE Injected_Snippet SHALL wrap the existing checkAnswer_Function by saving a reference to the original and replacing `window.checkAnswer` with a new function that calls the original first, then captures result data — preserving all visible quiz behavior (button styling, feedback text, re-answer prevention via dataset.answered)
3. WHEN a quiz answer is submitted, THE Injected_Snippet SHALL POST a Quiz_Result object to the `/quiz-result` endpoint on the Skill_Server containing: quizId (the quiz element's `id` attribute), lessonFile (the filename portion of the current URL path), selectedAnswer (the textContent of the clicked button), correctAnswer (the textContent of the button whose onclick contains `true`), isCorrect (the boolean argument passed to checkAnswer), and timestamp (ISO 8601 UTC string generated at submission time)
4. WHILE a quiz element has already been answered (dataset.answered is set), THE Injected_Snippet SHALL not send duplicate result submissions for that quiz
5. IF the POST request to the Skill_Server fails due to network error or non-2xx response, THEN THE Injected_Snippet SHALL log the error to the browser console and allow the quiz to continue functioning normally without displaying any error to the learner
6. IF the served HTML file does not define a checkAnswer function on the window object, THEN THE Injected_Snippet SHALL skip wrapping and produce no errors in the browser console

### Requirement 3: Persist Quiz Results to Filesystem

**User Story:** As a teaching agent, I want quiz results written to structured JSON files, so that I can read performance data between turns to inform learning records.

#### Acceptance Criteria

1. WHEN a Quiz_Result is received via POST, THE Skill_Server SHALL append the result to the appropriate Result_File at `./quiz-results/<lesson-name>_<YYYY-MM-DD>.json` and respond with HTTP 201
2. IF the Results_Directory does not exist, THEN THE Skill_Server SHALL create it before writing the first result
3. THE Skill_Server SHALL store each Result_File as a JSON array of Quiz_Result objects, written with 2-space indented formatting
4. IF a Result_File contains corrupted or unparseable JSON (JSON.parse throws), THEN THE Skill_Server SHALL discard the corrupted content, start a fresh JSON array containing only the new result, and write it to the same file path
5. IF the filesystem write fails, THEN THE Skill_Server SHALL log the error to stderr and respond with HTTP 500 without crashing the process
6. THE Skill_Server SHALL serialize concurrent writes to the same Result_File so that rapid sequential POST requests do not corrupt the JSON array or lose results
7. IF the POST body is missing any required Quiz_Result field (quizId, lessonFile, question, selectedAnswer, correctAnswer, isCorrect, timestamp), THEN THE Skill_Server SHALL respond with HTTP 400 and an error message indicating which fields are missing, without writing to the Result_File

### Requirement 4: Graceful Degradation

**User Story:** As a learner, I want lessons to work normally even when the server is unavailable, so that infrastructure issues never block my learning.

#### Acceptance Criteria

1. WHILE the Skill_Server is not running, THE Lesson_File opened via file:// protocol SHALL accept quiz answers, apply correct/incorrect button styling, display feedback text, and prevent re-answering — without the Injected_Snippet present
2. IF the Injected_Snippet fails to POST a result (network error or HTTP error response), THEN THE Injected_Snippet SHALL suppress the error from the learner (no visible error messages or UI changes) and the quiz SHALL still apply button styling, display feedback text, and prevent re-answering
3. WHEN the Injected_Snippet reports a quiz result, THE Injected_Snippet SHALL send the POST asynchronously without blocking or delaying the quiz answer feedback (button styling and feedback text SHALL render before the POST completes)
4. WHILE the Skill_Server is running, THE Lesson_File served over HTTP SHALL produce the same button styling, feedback text, and re-answer prevention behavior as the file:// version (the Injected_Snippet SHALL not alter, remove, or delay any visible quiz behavior)

### Requirement 5: Skill Packaging

**User Story:** As a skill developer, I want the output packaged as a standard Kiro skill folder, so that it can be dropped into any teaching workspace and work immediately.

#### Acceptance Criteria

1. THE Skill_Server SHALL be implemented as a single `server.mjs` file within the skill folder
2. THE skill folder SHALL contain a SKILL.md file with frontmatter fields (name, description, disable-model-invocation, argument-hint) and a body that documents: the command to start the server, how to open lessons via the server URL, how to read and interpret quiz results, when to write learning records based on quiz performance, how to fall back if the server is unavailable, and the quiz HTML pattern the skill supports
3. WHEN the skill folder is placed in a workspace's `.kiro/skills/` directory and the server is started, THE skill SHALL serve lessons from the workspace's `./lessons/` directory relative to the current working directory, inject quiz result reporting, and write results to the workspace's `./quiz-results/` directory without any install steps or configuration
4. THE skill folder SHALL contain no dependencies outside Node.js standard library modules
5. WHEN the Skill_Server is launched, THE Skill_Server SHALL resolve the `./lessons/` and `./quiz-results/` paths relative to the current working directory (the workspace root), not relative to the skill folder location

### Requirement 6: Quiz Result Data Structure

**User Story:** As a teaching agent, I want quiz results to contain sufficient context, so that I can determine what the learner understood and what they got wrong without cross-referencing the lesson HTML.

#### Acceptance Criteria

1. THE Quiz_Result SHALL contain the following fields: `quizId` (the quiz element's ID attribute, e.g., "quiz1"), `lessonFile` (the lesson filename, e.g., "0008-flexbox.html"), `questionText` (the quiz question text), `selectedAnswer` (the text of the answer the learner clicked), `correctAnswer` (the text of the correct answer), `isCorrect` (a boolean indicating whether the selected answer was correct), and `timestamp` (an ISO 8601 datetime string with UTC offset, e.g., "2025-01-15T14:30:00Z")
2. WHEN a Quiz_Result is written, THE Injected_Snippet SHALL extract the question text from the `h3` element inside the quiz `div` and include it in the Quiz_Result as the `questionText` field
3. IF the quiz `h3` element is missing or contains no text content, THEN THE Injected_Snippet SHALL set the `questionText` field to an empty string
4. THE Result_File name SHALL follow the pattern `<lesson-name>_<YYYY-MM-DD>.json` where lesson-name is the lesson filename without the `.html` extension and the date is the UTC calendar day the result was recorded

### Requirement 7: Server Lifecycle Management

**User Story:** As a teaching agent, I want clear server lifecycle semantics, so that I can reliably start, detect, and stop the server using Kiro's background process management.

#### Acceptance Criteria

1. WHEN the Skill_Server starts successfully, THE Skill_Server SHALL print a single line to stdout in the exact format `Serving lessons at http://localhost:<port>` where `<port>` is the numeric port the server is listening on, within 5 seconds of process launch
2. IF the specified port is already in use, THEN THE Skill_Server SHALL exit with a non-zero exit code and print an error message to stderr that includes the port number that was unavailable
3. WHEN the Skill_Server receives a SIGTERM or SIGINT signal, THE Skill_Server SHALL stop accepting new connections, finish any in-progress response within 3 seconds, and then exit with code 0
4. IF an in-progress request does not complete within the 3-second shutdown window, THEN THE Skill_Server SHALL terminate the connection and exit with code 0
