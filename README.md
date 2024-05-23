# Save-data
save user input data on user interface
public class MainActivity extends AppCompatActivity {
    private EditText editText1, editText2, editText3, displayEditText;
    private Button saveButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText1 = findViewById(R.id.editText1);
        editText2 = findViewById(R.id.editText2);
        editText3 = findViewById(R.id.editText3);
        displayEditText = findViewById(R.id.displayEditText);
        saveButton = findViewById(R.id.saveButton);

        saveButton.setOnClickListener(new View.OnClickListener() {

            @Override
            public void onClick(View view) {
                saveUserData();
            }
        });

        loadUserData(); // Load saved data on app start
    }

    private void saveUserData() {
        SharedPreferences preferences = getSharedPreferences("UserData", MODE_PRIVATE);
        SharedPreferences.Editor editor = preferences.edit();

        editor.putString("key_user_data_1", editText1.getText().toString());
        editor.putString("key_user_data_2", editText2.getText().toString());
        editor.putString("key_user_data_3", editText3.getText().toString());
        editor.apply();
        // Update the display with the saved data
        loadUserData();
    }
    private void loadUserData() {
        SharedPreferences preferences = getSharedPreferences("UserData", MODE_PRIVATE);

        String savedData1 = preferences.getString("key_user_data_1", "");
        String savedData2 = preferences.getString("key_user_data_2", "");
        String savedData3 = preferences.getString("key_user_data_3", "");

        displayEditText.setText("Telegram-API : " + savedData1 + "\nToken : " + savedData2 + "\nUser-ID : " + savedData3);

    }
}
