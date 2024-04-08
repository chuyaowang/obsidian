# Premiere Pro

## Dehaze

- [Reference](https://www.youtube.com/watch?v=W2oSBypQegU)
- Adjust colors
- Duplicate clip to track above
- Apply invert and black & white
- Set blend mode to subtract
- Lower substract amount
- Adjust colors of the two clips
- Nest them and adjust colors again

## Normalize Volume

- Right click on audio clip, audio gain, look at the peak volume, use it for a reference
	- If the peak volume (max volume) does not represent most of the peaks, also note average amplitude
- Select normalize all peaks to 0 db
	- This brings the tallest peak to 0 db and add the same amount to the other peaks
	- Set gain to 0: no change made to the gain, the peak retains its original amplitude
- Use the dynamics effect to make further adjustments
	- Compressor: increases volume of parts below the *threshold* in an amount defined by *makeup*
		- This should be used to bring parts with lower than average volume to the average volume, -3 db is a good point
		- However, if it is the same song, speech, etc., take care not to make a part that is intended to be quiet louder than it should be
	- Limiter: the highest volume cannot go above the *limit*; adding the limiter muffles the sound
		- Personally I don't use it
- Increasing volume amplifies noise as well
- Volume clips at 0 db

[max peaks vs. all peaks](https://community.adobe.com/t5/premiere-pro-discussions/normalize-audio-max-peak-vs-all-peaks/m-p/14091548)

- Adjusting the volume line directly on the timeline for quick and simple volume changes.
- Using the Audio Gain function for precise dB adjustments.
- Employing the Audio Clip Mixer for volume control.
- Utilizing keyframes for creating dynamic volume changes over time, such as fade-in and fade-out effects.
- Shortcut for gain control: **G**

## Shortcuts

- To next keyframe: drag while holding shift
