# Covey To-Do

A minimal, quadrant-based task manager inspired by the Eisenhower Matrix. Built with Vanilla JS and Firebase.

## Development Workflow

### Prerequisites
- **Git**
- **Node.js** (for local testing via `npx serve`)
- **Google Firebase Account** (for deployment)

### Local Development
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/officialpumpkin/Covey-To-Do.git
    cd Covey-To-Do
    ```

2.  **Start a local server:**
    Use `npx` to start a lightweight local web server for immediate feedback.
    ```bash
    npx serve .
    ```
    Open `http://localhost:3000` in your browser.

3.  **Make changes:**
    - Edit `index.html` directly (this is a single-file application).
    - Refresh the browser to see updates.

### Deployment
Deployment is **fully automated** via GitHub Actions.

1.  **Commit & Push:**
    When you are happy with your changes, push them to the `main` branch.
    ```bash
    git add .
    git commit -m "feat: description of changes"
    git push origin main
    ```

2.  **Automated Deploy:**
    - GitHub Actions detects the push.
    - It triggers the `.github/workflows/firebase-hosting.yml` workflow.
    - Your changes are deployed to **[https://covey-to-do-minimal.web.app/](https://covey-to-do-minimal.web.app/)**.

### Cloud Development (Firebase/Project IDX)
You can also edit this project directly in the cloud using **Firebase Project IDX**.
- The `.idx/dev.nix` file configures this environment.
- **Syncing:** Use the "Sync Changes" button in the IDE to pull/push changes to GitHub.
- **Note:** Always ensure you pull changes locally (`git pull`) after working in the cloud to keep your environments in sync.

## Project Structure
- `index.html`: The entire application (HTML, CSS, JS).
- `firebase.json`: Hosting configuration.
- `.github/workflows`: CI/CD automation scripts.
- `.idx/`: Configuration for Project IDX cloud environment.

## Security
- **API Keys:** Firebase API keys are restricted by HTTP Referrer in the Google Cloud Console.
- **Firestore:** Data is synced per-user under `users/{uid}/lists/default`.

## Contributing
1.  Check the `tasks/` folder for current product requirements documents (PRDs).
2.  Create a feature branch for major changes.
3.  Test locally using `npx serve`.
4.  Merge to `main` to release.

