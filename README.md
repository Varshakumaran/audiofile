# Ex.No:3 Develop a simple application to play and control the audio file in android studio.


## AIM:

To develop a simple application, to play and control the audio file and to perfrom the start,pause and stop opeartion in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as audiofile and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml and create start,pause and stop button.

Step 6: Display message give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to play and control the audio file”.
Developed by: VARSHA K
Registeration Number :212223220122
*/
```
## activity_main.xml:
```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Audio Player"
        android:textSize="28sp"
        android:textStyle="bold"
        android:layout_marginBottom="40dp" />

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/btnPlay"
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Play"
            android:layout_margin="8dp" />

        <Button
            android:id="@+id/btnPause"
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Pause"
            android:layout_margin="8dp" />

        <Button
            android:id="@+id/btnStop"
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Stop"
            android:layout_margin="8dp" />

    </LinearLayout>

</LinearLayout>
```
## MainActivity.java:
```
package com.example.audio;

import android.media.AudioManager;
import android.media.MediaPlayer;
import android.os.Bundle;
import android.util.Log;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private static final String TAG = "MainActivity";
    private MediaPlayer mediaPlayer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Ensure media volume is set to maximum on emulator/device
        AudioManager audioManager = (AudioManager) getSystemService(AUDIO_SERVICE);
        if (audioManager != null) {
            int maxVolume = audioManager.getStreamMaxVolume(AudioManager.STREAM_MUSIC);
            audioManager.setStreamVolume(AudioManager.STREAM_MUSIC, maxVolume, 0);
            Log.i(TAG, "Media volume set to max: " + maxVolume);
        }

        Button btnPlay = findViewById(R.id.btnPlay);
        Button btnPause = findViewById(R.id.btnPause);
        Button btnStop = findViewById(R.id.btnStop);

        // Create MediaPlayer and load the audio file from res/raw/audio.mpeg
        mediaPlayer = MediaPlayer.create(this, R.raw.audio);
        if (mediaPlayer == null) {
            Log.e(TAG, "MediaPlayer.create returned null! Check audio file format.");
        } else {
            Log.i(TAG, "MediaPlayer created successfully.");
            mediaPlayer.setVolume(1.0f, 1.0f);
            mediaPlayer.setOnErrorListener((mp, what, extra) -> {
                Log.e(TAG, "MediaPlayer error occurred: what=" + what + ", extra=" + extra);
                return true;
            });
            mediaPlayer.setOnCompletionListener(mp -> Log.i(TAG, "MediaPlayer playback completed."));
        }

        // Play Button
        btnPlay.setOnClickListener(v -> {
            Log.d(TAG, "Play clicked. mediaPlayer=" + mediaPlayer + ", isPlaying=" + (mediaPlayer != null ? mediaPlayer.isPlaying() : "null"));
            if (mediaPlayer != null) {
                if (!mediaPlayer.isPlaying()) {
                    try {
                        mediaPlayer.start();
                        Log.i(TAG, "mediaPlayer.start() called successfully. isPlaying=" + mediaPlayer.isPlaying());
                    } catch (Exception e) {
                        Log.e(TAG, "Exception calling mediaPlayer.start()", e);
                    }
                } else {
                    Log.w(TAG, "MediaPlayer is already playing.");
                }
            } else {
                Log.e(TAG, "MediaPlayer is null when Play is clicked!");
            }
        });

        // Pause Button
        btnPause.setOnClickListener(v -> {
            Log.d(TAG, "Pause clicked.");
            if (mediaPlayer != null && mediaPlayer.isPlaying()) {
                mediaPlayer.pause();
                Log.i(TAG, "mediaPlayer.pause() called.");
            }
        });

        // Stop Button
        btnStop.setOnClickListener(v -> {
            Log.d(TAG, "Stop clicked.");
            if (mediaPlayer != null) {
                mediaPlayer.pause();
                mediaPlayer.seekTo(0);
                Log.i(TAG, "mediaPlayer stopped (paused & reset to 0).");
            }
        });
    }

    // Release MediaPlayer when the app is destroyed
    @Override
    protected void onDestroy() {
        super.onDestroy();

        if (mediaPlayer != null) {
            mediaPlayer.release();
            mediaPlayer = null;
            Log.i(TAG, "MediaPlayer released in onDestroy.");
        }
    }
}

```

## OUTPUT:
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d2cd44bd-fd94-46dd-b070-326ca266f705" />





## RESULT
   Thus a simple application, to play and control the audio file and to perfrom the start,pause and stop opeartion in Android Studio is developed and executed successfully.
