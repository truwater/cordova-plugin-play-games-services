cordova-google-play-game
========================

Cordova Plugin For Google Play Game Service (Forked from ptgamr/cordova-google-play-game)

### Before you start

Understand about **Leaderboard** and **Achievement**. Setting up your game in Google Play Developer Console https://developers.google.com/games/services/android/quickstart

## Install

```
cordova plugin add https://github.com/artberri/cordova-google-play-game.git --variable APP_ID=you_app_id_here
```

## Usage

### Authentication

#### Sign in
You should do this as soon as your `deviceready` event has been fired. The plugin handles the various auth scenarios for you.

```
cordova.plugins.playGamesServices.auth();
```

#### Sign out
You should provde the option for users to sign out

```
cordova.plugins.playGamesServices.signout();
```

#### Auth status
To check if the user is already logged in (eg. to determine weather to show the Log In or Log Out button), use the following

```
cordova.plugins.playGamesServices.isSignedIn(function (result) {
	// ‘result’ is a JSON object with a single boolean property of ‘isSignedIn’
	// {
	// 		“isSignedIn” : true
	// }

	console.log(“Do something with result.isSignedIn”);
});
```

#### Player Information
Fetch the currently authenticated player's data.

```
cordova.plugins.playGamesServices.showPlayer(function (playerData) {
	...
	console.log(“Authenticated as ”+playerData['displayName']);
});
```


### Leaderboards

#### Submit Score

Ensure you have had a successful callback from `cordova.plugins.playGamesServices.auth()` first before attempting to submit a score. You should also have set up your leaderboard(s) in Google Play Game Console and use the leaderboard identifier assigned there as the `leaderboardId`.

```
var data = {
    score: 10,
    leaderboardId: "board1"
};
cordova.plugins.playGamesServices.submitScore(data);
```

#### Show all leaderboards

Launches the native Play Games leaderboard view controller to show all the leaderboards.

```
cordova.plugins.playGamesServices.showAllLeaderboards();
```

#### Show specific leaderboard

Launches directly into the specified leaderboard:

```
var data = {
	leaderboardId: "board1"
};
cordova.plugins.playGamesServices.showLeaderboard(leaderboardId);
```

### Achievements
#### Unlock achievement

Unlocks the specified achievement:

```
var data = {
	achievementId: "achievementId1"
};

cordova.plugins.playGamesServices.unlockAchievement(data);
```

#### Increment achievement

Increments the specified incremental achievement by the provided numSteps:

```
var data = {
	achievementId: "achievementId1",
	numSteps: 1
};

cordova.plugins.playGamesServices.incrementAchievement(data);
```

#### Show achievements

Launches the native Play Games achievements view controller to show the user’s achievements.

```
cordova.plugins.playGamesServices.showAchievements();
```

### Other

#### Success/Failure callbacks

For all methods, you can optionally provide custom success/failure callbacks.

For example:

```
var successfullyLoggedIn = function () { ... };
var failedToLogin = function () { ... };
cordova.plugins.playGamesServices.auth(successfullyLoggedIn, failedToLogin);

var data = { ... };
var successfullySubmittedScore  = function () { ... };
var failedToSubmitScore  = function () { ... };
cordova.plugins.playGamesServices.submitScore(data, successfullySubmittedScore, failedToSubmitScore);
```

## Platform

Currently, only Android is supported

## Donation:
Wish you dont mind buying me a cup of coffee (highfive)

[Donate](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=anh%2etrinhtrung%40gmail%2ecom&lc=US&item_name=Cordova%20Google%20Play%20Game&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHosted)

## License

[MIT License](http://ilee.mit-license.org)
