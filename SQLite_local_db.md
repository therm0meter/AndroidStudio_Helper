> DBHelper.java

```
import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

public class DBHelper extends SQLiteOpenHelper {

    private static final String dbName = "appDatabase.db";
    private static final int dbVersion = 18;
    private Context context;

    public DBHelper(Context content) {
        super(content, dbName, null, dbVersion);
        this.context = content;

        this.db_refresh();
        this.db_copy();

    }

    // --- refresh the db file ---
    public void db_refresh() {
        String appDbPath = this.context.getDatabasePath(dbName).getAbsolutePath();
        File dbFile = new File(appDbPath);
        dbFile.delete();
    }

    // --- copy the db file
    private void db_copy() {
        // Ensure /data/data/YOUR_PACKAGE_NAME/databases/ directory is created.
        File dbDir = new File(context.getDatabasePath(dbName).getParentFile().getPath());
        if (!dbDir.exists())
            dbDir.mkdir();

        // Copy database starts here.
        String appDbPath = this.context.getDatabasePath(dbName).getAbsolutePath();
        File dbFile = new File(appDbPath);
        if (!dbFile.exists()) {
            try {
                InputStream mInput = context.getAssets().open("main_db.db");
                OutputStream mOutput = new FileOutputStream(appDbPath);
                byte[] mBuffer = new byte[1024];
                int mLength;
                while ((mLength = mInput.read(mBuffer, 0, 1024)) > 0)
                    mOutput.write(mBuffer, 0, mLength);
                mOutput.flush();

                mOutput.close();
                mInput.close();
            } catch (IOException ex) {
                throw new Error("Error copying database: " + ex.getMessage());
            }
        }
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        // -- nothing
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db_refresh();
        db_copy();
    }
}
```

> 1

```
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.database.Cursor;
import android.database.SQLException;
import android.database.sqlite.SQLiteDatabase;
import android.graphics.Color;
import android.net.Uri;
import android.os.Build;
import android.os.Bundle;
import android.text.Html;
import android.text.util.Linkify;
import android.view.View;
import android.widget.LinearLayout;
import android.widget.TextView;

import com.google.android.material.card.MaterialCardView;

public class md extends AppCompatActivity {

    TextView name, designation;
    MaterialCardView call, msg;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.md);

        name = this.findViewById(R.id.name);
        name.setText(getIntent().getStringExtra("name"));

        designation = this.findViewById(R.id.designation);
        designation.setText(getIntent().getStringExtra("designation"));

        call = this.findViewById(R.id.call);
        msg = this.findViewById(R.id.msg);

        String number = getIntent().getStringExtra("phone");

        call.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                dialContactPhone(number);
            }
        });

        msg.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                // TODO Auto-generated method stub

                String smsText = "Hello";

                Uri uri = Uri.parse("smsto:" + number);
                Intent intent = new Intent(Intent.ACTION_SENDTO, uri);
                intent.putExtra("sms_body", smsText);
                startActivity(intent);
            }
        });

        LinearLayout db1 = this.findViewById(R.id.db1);
        LinearLayout db2 = this.findViewById(R.id.db2);
        TextView db1_header,db2_header;

        // Fetch data and display.
        DBHelper dbHelper = new DBHelper(this);
        SQLiteDatabase db;
        try {
            db = dbHelper.getWritableDatabase();
        } catch (SQLException mSQLException) {
            throw mSQLException;
        }

        //passed data from main_activity
        db1_header = this.findViewById(R.id.db1_header);
        db1_header.setText(getIntent().getStringExtra("db1_header"));
        db2_header = this.findViewById(R.id.db2_header);
        db2_header.setText(getIntent().getStringExtra("db2_header"));

        Cursor cursor = db.rawQuery("SELECT name,designation,phone FROM md_office;", null);
        while (cursor.moveToNext()) {
            int i = 0;
            final String name = cursor.getString(i++);
            final String designation = cursor.getString(i++);
            final String phone = cursor.getString(i++);

            TextView textView = new TextView(this);
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
                textView.setText(Html.fromHtml("<h5>" + name + "</h5>" + designation + "<br>" + phone, Html.FROM_HTML_MODE_COMPACT));
            } else {
                textView.setText(Html.fromHtml("<h5>" + name + "</h5>" + designation + "<br>" + phone));
            }
            textView.setTextAppearance(R.style.dbText);
            textView.setPadding(50, 20, 0, 20);
            textView.setBackgroundResource(R.drawable._card_child2);
            Linkify.addLinks(textView, Linkify.ALL);
            textView.setLinkTextColor(Color.parseColor("#FF373737"));
            db1.addView(textView);
        }
        cursor.close();

        Cursor cursor2 = db.rawQuery("SELECT name,designation,phone FROM biniyog_unnoyon;", null);
        while (cursor2.moveToNext()) {
            int i = 0;
            final String name = cursor2.getString(i++);
            final String designation = cursor2.getString(i++);
            final String phone = cursor2.getString(i++);

            TextView textView2 = new TextView(this);
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
                textView2.setText(Html.fromHtml("<h5>" + name + "</h5>" + designation + "<br>" + phone, Html.FROM_HTML_MODE_COMPACT));
            } else {
                textView2.setText(Html.fromHtml("<h5>" + name + "</h5>" + designation + "<br>" + phone));
            }
            textView2.setTextAppearance(R.style.dbText);
            textView2.setPadding(50, 20, 0, 20);
            textView2.setBackgroundResource(R.drawable._card_child2);
            Linkify.addLinks(textView2, Linkify.ALL);
            textView2.setLinkTextColor(Color.parseColor("#FF373737"));
            db2.addView(textView2);
        }
        cursor.close();
    }

    private void dialContactPhone(final String phoneNumber) {
        startActivity(new Intent(Intent.ACTION_DIAL, Uri.fromParts("tel", phoneNumber, null)));
    }
}
```

> 2

```
package com.therm0meter.titasgas;

import androidx.appcompat.app.AppCompatActivity;

import android.database.Cursor;
import android.database.SQLException;
import android.database.sqlite.SQLiteDatabase;
import android.os.Build;
import android.os.Bundle;
import android.text.Html;
import android.widget.LinearLayout;
import android.widget.TextView;

public class DB2 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_db2);

        LinearLayout linearLayout = this.findViewById(R.id.main_linearlayout_view);
        TextView db2_header;

        // Fetch data and display.
        DBHelper dbHelper = new DBHelper(this);
        SQLiteDatabase db;

        try {
            db = dbHelper.getWritableDatabase();
        } catch (SQLException mSQLException) {
            throw mSQLException;
        }

        //passed data from main_activity
        String table = getIntent().getStringExtra("table");
        db2_header=(TextView) findViewById(R.id.db2_header);
        db2_header.setText(getIntent().getStringExtra("header"));

        if(table.equals("table"))
        {
            Cursor cursor = db.rawQuery("SELECT name,designation,phone FROM dmr;", null);
            while(cursor.moveToNext())
            {
                int i=0;
                final String name = cursor.getString(i++);
                final String designation = cursor.getString(i++);
                final String phone = cursor.getString(i++);

                TextView textView = new TextView(this);
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
                    textView.setText(Html.fromHtml("<h5>"+ name +"</h5>"+ designation +"<br>"+ phone, Html.FROM_HTML_MODE_COMPACT));
                } else {
                    textView.setText(Html.fromHtml("<h5>"+ name +"</h5>"+ designation +"<br>"+ phone));
                }
                textView.setTextAppearance(R.style.dbText);
                textView.setPadding(20,10,0,10);
                textView.setBackgroundResource(R.drawable._card_child2);
                linearLayout.addView(textView);
            }
            cursor.close();
        }
        else if (table.equals("table2"))
        {
            Cursor cursor = db.rawQuery("SELECT name,designation,phone FROM nganj;", null);
            while(cursor.moveToNext())
            {
                int i=0;
                final String name = cursor.getString(i++);
                final String designation = cursor.getString(i++);
                final String phone = cursor.getString(i++);

                TextView textView = new TextView(this);
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
                    textView.setText(Html.fromHtml("<h5>"+ name +"</h5>"+ designation +"<br>"+ phone, Html.FROM_HTML_MODE_COMPACT));
                } else {
                    textView.setText(Html.fromHtml("<h5>"+ name +"</h5>"+ designation +"<br>"+ phone));
                }
                textView.setTextAppearance(R.style.dbText);
                textView.setPadding(20,10,0,10);
                textView.setBackgroundResource(R.drawable._card_child2);
                linearLayout.addView(textView);
            }
            cursor.close();
        }
    }
}
```
