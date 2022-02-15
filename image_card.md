```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/white"
    tools:context=".Page_I">

    <RelativeLayout
        android:id="@+id/container_one"
        android:layout_marginTop="15dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <androidx.cardview.widget.CardView
            android:layout_width="match_parent"
            android:layout_height="60dp"
            android:layout_marginLeft="45dp"
            android:layout_marginTop="10dp"
            android:layout_marginRight="25dp"
            android:layout_marginBottom="10dp"
            app:cardBackgroundColor="@color/_awb_bg_card"
            app:cardCornerRadius="40dp"
            app:cardElevation="2dp">

            <LinearLayout
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:orientation="vertical">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginStart="50dp"
                    android:maxLines="2"
                    android:text="@string/_md"
                    android:textSize="16sp"
                    android:textStyle="bold" />

            </LinearLayout>

        </androidx.cardview.widget.CardView>

        <ImageView
            android:layout_width="50dp"
            android:layout_height="50dp"
            android:layout_centerVertical="true"
            android:layout_marginStart="25dp"
            android:elevation="2dp"
            android:src="@drawable/tgtdcl_logo" />

    </RelativeLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:orientation="horizontal"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/container_one">

        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1">

            <androidx.cardview.widget.CardView
                android:layout_width="match_parent"
                android:layout_height="60dp"
                android:layout_marginLeft="45dp"
                android:layout_marginTop="10dp"
                android:layout_marginRight="25dp"
                android:layout_marginBottom="10dp"
                app:cardBackgroundColor="@color/_awb_bg_card"
                app:cardCornerRadius="40dp"
                app:cardElevation="2dp">

                <LinearLayout
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center"
                    android:orientation="vertical">

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:layout_marginStart="50dp"
                        android:maxLines="2"
                        android:text="@string/_md"
                        android:textSize="16sp"
                        android:textStyle="bold" />

                </LinearLayout>

            </androidx.cardview.widget.CardView>

        </RelativeLayout>
        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1">

            <androidx.cardview.widget.CardView
                android:layout_width="match_parent"
                android:layout_height="60dp"
                android:layout_marginLeft="45dp"
                android:layout_marginTop="10dp"
                android:layout_marginRight="25dp"
                android:layout_marginBottom="10dp"
                app:cardBackgroundColor="@color/_awb_bg_card"
                app:cardCornerRadius="40dp"
                app:cardElevation="2dp">

                <LinearLayout
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center"
                    android:orientation="vertical">

                    <TextView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:layout_marginStart="50dp"
                        android:maxLines="2"
                        android:text="@string/_md"
                        android:textSize="16sp"
                        android:textStyle="bold" />

                </LinearLayout>

            </androidx.cardview.widget.CardView>

        </RelativeLayout>
    </LinearLayout>

</androidx.constraintlayout.widget.ConstraintLayout>
```
