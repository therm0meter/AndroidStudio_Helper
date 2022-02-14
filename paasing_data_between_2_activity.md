For the first activity java file..

1. outside of onCreate function

```
Button button1,button2;
```

2. inside of onCreate function

```
button1=(Button)findViewById(R.id.button1);
        button4 = (Button) findViewById(R.id.button4);

        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent=new Intent(MainActivity.this, userInfo.class);
                intent.putExtra("user_name",getResources().getString(R.string.test_name2));
                intent.putExtra("user_designation",getResources().getString(R.string.test_designation2));
                intent.putExtra("user_dept",getResources().getString(R.string.test_dept2));
                intent.putExtra("user_phone",getResources().getString(R.string.test_phone2));
                intent.putExtra("user_mail",getResources().getString(R.string.test_mail2));
                startActivity(intent);
            }
        });
```


For the target activity java file...

1. outside of onCreate function

```
TextView user_name, user_designation, user_dept, user_phone, user_mail;
ImageView user_pic;
```

2. inside of onCreate function

```
user_name=(TextView) findViewById(R.id.user_name);
        user_name.setText(getIntent().getStringExtra("user_name"));

        user_designation=(TextView) findViewById(R.id.user_designation);
        user_designation.setText(getIntent().getStringExtra("user_designation"));

        user_dept=(TextView) findViewById(R.id.user_dept);
        user_dept.setText(getIntent().getStringExtra("user_dept"));

        user_phone=(TextView) findViewById(R.id.user_phone);
        user_phone.setText(getIntent().getStringExtra("user_phone"));

        user_mail=(TextView) findViewById(R.id.user_mail);
        user_mail.setText(getIntent().getStringExtra("user_mail"));

        user_pic=(ImageView) findViewById(R.id.user_pic);

        //image_code
        if(user_name.getText().toString().equals(getResources().getString(R.string.test_name2)))
        {
            user_pic.setImageResource(R.drawable.baby);
        }
```
