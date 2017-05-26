# [UI] bottom sheet 코드

### 요구 조건
1. Android Support Library 23.2부터 사용 가능
2. android.support.design.widget.CoordinatorLayout 내에 포함되어야 함

### 사전 준비
1. app수준 gradle에 compile 'com.android.support:design:25.3.1'를 추가한다.

xml 파일

    <?xml version="1.0" encoding="utf-8"?>
    <android.support.design.widget.CoordinatorLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:id="@+id/layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@android:color/white">

        <LinearLayout
            android:id="@+id/bottomSheet"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            app:behavior_hideable="false"
            app:behavior_peekHeight="64dp"
            app:layout_behavior="@string/bottom_sheet_behavior">

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:padding="16dp"
                android:text="Bottom sheets"
                android:textColor="@color/colorPrimaryDark" />
                android:textAppearance="?android:attr/textAppearanceLarge"


            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:padding="16dp"
                android:text="표시할 제목"
                android:textAppearance="?android:attr/textAppearanceMedium" />


            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:padding="16dp"
                android:text="Bottom sheet에 담을 내용"
                android:textAppearance="?android:attr/textAppearanceSmall" />

        </LinearLayout>

        <android.support.design.widget.FloatingActionButton
            android:id="@+id/fab"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginEnd="16dp"
            android:layout_marginRight="16dp"
            android:src="@mipmap/ic_launcher"
            app:layout_anchor="@+id/bottomSheet"
            app:layout_anchorGravity="top|right" />

    </android.support.design.widget.CoordinatorLayout>

자바 파일

    public class MainActivity extends AppCompatActivity {

        boolean isClicked = false;

        private Button button;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            View layout = findViewById(R.id.layout);
            View mBottomSheet = findViewById(R.id.bottomSheet);
            final BottomSheetBehavior mBehavior = BottomSheetBehavior.from(mBottomSheet);

            mBehavior.setBottomSheetCallback(new BottomSheetBehavior.BottomSheetCallback() {
                @Override
                public void onStateChanged(@NonNull View bottomSheet, int newState) {
                }

                @Override
                public void onSlide(@NonNull View bottomSheet, float slideOffset) {
                    Log.i("TAG", "slideOffSet : " + String.valueOf(slideOffset));
                }
            });

            mBottomSheet.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    if (!isClicked) {
                        mBehavior.setState(BottomSheetBehavior.STATE_EXPANDED);
                        isClicked = true;
                    } else {
                        mBehavior.setState(BottomSheetBehavior.STATE_COLLAPSED);
                        isClicked = false;
                    }
                }
            });

            layout.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    if(mBehavior.getState() == BottomSheetBehavior.STATE_EXPANDED){
                        mBehavior.setState(BottomSheetBehavior.STATE_COLLAPSED);
                        isClicked = false;
                    }
                }
            });
        }
    }
