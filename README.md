Assignment 6 Rapport.


Det första som skulle göras i uppgiften var att skapa shared preferences i MainActivity som kan läsa data.
Detta gjordes genom att lägga till koden:
textViewName = findViewById(R.id.name) används för att hitta den textView widgeten som ska användas.
Sedan i onResume så skrivs koden som ska kunna läsa datan som skickas.
Först så hämtas textsträngen getString och sedan så sätts den hämtade texten i textViewName med koden setText.

```
onCreate {
    textViewName = findViewById(R.id.name);
    ...
}

onResume {
    String name = preferences.getString("name", "inget namn hittades");
    textViewName.setText(name);

    super.onResume();
}

```


Efter detta så skapades en ny aktivitet (SecondActivity), och varsin button till layouten i activity_main samt activity_second.
Det lades sedan till kod så att button widgeten ska vid onClick byta mellan aktiviteterna.
Först används findViewById för att hitta button widgeten som ska gälla.
Sedan sätts en onClick på button, där den button som är i MainActivity byter sida till SecondActivity och tvärtom.
Koden till detta ser ut såhär:

```
MainActivity:
    Button b = findViewById(R.id.button);
    b.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent(MainActivity.this, SecondActivity.class);
            startActivity(intent);
        }
    });

SecondActivity:
    Button b = findViewById(R.id.button2);
    b.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent(SecondActivity.this, MainActivity.class);
            startActivity(intent);
        }
    });

```

I SecondActivity skrivs Shared Preferences kod som ska kunna skicka data.
Först läggs SharedPreferences in och detta är objektet som håller våra preferences.
Seadan läggs SharedPreferences.Editor till, och denna kod låter oss att göra ändringar/uppdateringar i datan.
I putString skrivs den data som ska lagras.
Och sist editor.apply(); lagrar datan.

```

SecondActivity:
onCreate {
    preferences = getSharedPreferences("preferences", MODE_PRIVATE);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putString("name", "Wilmer");
    editor.apply();
    ...

}

```



