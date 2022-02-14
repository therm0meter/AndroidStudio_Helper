add in activity java file...

1. outside of onCreate function
```
Button button1;
```

2. inside of onCreate function
```
button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent=new Intent(current_activity.this, target_activity.class);
                startActivity(intent);
            }
        });
```
