
# Rapport
Veckans uppgift handlade om att arbeta med Shared Preferences för att spara data emellean aktiviteter och emellan app start.

## MainActivity


```java
public class MainActivity extends AppCompatActivity {

    private SharedPreferences myPreferenceRef;
    private SharedPreferences.Editor myPreferenceEditor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        myPreferenceRef = getSharedPreferences("MyPreferenceName", MODE_PRIVATE);
        myPreferenceEditor = myPreferenceRef.edit();
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

        TextView prefTextRef=new TextView(this);
        prefTextRef=(TextView)findViewById(R.id.prefText);
        prefTextRef.setText(myPreferenceRef.getString("MyAppPreferenceString", "No preference found."));
    }

    public void onButtonClickIntent(View button){
        Intent intent = new Intent(MainActivity.this, SecondActivity.class);
        startActivity(intent);
    }
}
```
![](Screen%201.jpg)
## SecondActivity

```java
public class SecondActivity extends AppCompatActivity {

    private SharedPreferences myPreferenceRef;
    private SharedPreferences.Editor myPreferenceEditor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        myPreferenceRef = getSharedPreferences("MyPreferenceName", MODE_PRIVATE);
        myPreferenceEditor = myPreferenceRef.edit();
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);
    }

    public void savePref(View v){
        // Get the text
        EditText newPrefText=new EditText(this);
        newPrefText=(EditText)findViewById(R.id.settingseditview);

        // Store the new preference
        myPreferenceEditor.putString("MyAppPreferenceString", newPrefText.getText().toString());
        myPreferenceEditor.apply();

        // Clear the EditText
        newPrefText.setText("");

        Intent intent = new Intent(SecondActivity.this, MainActivity.class);
        startActivity(intent);
    }
}

```
![](Screen%202.jpg)

