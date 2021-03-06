### Activity lifecycle

---

### Activity & lifecycle

- Activity:
    - Using Intents.
    - Multiple Activity.
- Activity Lifecycle:
    - Understand the Activity Lifecycle.
    - Multiple states.
    - When to use what.
- Activity Instance state
    - Save & Retrieve instance/UI state.
---

### Activity

- An activity represents a single screen in your app with an interface the user can interact with.
- Create Activity in Android Studio: RMB -> New -> Activity.
- XML layout file.

<img width="350" src="/media/android-dev-images/android-dev-7/android-dev-activity.gif" alt="Activity gif">

---

### Activity Example

- ```Java
    public class MainActivity extends AppCompatActivity {
        //All declarations should be here ..

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            //All initialization should be here ..
        }

        //Other Functions ..
    }
    ```

---

### Multiple Activity

- Start a new activity using Intent.
- Intent: messaging object you can use to request an action from another app component.
- ```Java
    //New intent
    Intent myIntent = new Intent(this, LoginActivity.class);

    //Start a new activity
    startActivity(myIntent);
    ```
- <img width="550" src="/media/android-dev-images/android-dev-7/android-dev-intent.png" alt="Intent">

---

### Activity lifecycle

<img width="550" src="/media/android-dev-images/android-dev-7/android-dev-activity-lifecycle.png" alt="Activity lifecycle">

---

### onCreate()

- Called when the activity is first created.
- Normal static set up: create views, bind data to lists, etc.
- Always followed by onStart().

---

### onStart()

- Called when the activity is becoming visible to the user.
- Followed by onResume() if the activity comes to the foreground.

---
### onResume()

- Called when the activity will start interacting with the user.
- Always followed by onPause().
    - if user clicked Home button.
    - fragment on top.
    - dialog on top.

---

### onPause()

- Called as part of the activity lifecycle when an activity is going into the background, but has not been killed yet.
- Going from Activity A to Activity B, Activity A will be paused until called again.
- Activity B will not be called until Activity A is paused, don't put anything that will take time here.

---

### onStop()

- Called when you are no longer visible to the user. You will next receive either onRestart(), onDestroy() depending on later user activity.

### onDestroy()

- The final call you receive before your activity is destroyed.
- Called when the app is closed & on device orientation.

---

### Multiple states

- All three called when the activity start running:
- onCreate() -> onStart() ->onResume().
- <img width="150" src="/media/android-dev-images/android-dev-7/android-dev-lifecycle1.gif" alt="lifecycle 1">

- When back button is presed:
- onPaused() - > onStop() -> onDestory().

- When home button pressed:
- onPaused() -> onStop().

---

### Demo: Activity-Lifecycle in the code example folder.

<img width="550" src="/media/android-dev-images/android-dev-7/android-dev-activity-lifecycle.png" alt="Activity lifecycle">

---

### Saving UI state

- onDestory method will remove state date from the activity, called when the app is closed & on device rotation.
- Save UI state using savedInstanceState.
- <img width="550" src="/media/android-dev-images/android-dev-7/android-dev-uistate.gif" alt="UI State">

---

### Saving UI state

- ```Java
    @Override
    protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        //Save what you want:
        //Example, Save the name.
        outState.putString("name", name);
    }
    ```
- Bundle are used by activities to pass data to themselves in the future.
- putString(key,value), putChar, putInt ... etc.
- Exist on onCreate function in every Activity:
- ```Java
    @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            //All initialization should be here ..
        }
    ````

--- 

### Retrieve saved UI state

- ```Java
    public class MainActivity extends AppCompatActivity {
            //All declarations should be here ..
            String name;
            @Override
            protected void onCreate(Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.activity_main);

                //Check if savedInstanceState is not null
                if(savedInstanceState != null){
                    //Get the saved name
                    name = savedInstanceState.getString("name");
                }
            }
        }
    ```
- Check for null.
- Get Saved states using savedInstanceState.getString(key), getChar, getInt ..etc.

---

### Retrieve saved UI state alternative way

- ```Java
    @Override
        protected void onRestoreInstanceState(@NonNull Bundle savedInstanceState) {
            super.onRestoreInstanceState(savedInstanceState);
            //Get the saved name
            name = savedInstanceState.getString("name");
        }
    ````
- Override onRestoreInstanceState method.
- No need to check for null.
- Check Saved-instance-state in code examples folder. 

---

### Questions ..