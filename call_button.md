1. add this in manifest file

```
<uses-permission android:name="android.permission.CALL_PHONE"/>
```

2. add this in java file

```
findViewById(R.id.the_button_name).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                dialContactPhone(getIntent().getStringExtra("user_phone"));
            }
        });
    }
    private void dialContactPhone(final String phoneNumber) {
        startActivity(new Intent(Intent.ACTION_DIAL, Uri.fromParts("tel", phoneNumber, null)));
    }
```
