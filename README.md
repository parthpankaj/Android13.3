# Android13.3
package com.example.pankaj.context133;

import java.io.IOException;
import java.util.Timer;
import java.util.TimerTask;
import android.media.MediaPlayer;
import android.os.Bundle;
import android.os.Handler;
import android.preference.PreferenceManager;
import android.app.Activity;
import android.content.SharedPreferences;
import android.view.Menu;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.SeekBar;
import android.widget.TextView;
import android.widget.SeekBar;
import android.widget.SeekBar.OnSeekBarChangeListener;
import android.widget.Toast;
public class MainActivity extends Activity   implements OnSeekBarChangeListener  {

    MediaPlayer OurSong;

    public  Handler handler1 = new Handler();
    Button Start;
    Button Stop;
    Button Button21;
    Button Button22;

    Button StopButton;
    public int GProgreess=0;
    int Rc=0;
    int BitCount=6;
    int SeekPos=0;
    int Period=500;


    int BreakVar=0;
    Thread myThread ;
    public TextView text1,text2,text3,text4;
    private SeekBar bar;
    private TextView textProgress,textAction;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toast.makeText(this, "onCreate()", Toast.LENGTH_LONG).show();

        Button21=(Button)findViewById(R.id.button);
        Button22=(Button)findViewById(R.id.button2);

        StopButton=(Button)findViewById(R.id.button2);
        bar = (SeekBar)findViewById(R.id.seekBar1);
        textProgress = (TextView)findViewById(R.id.textViewProgress);
        OurSong=MediaPlayer.create(MainActivity.this,R.raw.a);
        try {
            OurSong.prepare();
        } catch (IllegalStateException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        bar.setOnSeekBarChangeListener(this); // set seekbar listener.
        /*handler1.post(runnable1);
        stopPlaying();*/


        StopButton.setOnClickListener(new View.OnClickListener() {

            public void onClick(View v)
            {


                stopPlaying();

                BitCount=5;
                handler1.removeCallbacks(runnable1);



            }/****End of on clk******/

        });/*****End of set on clk listener*****/

        Button21.setOnClickListener(new View.OnClickListener() {

            public void onClick(View v)
            {

                stopPlaying();
                Rc=0;
                BitCount=13;

                handler1.removeCallbacks(runnable1);

                handler1.post(runnable1);

            }/****End of on clk******/

        });/*****End of set on clk listener*****/
        Button22.setOnClickListener(new View.OnClickListener() {

            public void onClick(View v)
            {



                stopPlaying();

                Rc=0;
                BitCount=15;

                handler1.removeCallbacks(runnable1);

                handler1.post(runnable1);


            }/****End of on clk******/

        });/*****End of set on clk listener*****/

    }

    @Override
    protected void onStart() {
        //the activity is become visible.
        super.onStart();
    /*handler1.removeCallbacks(runnable1);*/

    }
    @Override
    protected void onPause() {
        super.onPause();


    }
    @Override
    protected void onResume() {

        super.onResume();



    }
    @Override
    protected void onStop() {
        //the activity is no longer visible.
        super.onStop();
        Toast.makeText(this, "onStop()", Toast.LENGTH_LONG).show();
    }
    @Override
    protected void onDestroy() {
        //The activity about to be destroyed.
        super.onDestroy();
        Toast.makeText(this, "onDestroy()", Toast.LENGTH_LONG).show();
    }



    private void stopPlaying()
    {
        if (OurSong != null)
        {
            OurSong.stop();
            OurSong.release();
            OurSong = null;
        }
    }

/* private void stopPlaying() 
     {

                OurSong.stop();
                OurSong.release();



        }*/



    public Runnable runnable1= new Runnable() {
        @Override
        public void run() {
            if(BitCount==13)
            {
                text1.setText("1");
                text2.setText(""+Rc);
                text3.setText(""+BitCount);
                if(Rc==0||Rc==6||Rc==10)
                {

                    stopPlaying();
                    OurSong=MediaPlayer.create(MainActivity.this,R.raw.a);
                    OurSong.start();



                }


                if(Rc==2||Rc==4||Rc==8||Rc==12)
                {
                    stopPlaying();
                    OurSong=MediaPlayer.create(MainActivity.this,R.raw.b);
                    OurSong.start();


                }
                if(Rc==13)
                {
                    stopPlaying();
                    OurSong=MediaPlayer.create(MainActivity.this,R.raw.c);
                    OurSong.start();

                }

                Rc++;
                if(Rc>BitCount)
                {
                    text4.setText(""+Rc);
                    Rc=0;
                }

            }/****End of bitcount=13****/
            if(BitCount==15)
            {
                text1.setText("2");
                text2.setText(""+Rc);
                text3.setText(""+BitCount);
                if(Rc==0||Rc==8||Rc==12)
                {
                    stopPlaying();
                    OurSong=MediaPlayer.create(MainActivity.this,R.raw.a);
                    OurSong.start();


                }


                if(Rc==2||Rc==4||Rc==6||Rc==10||Rc==14)
                {
                    stopPlaying();
                    OurSong=MediaPlayer.create(MainActivity.this,R.raw.b);
                    OurSong.start();

                        /* Toast.makeText(getApplicationContext(), "-",
                      Toast.LENGTH_LONG).show();*/

                }
                if(Rc==15)
                {
                    stopPlaying();
                    OurSong=MediaPlayer.create(MainActivity.this,R.raw.c);
                    OurSong.start();

                        /*Toast.makeText(getApplicationContext(), "|",
                      Toast.LENGTH_LONG).show();*/

                }

                Rc++;
                if(Rc>BitCount)
                {
                    text4.setText(""+Rc);
                    Rc=0;
                }
            }/***End of bitcount=15***/




            if(BitCount==5)
            {
                text1.setText("Rc"+Rc);
                stopPlaying();
            }
            if(BitCount==6)
            {
                text1.setText("x"+Rc);
                stopPlaying();
            }

            handler1.postDelayed(runnable1, Period);

        }
    };
    public void onProgressChanged(SeekBar seekBar, int progress,
                                  boolean fromUser) {

        GProgreess=progress+20;

        textProgress.setText("Bit/Minute: "+(progress+20));

    }

    @Override
    public void onStartTrackingTouch(SeekBar seekBar) {


    }

    @Override
    public void onStopTrackingTouch(SeekBar seekBar) {

        seekBar.setSecondaryProgress(seekBar.getProgress());
        SeekPos=GProgreess;
        Period=(int)(30000/SeekPos);    
        /*textProgress.setText("Period: "+Period);*/
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.main, menu);

        return true;
    }

}
------
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.pankaj.context133.MainActivity">

    <Button
        android:text="Play"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_alignParentStart="true"
        android:layout_marginStart="11dp"
        android:layout_marginBottom="97dp"
        android:id="@+id/button" />

    <Button
        android:text="Stop"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignBottom="@+id/button"
        android:layout_alignParentEnd="true"
        android:layout_marginEnd="12dp"
        android:id="@+id/button2" />
</RelativeLayout>
