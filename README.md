# Warp Engine Regulator - Frontend

This project controls the Warp Engine Regulator's Backend in order to run the Warp Engine intermix process in balanced fashion.
In order for it to work, both Regulator's Backend (running at http://localhost:3000) and also Frontend (running at http://localhost:5173) should be started up.
On Frontend's screen, user specifies his/her name and e-mail address, then pushes "Start", which starts up the Warp Engine. From this point on, the Warp Engine Regulator's Backend runs the process of keeping the engine's matter/antimatter mix in balance. Regulator's Frontend polls the Warp Engine's status as well as time elapsed from the Regulator's Backend every 1 second.
When user presses "Stop", the Frontend tells Backend to stop the Warp Engine intermix adjustment process.

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

