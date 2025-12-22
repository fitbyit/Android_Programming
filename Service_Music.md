```
<uses-permission android:name="android.permission.FOREGROUND_SERVICE"/>
```

```
Button btn;
boolean isplaying = false;
MediaPlayer mp;
```

```java
btn = findViewById(R.id.btnGreet);
mp = MediaPlayer.create(this, R.raw.ring);
mp.setLooping(true);
btn.setOnClickListener(new View.OnClickListener() {
  @Override
  public void onClick(View v) {
    if (!isplaying){
      btn.setText("Stop");
      mp.start();
      isplaying = true;
    } else {
       btn.setText("Play");
       mp.pause();
       isplaying = false;
      }
}
});
```

```
@Override
    protected void onDestroy() {
        super.onDestroy();
        if (mp != null) {
            mp.release();
            mp = null;
        }
    }
```
