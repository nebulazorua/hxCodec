# hxCodec - Native video support for OpenFL & HaxeFlixel

[Original Repository](https://github.com/polybiusproxy/PolyEngine).  
[Click here to check the roadmap of hxCodec](https://github.com/brightfyregit/Friday-Night-Funkin-Mp4-Video-Support/projects/1).

## Table of Contents
- [Instructions](#instructions)  
- [Building](#building)  
- [Credits](#credits)  

## Instructions
**These are for Friday Night Funkin' mostly so it may not work for your HaxeFlixel project.**

### 1. Install the Haxelib:
[Install the Haxelib here](https://lib.haxe.org/p/hxCodec/).
You can also install it through git:
```cmd
haxelib git hxCodec https://github.com/polybiusproxy/hxCodec.git
```

### 2. Create a folder called `videos` in your `assets/preload` folder:

### 3. **OPTIONAL: If your PC is ARM64, add this code in `Project.xml`:**

```xml
<haxedef name="HXCPP_ARM64" />
```

### 3. Edit `Paths.hx`
```haxe
inline static public function video(key:String)
{
	return 'assets/videos/$key';
}
```

### 4. Playing videos

1. Put your video in the videos folder.
2. Create somewhere in PlayState:
```haxe
import vlc.VideoHandler;

var video:VideoHandler;

function playCutscene(name:String) //the format can be anything then is a video
{
	inCutscene = true;

	video = new VideoHandler();
	video.finishCallback = function()
	{
		startCountdown();
	}
	video.playVideo(Paths.video(name));
}

function playEndCutscene(name:String) //the format can be anything then is a video
{
	inCutscene = true;

	video = new VideoHandler();
	video.finishCallback = function()
	{
		SONG = Song.loadFromJson(storyPlaylist[0].toLowerCase());
		LoadingState.loadAndSwitchState(new PlayState());
	}
	video.playVideo(Paths.video(name));
}
```

### EXAMPLE (FOR FNF)
At the PlayState "create()" function:
```haxe
switch (curSong.toLowerCase())
{
	case 'song1':
		playCutscene('song1scene.mp4');
	case 'song2':
		playCutscene('song2scene.mp4');
	default:
		startCountdown();
}
```
**FOR KADE 1.8 USERS!!**
```haxe
generateSong(SONG.songId);

switch (curSong.toLowerCase())
{
	case 'bopeebo':
		playCutscene('gunsCutscene.mp4');
	default:
		startCountdown();
}

```

At the PlayState "endSong()" function:
```haxe
if (SONG.song.toLowerCase() == 'pingas')
	playEndCutscene('pingas.mp4');
```

**FOR KADE 1.8 USERS AGAIN**
```haxe
PlayState.SONG = Song.loadFromJson(PlayState.storyPlaylist[0], diff);
FlxG.sound.music.stop();

switch (curSong.toLowerCase())
{
	case 'deez':
		playEndCutscene('bigChungus.mp4');
	case 'nuts':
		playEndCutscene('bigChungus.mp4');
}
```

## BUILDING
### Windows
You don't need any special instructions in order to build for Windows.
Just pull the `lime build windows`.

### Linux
In order to make your game work with the library, every Linux user (this includes the player) **has to download** "libvlc-dev" and "libvlccore-dev" from your distro's package manager.
You can also install them through the terminal:
```bash
sudo apt-get install libvlc-dev
sudo apt-get install libvlccore-dev
```

### Android
Currently, hxCodec will search the videos only on the external storage (`/storage/emulated/0/appname/assets/videos/yourvideo.(whatever format it has)`), one more thing, you need to put the location manualy in paths.
This is not suitable for games and will be fixed soon.

## Credits

- [PolybiusProxy (me!)](https://github.com/polybiusproxy) - Creator of hxCodec.
- [datee](https://github.com/datee) - Creator of HaxeVLC.
- [Jigsaw](https://github.com/jigsaw-4277821) - Android Support
- [Erizur](https://github.com/Erizur) - Linux Support
- The contributors.
