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
