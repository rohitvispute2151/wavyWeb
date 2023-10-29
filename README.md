
	#1.	Toast
	
	activity_main.xml
	
		<?xml version="1.0" encoding="utf-8"?>
		<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
			xmlns:app="http://schemas.android.com/apk/res-auto"
			xmlns:tools="http://schemas.android.com/tools"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			tools:context=".MainActivity">

			<Button
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:id="@+id/showToast"
				android:text="whassup!!" />



		</androidx.constraintlayout.widget.ConstraintLayout>

	MainActivity.java
	
	package com.example.firstapp;

		import androidx.appcompat.app.AppCompatActivity;
		import android.os.Bundle;
		import android.view.View;
		import android.widget.Button;
		import android.widget.Toast;


		public  class MainActivity extends AppCompatActivity{
			@Override
			protected void onCreate(Bundle savedInstanceState){
				super.onCreate(savedInstanceState);
				setContentView(R.layout.activity_main);

				Button showToast = findViewById(R.id.showToast);
				showToast.setOnClickListener(new View.OnClickListener(){
					@Override
					public void onClick(View v){
						Toast.makeText(getApplicationContext(),"whassup!!",Toast.LENGTH_SHORT).show();
					}
				});
			}
		}
		
	--------------------------------
	
	#2. user authentication
	
	Creating a simple login screen in Android involves designing a user 
	interface and handling user input. Here's a step-by-step guide to create a 
	basic login screen with two text fields for login ID and password, and a login button. 
	We'll also display a success message with hardcoded login credentials.

		1. **Design the XML Layout:**

		   Create an XML layout file (e.g., `activity_login.xml`) for the login screen. Here's a basic example:

		   ```xml
		   <?xml version="1.0" encoding="utf-8"?>
		   <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
			   android:layout_width="match_parent"
			   android:layout_height="match_parent"
			   android:orientation="vertical"
			   android:padding="16dp">

			   <EditText
				   android:id="@+id/editTextLoginId"
				   android:layout_width="match_parent"
				   android:layout_height="wrap_content"
				   android:hint="Login ID"
				   android:inputType="text"
				   android:autofillHints="username"
				   android:layout_marginBottom="16dp" />

			   <EditText
				   android:id="@+id/editTextPassword"
				   android:layout_width="match_parent"
				   android:layout_height="wrap_content"
				   android:hint="Password"
				   android:inputType="textPassword"
				   android:autofillHints="password"
				   android:layout_marginBottom="16dp" />

			   <Button
				   android:layout_width="match_parent"
				   android:layout_height="wrap_content"
				   android:id="@+id/buttonLogin"
				   android:text="Login" />
		   </LinearLayout>
		   ```

		2. **Create the Java Code:**

		   In your Java class (e.g., `LoginActivity.java`), you can handle 
		   the login logic and display a message. Here's a basic example:

		   ```java
		   import android.os.Bundle;
		   import android.view.View;
		   import android.widget.Button;
		   import android.widget.EditText;
		   import android.widget.Toast;
		   import androidx.appcompat.app.AppCompatActivity;

		   public class LoginActivity extends AppCompatActivity {

			   @Override
			   protected void onCreate(Bundle savedInstanceState) {
				   super.onCreate(savedInstanceState);
				   setContentView(R.layout.activity_login);

				   // Initialize UI elements
				   EditText editTextLoginId = findViewById(R.id.editTextLoginId);
				   EditText editTextPassword = findViewById(R.id.editTextPassword);
				   Button buttonLogin = findViewById(R.id.buttonLogin);

				   // Hardcoded login credentials
				   final String hardcodedLoginId = "user123";
				   final String hardcodedPassword = "password123";

				   buttonLogin.setOnClickListener(new View.OnClickListener() {
					   @Override
					   public void onClick(View v) {
						   String loginId = editTextLoginId.getText().toString();
						   String password = editTextPassword.getText().toString();

						   if (loginId.equals(hardcodedLoginId) && password.equals(hardcodedPassword)) {
							   // Successful login
							   String successMessage = "Login successful. Welcome, " + loginId;
							   Toast.makeText(LoginActivity.this, successMessage, Toast.LENGTH_SHORT).show();
						   } else {
							   // Invalid credentials
							   Toast.makeText(LoginActivity.this, "Login failed. Please check your credentials.", Toast.LENGTH_SHORT).show();
						   }
					   }
				   });
			   }
		   }
		   ```

			3. **Add Activity to AndroidManifest.xml:**

			   Don't forget to add your `LoginActivity` to the `AndroidManifest.xml` file:

			   ```xml
			   <activity android:name=".LoginActivity">
				   <intent-filter>
					   <action android:name="android.intent.action.MAIN" />
					   <category android:name="android.intent.category.LAUNCHER" />
				   </intent-filter>
			   </activity>
			   ```

	----------------------------
	
	#3. Android Activity  LifeCycle
	
		Sure, here's a simple example of the Android activity lifecycle using a basic 
		Android Studio project. We'll create a single activity and override its lifecycle 
		methods to demonstrate their sequence.

		1. Open Android Studio and create a new Android Project with an Empty Activity template.

		2. In your `MainActivity.java` file, add the following code:

		```java
		import androidx.appcompat.app.AppCompatActivity;
		import android.os.Bundle;
		import android.util.Log;

		public class MainActivity extends AppCompatActivity {

			@Override
			protected void onCreate(Bundle savedInstanceState) {
				super.onCreate(savedInstanceState);
				setContentView(R.layout.activity_main);

				Log.d("Lifecycle", "onCreate called");
			}

			@Override
			protected void onStart() {
				super.onStart();
				Log.d("Lifecycle", "onStart called");
			}

			@Override
			protected void onResume() {
				super.onResume();
				Log.d("Lifecycle", "onResume called");
			}

			@Override
			protected void onPause() {
				super.onPause();
				Log.d("Lifecycle", "onPause called");
			}

			@Override
			protected void onStop() {
				super.onStop();
				Log.d("Lifecycle", "onStop called");
			}

			@Override
			protected void onDestroy() {
				super.onDestroy();
				Log.d("Lifecycle", "onDestroy called");
			}

			@Override
			protected void onRestart() {
				super.onRestart();
				Log.d("Lifecycle", "onRestart called");
			}
		}
		```

		In this code, we've added logging statements in each of the activity's lifecycle 
		methods to track their execution.

		3. Open your `activity_main.xml` layout file and add a simple layout 
		(e.g., a TextView) to display the activity:

		```xml
		<?xml version="1.0" encoding="utf-8"?>
		<RelativeLayout
			xmlns:android="http://schemas.android.com/apk/res/android"
			xmlns:app="http://schemas.android.com/apk/res-auto"
			xmlns:tools="http://schemas.android.com/tools"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			tools:context=".MainActivity">

			<TextView
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:text="Hello Activity Lifecycle"
				android:layout_centerInParent="true"
				android:textSize="24sp"/>
		</RelativeLayout>
		```

		4. Run the app on an emulator or a physical Android device.

		5. Observe the Logcat output in Android Studio to see the sequence of lifecycle 
		methods being called. You'll see messages indicating when each method is executed.

		For example, you might see a sequence like this:

		```
		onCreate called
		onStart called
		onResume called
		```

		This is the basic example of an Android activity's lifecycle. The sequence can vary 
		depending on the app's behavior, such as when you navigate away from the activity 
		and then return to it.
		
		-------------------------------------
		
		#4. Horizonatal scroll view
		
			<HorizontalScrollView
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:scrollbars="none">

			<LinearLayout
				android:id="@+id/imageContainer"
				android:layout_width="wrap_content"
				android:layout_height="wrap_content"
				android:orientation="horizontal">
				<!-- Add your image views here -->
				<ImageView
					android:layout_width="200dp"
					android:layout_height="200dp"
					android:src="@drawable/image1"
					android:scaleType="centerCrop"
					android:padding="8dp"/>

				<ImageView
					android:layout_width="200dp"
					android:layout_height="200dp"
					android:src="@drawable/image2"
					android:scaleType="centerCrop"
					android:padding="8dp"/>

				<!-- Add more images as needed -->
			</LinearLayout>
			</HorizontalScrollView>

	-----------------------------
	
	#5. Verticle Scrolling
	
	To implement vertical scrolling of images in Android Studio, you can use a `ScrollView` to contain an `ImageView`. Here are the steps to achieve this:

		1. Create an Android project or open your existing project in Android Studio.

		2. In your layout XML file (e.g., `activity_main.xml`), add a `ScrollView` that wraps an `ImageView`:

		```xml
				<ScrollView
					xmlns:android="http://schemas.android.com/apk/res/android"
					android:layout_width="match_parent"
					android:layout_height="match_parent">

					<ImageView
						android:id="@+id/scrollingImage"
						android:layout_width="match_parent"
						android:layout_height="wrap_content"
						android:src="@drawable/your_image" <!-- Replace with your image resource -->
						android:scaleType="fitCenter" <!-- Adjust the scale type as needed -->
						android:adjustViewBounds="true" />

				</ScrollView>
		```

		In this example, we've wrapped an `ImageView` with a `ScrollView`.
		The `ImageView` displays an image, and the `ScrollView` allows vertical scrolling.

		3. Replace `@drawable/your_image` with the resource reference of the 
		image you want to display.

		4. Adjust the `scaleType` and other attributes of the `ImageView` to 
		control how the image is displayed.

		5. To enable scrolling, ensure that the content of the `ImageView` is 
		taller than the screen's height. If the image is too large, you might 
		need to use a large image or set `android:layout_height` to a specific height.

		6. Run your Android app, and you'll see the image with vertical scrolling.

		With this setup, the user can scroll vertically to view the entire image 
		if it's larger than the screen's height.
		
		
		-----------------------------------
		
		#6. List View
		
		To create a `ListView` in Android Studio, you need to follow these steps:

			1. Open Android Studio and create a new Android project or open an existing project.

			2. Open the layout XML file where you want to add the `ListView`. 
			You can do this by navigating to the "res" folder, then the "layout" folder, 
			and opening the desired XML layout file (e.g., `activity_main.xml`).

			3. In the XML layout file, add the `ListView` widget. You can define it with an ID, 
			which you'll use to reference it in your Java/Kotlin code. Here's an example 
			of a `ListView` added to an XML layout:

			```xml
			<ListView
				android:id="@+id/listView"
				android:layout_width="match_parent"
				android:layout_height="match_parent"
			/>
			```

			4. Customize the layout of each item in the `ListView`. Typically, you'll 
			create a separate XML layout file for each item. For example, you can 
			create `list_item.xml` in the "layout" folder:

			```xml
			<!-- res/layout/list_item.xml -->
			<TextView
				xmlns:android="http://schemas.android.com/apk/res/android"
				android:id="@+id/textView"
				android:layout_width="match_parent"
				android:layout_height="wrap_content"
				android:textSize="18sp"
			/>
			```

			5. In your activity or fragment class (Java or Kotlin), you'll need to set 
			up the `ListView` and an adapter to populate the data. Here's a basic example in Java:

			```java
			import android.app.Activity;
			import android.os.Bundle;
			import android.widget.ArrayAdapter;
			import android.widget.ListView;

			public class MainActivity extends Activity {
				@Override
				protected void onCreate(Bundle savedInstanceState) {
					super.onCreate(savedInstanceState);
					setContentView(R.layout.activity_main);

					// Get a reference to the ListView
					ListView listView = findViewById(R.id.listView);

					// Sample data
					String[] items = {"Item 1", "Item 2", "Item 3", "Item 4"};

					// Create an adapter
					ArrayAdapter<String> adapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, items);

					// Set the adapter to the ListView
					listView.setAdapter(adapter);
				}
			}
			```

			And here's an example in Kotlin:



			Make sure to replace "Item 1," "Item 2," etc., with your actual data. 
			This is a basic example, and you can create custom adapters and layouts 
			for more complex scenarios.
			
		---------------------------
		
	#7. MultiScreen
		
		Creating a multi-screen Android app involves designing multiple activities 
		and navigating between them. Here are the basic steps to create a simple 
		multi-screen Android app in Android Studio:

		1. **Create a New Project:**
		   Open Android Studio and create a new Android project. You can choose an 
		   empty activity template to start with a single screen.

		2. **Create Additional Activities:**
		   To create multiple screens, you need to create additional activities. 
		   Right-click on the "app" folder, select "New," and then "Activity." Create 
		   a new activity for each screen you want to add. For example, you can 
		   create "SecondActivity" and "ThirdActivity."

		3. **Design Layouts:**
		   Design the layouts for each activity by editing the XML layout files. 
		   These XML files are located in the "res" folder, specifically in the "layout" 
		   folder. You can customize the UI for each screen using XML.

		4. **Define Buttons or UI Elements:**
		   In the layout XML for the first activity, add buttons or UI elements 
		   that will trigger navigation to other activities. For example, you can add 
		   buttons with `onClick` attributes that correspond to the actions to start other activities.

		   ```xml
		   <Button
			   android:id="@+id/buttonGoToSecond"
			   android:layout_width="wrap_content"
			   android:layout_height="wrap_content"
			   android:text="Go to Second Activity"
			   android:onClick="goToSecondActivity" />
		   ```

		5. **Handle Click Events:**
		   In the Java or Kotlin code for the first activity, create a method that 
		   handles the button click event and initiates navigation to the second activity. 
		   Use an `Intent` to start a new activity.

		   In Java:

		   ```java
		   public void goToSecondActivity(View view) {
			   Intent intent = new Intent(this, SecondActivity.class);
			   startActivity(intent);
		   }
		   ```

		   In Kotlin:

		   ```kotlin
		   fun goToSecondActivity(view: View) {
			   val intent = Intent(this, SecondActivity::class.java)
			   startActivity(intent)
		   }
		   ```

		6. **Repeat for Other Activities:**
		   Repeat the steps for the second activity to navigate to the third activity 
		   or any other screens. You can use different buttons or UI elements to trigger 
		   navigation to various activities.

		7. **Manifest File:**
		   Don't forget to declare all your activities in the AndroidManifest.xml file. 
		   Add `<activity>` elements for each activity to specify their entry points.

		   ```xml
		   <activity android:name=".SecondActivity">
			   <!-- Intent filters -->
		   </activity>

		   <activity android:name=".ThirdActivity">
			   <!-- Intent filters -->
		   </activity>
		   ```

		8. **Run the App:**
		   Run the app on an emulator or a physical Android device. You should be able 
		   to navigate between the screens by clicking buttons or UI elements that trigger the intended actions.

		This is a basic example of creating a multi-screen Android app. For more complex apps, 
		you may need to pass data between activities or use other navigation components like the Navigation Component.
