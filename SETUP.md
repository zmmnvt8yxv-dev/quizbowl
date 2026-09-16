# Quizbowl

## Enable the free website

Open https://github.com/zmmnvt8yxv-dev/quizbowl/settings/pages

Under Build and deployment, select **Deploy from a branch**, choose **main** and **/(root)**, then **Save**. After deployment, GitHub displays the live link:

https://zmmnvt8yxv-dev.github.io/quizbowl/

## Play

1. The referee opens the website and taps **Host a game**.
2. Tap **Copy invite link** and send the link to friends.
3. Each player enters a unique name and taps **Join game**.
4. The host taps **Open first round**. The first buzz received by the host locks the round and names the winner.
5. The host uses **+1 / −1** on the live scoreboard to award or correct points, then taps **Next round**.

Scores carry across rounds. Disconnected players retain their points and can reclaim them with the same name. Closing or refreshing the host page ends the game and clears scores. The host should use a second device to participate as a player.

## Connection and fairness

Keep the host page visible and awake. Internet is required; the app uses PeerJS 1.5.5 and the free PeerJS Cloud signaling service. Some VPNs, corporate Wi-Fi, or cellular networks block peer-to-peer connections; try the same home Wi-Fi. Third-party service availability is not guaranteed. No paid backend, account, or API keys are required.

The winner is the first message received by the host, not a measurement of physical finger-press times. Network delay affects close calls. This is designed for casual games with trusted friends, up to 30 players. Room codes and player names are not authentication.

Game logic checks passed with a simulated DOM and transport, covering winner lockout, reset, stale buzz rejection, score changes and retention, duplicate names, and rejoining. Test on two phones on your intended network before quiz night; real cross-device connectivity has not been verified here.

## YouTube quizzes with automatic rounds

The host now has a **YouTube quiz · automatic rounds** panel.

1. Paste the quiz's YouTube link and click **Load video**.
2. Set either exact question start times (one per line, e.g. `0:15`, `0:45`, `1:20`) or an evenly spaced schedule (first question time, seconds per question, question count).
3. Optionally set an answer window to lock buzzers before the answer is revealed.
4. Click **Start timed quiz**. This restarts the video at the beginning and automatically opens each question as the playhead reaches its start time. If playback is blocked, tap Play in the video.
5. Award points as before. There is no need to press Next between questions.

**This is timing-based automation, not automatic recognition of questions in arbitrary videos.** YouTube's player API exposes playback time, not quiz question boundaries. Exact timings must be supplied once; interval mode is only appropriate for evenly spaced videos. Use **Add current video time** while previewing to build a timing list. Changes to timings apply the next time you start the timed quiz.

Everyone watches the host's video; player phones remain buzzers and scoreboards. Remote participants would need a separate shared viewing setup, whose delay can affect fairness.

Pausing, buffering, or hiding the host tab temporarily closes buzzers. Resuming an unanswered question reopens it if its answer window remains active. A winner stays locked until a different question. Forward/backward seeking follows the question at the new playhead position; it never rolls back points. The last question closes at its answer-window end or video end. Optional **Pause video when someone buzzes** requires the host to resume playback afterward.

**Use manual rounds** disables video timing and preserves the scoreboard. Videos that prohibit embedding or require unavailable sign-in may not play; use another video or manual mode. Keep the host tab visible and use the embedded player, rather than opening YouTube separately.

Run `node test.cjs` for deterministic tests with mocked DOM, YouTube, and peer transport. These cover manual lockout, score retention, time/URL validation, both schedule modes, transitions, stale buzzes, rewind, pause/resume, tab visibility, pause-on-buzz, completion, and cleanup. Actual YouTube playback and cross-phone networking still require a live-device check.
