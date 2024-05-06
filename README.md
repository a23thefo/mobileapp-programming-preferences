
# Rapport
Veckans uppgift handlade om att arbeta med Shared Preferences för att spara data emellean aktiviteter och emellan app start.

## MainActivity
I ***MainActivity:s*** *onCreate()* hämtas en *SharedPreference* vid namn *"MyPreferenceName"*(Jätte kreativ tack jag vet.) som är satt som *MODE_PRIVATE*
detta är för att denna preferens enbart ska kunna hämtas av denna application. Om preferencen *"MyPreferenceName"* finns skappas den. --

Sedan finns det en text view som hämtar strängen med namn *"MyAppPreferenceString"* ifrån den delade preferensen och lägger den som sin text. Om strängen vid det namnet
inte finns så skrivs *"No preference found."* ut. 


Det finns också en knapp med en enkel intent som tar dig till nästa activity.

```java
public class MainActivity extends AppCompatActivity {

    private SharedPreferences myPreferenceRef;
    private SharedPreferences.Editor myPreferenceEditor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        myPreferenceRef = getSharedPreferences("MyPreferenceName", MODE_PRIVATE);
        ...
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
I ***SecondActivity*** hämtas *"MyPreferenceName"* igen men den här gången defineras en editor också. Det den här editorn gör är att när den blir kallad
med en *.putString()* efter sig kan en sträng läggas in i själva preferens objektet där det första värdet man skriver in är namnet på strängen och det andra är själva värdet. --

Efter man har gjort det behövs en *.apply()* med editor objektet framför sig också vilket enbart tillämpar ändringarna som objektet har undergått till där den sparas på mobilen.
```java
public class SecondActivity extends AppCompatActivity {

    private SharedPreferences myPreferenceRef;
    private SharedPreferences.Editor myPreferenceEditor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        myPreferenceRef = getSharedPreferences("MyPreferenceName", MODE_PRIVATE);
        myPreferenceEditor = myPreferenceRef.edit();
        ...
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

