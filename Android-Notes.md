# Android Notes
## Lec02: Layout
add widget to layout <br />
set individual properties <br />

write kotlin functions<br />
widget property -> onClick link to Function<br />

```kotlin

class MainActivity: AppCompatActivity(){
   private var points=0
   
   override fun onCreate(savedInstanceState:Bundle?){
      super.onCreate(savedInstanceState)
      setContentView(R.layout.activity_main)
      pickRandomNumbers()
   }
   
   fun leftButtonClick(view:View){
      val leftButton=findViewByID<Button>(R.id.left_Button)
      val rightButton=findViewByID<Button>(R.id.right_Button)
      val leftNum: Int= leftButton.text.toString().toInt
      val rightNum: Int= rightButton.text.toString().toInt
      if (leftNum > rightNum){
         //you win!
         points++
      } else {
         //you lose!
         points--
      }
      findViewById<TextView>(R.id.points).text="Points: $points"
    }
    
    // Good Practice, make val when possible. ( val are similar to Constants)
    fun pickRandomNumbers(){
       val leftButton =findViewById<Button>(R.id.left_button)
       val rightButton =findViewById<Button>(R.id.right_button)
       val r =Random()
       val num1 =r.nextInt(bound:10)
       var num2 =num1
       while (num1==num2){
          num2=r.nextInt(bound:10)
       }
       
       leftButton.text="$num1"
       rightButton.text="$num2"
    }
}

```

A different way function call by both left right button to share code
```kotlin
fun leftButtonClick{
   checkIfCorrectAnswer(true)
}

fun rightButtonClick{
   checkIfCorrectAnswer(false)
}

fun checkIfCorrectAnswer(isLeft: Boolean){
   val leftButton=findViewByID<Button>(R.id.left_Button)
   val rightButton=findViewByID<Button>(R.id.right_Button)
   val leftNum: Int= leftButton.text.toString().toInt
   val rightNum: Int= rightButton.text.toString().toInt
   if (leftNum > rightNum){
      //you win!
      points++
   } else {
      //you lose!
      points--
   }
   findViewById<TextView>(R.id.points).text="Points: $points"
}
```

Displaying Toasts
``` kotlin
   Toast.makeText(context:this, text:Ÿou got this", Toast.LENGTH_SHORT)
```

###Sizing and positioning 
Absolute positioning (C++,c# etc)
Layout managers (Java, Kotlin, Android):

ViewGroup
- layouts are described in XML
- Android provides several pre-existing layout managers; you can define your own cutsom layouts if needed
- layouts can be nested to achieve combinations of features

in the Java code and XML
- an Activity is a ViewGroup
- various Layout classes are also ViewGroups
- widgets can be added to a ViewGroup, which will then manage that widget's position/size behavior

XML (Data Markup), Describing hierarchical text data
``` XML
<course name="CS193A"quarter="19wi">
   <instructor>Marty Stepp</instructor>
   <ta>none</ta>
</course>
```

LinearLayout
-orientation horizontal or vertical 
``` XML
<LinearLayout...
   android:orientation="horizontal"
   android:gravity="center|right">
   <Button
      andriod:gravity="left"
      android:layout_weight=1
   />
   </LinearLayout>
```
Margin<br />
   Border<br />
      Padding<br />
         Content<br />

Gridlayout Nestedlayout Constraintlayout

Constraint layout<br />
- anchor points ( for vertical and horizontal sides)

## Lec03: Widgets, Lists
Widgets: 
1. declare/position it in your layout XML file
2. add any event handling code to your kotlin code file
```kotlin
class MainActivity: AppCompatActivity(){
   ...
   fun myButtonClick(view: View){
      // event-handling code goes here
    }
}

Common widget attributes
android:clickable="bool" set to false to disable
```

| Tables| Area|
| -------------|:-------------:|
| android:clickable="bool"       | set to false to disable              |
| android:id="@+id/id"           | unique ID for use in Kotlin code     |
| android:onClick="function"     | function to call in activity when clicked <br />(mustbe public,void and take a View arg)|
| android:text="text"           | text to put in the button    |


- Text Edit, Hint, Input Type (will change the keyboard)
- res/drawable > images
- ImageView, Resource >XML (android:src = "@drawable/tmntleo" , id="@+id/imageView", scaleType
- CheckBox (link)
- RadioButton (non mutually exclusive)-> Radiogroup (group RadioButtons Together , for mutually exclusive)
- Switch (link)

Link radiobuttons onclick to radioButtonClick function
```kotlin
fun radioButtonClick(view: View){
   // To identify which radio button
   if(view== rb_leo){
      turtle.setImageResource(R.drawable.tmntleo)
   }
   
   // Kotlin Switch
    when(view){
       rb_leo->turtLe.setImageResource(R.drawable.tmntleo)
    }
    // 2 Kotlin Switch
     val id=when(view){
       rb_leo->R.drawable.tmntleo
       else R.drawable.default
    }
}
```
List 
onCreate> 
characterList.setOnItemClickListener{
   //Write a function 
}

## Lec 4 More Lists ; Files
List adapter

val list=ArrayList<String?()
list.add("Hello")
list.add("Goodbye")

val rand=Random()
val index=rand.nextInt(list.size)
val word=list[index]

val defns= ArrayList<String>()
defns.add("a gretting")

( Error> Log Cat , too early to set Adapter)
private val defns= ArrayList<String>()
private val myAdapter= ArrayAdapter<String>(this, android.R.layout.simple_list_item_1,defns)

definitions_list.setOnItemClickListener{_,_,index,_ ->
   defns.remove(index)
   myAdapter.notifyDataSetChanged()
}

( Instead )
private var defns
private var myAdapter
<!-- private lateinit var myAdapter: ArrayAdapter<String> -->

definitions_list.setOnItemClickListener{_,_,index,_ ->
   defns.remove(index)
   myAdapter.notifyDataSetChanged()
}
defns= ArrayList<String>()
myAdapter= ArrayAdapter<String>(this, android.R.layout.simple_list_item_1,defns)


Files & Storage 
- internal storage :private to app
- external storage :shared file system used by all apps

Internal
- res/raw

File and Stream Objects
-File
-InputSteam, OutputStream (not usuall used directly, wrap them in a reader or scanner )
- BufferedReader & Scanner 

```kotlin
private fun readDictionaryFile(){
   val reader= Scanner(resources.openRawResource(R.raw.grewords))
   while (reader.hasNextLine()){
      val line = reader.nextLine()
      Log.d("tag","the line i: $line")
      val pieces = line/split("\t")
      wordToDefn.put(pieces[0], pieces[1])
   }
}
```

## Lec 05 Multiple acitivites and intents
- Create activity, addWordActivity and addWord.xml
- Create Layout in XML (Create Widgets and Layout)

Activity and Intent.
Intent an object representing a desired action

```xml
<--AndroidManifest.xml-->
<activity android:name=".MainActivity">
<intent-filter Mainactivity> 
```

Uses of Intents
- to start an activity
- to start a service
- to broadcast a message to another app or service
- types of intent ( Explicit, Implicit)

Creating an Intent (Start secondActivity)
```kotlin
fun addWordBUttonClick(view:View){
   val myIntent=Intent(this,AddWordActivity::class.java)
   myIntent.putExtra("Name",value) //Store extra data key/value pairs
   startActivity(myIntent)
}
```
After submit button ( Return data to Mainactivity)
```kotlin
private val WORDS_FILE_NAME="word.txt"

val word=word_to_add.text.toSTring()
val defn=word_definition.text.toString()
val line="$word\t$defn"

//Write into .txt
val outStream= PrintStream(openFileOutput(WORDS_FILE_NAME,MODE_PRIVATE) //Can put mode append instead
outStream.println(line)
outStream.close()

//Send data via Intent, add into main activity
val myIntent=Intent()
myIntent.putExtra("word",word)
myIntent.putExtra("defn", defn)
setResult(RESULT_OK, myIntent)
finish()
```
Waiting for a Result
```kotlin
private val SOME_CODE= 1 //1-65535

fun addWordButtonClick(view:View){
   val myIntent=Intent(this,AddWordActivity::class.java)
   startActivity(myIntent, SOME_CODE)
}

override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?){
   if (requestCode==SOME_CODE){
      //unpack the word and definition sent back from AddWordActivity
      val word=myIntent?.getStringExtra("word") ?:"" //? to handle null, if (myIntent!=null) another way to handle
      val defn=myIntent?.getStringExtra("defn") ?:""
      wordToDefn[word]=defn
      words.add(word)
   }
}
```

## Lec 17 Services and Notifications
2 types of service 
normal and onBind

(Service allow stuff to run even when app is closed, or when phone bootsup) 
```kotlin
// MainActivity
Intent intent=new Intent(this, DownloadService.class);
intent.putExtra("url",webPageURL);
StartService(intent)
```

```kotlin
// Service
public int onStartCommand(Intent intent , int flags, int startId){
   String url = intent.getStringExtra("url");
   return START_STICKY;
```

setAction and getAction for intent with multiple action eg.(play, stop, pause)
//Activity class
intent.setAction("download")

//Service class
String action=intent.getAction()
if(action.equals("download)){...}

Activity -calls-> Service 
Service-broadcast-> All Apps

```kotlin
// Service
public int onStartCommand(Intent intent , int flags, int startId){

   if(intent.getAction().equals("download")){
      String url = intent.getStringExtra("url");
      String contents= Downloader.downLoadFake(url)

      // finished! Tell everyone
      Intent done = new Intent();
      done.setAction("downloadcomplete");
      done.putExtra("url",url)
      done.putExtra("data",contents);
      sendBroadcast(done);
   }   
   return START_STICKY;
```
Your Activity can hear broadcasts using a broadcast receiver
```kotlin
// MainActivity
protected void onCreate(Bundle savedInstanceState){
   super.onCreate(savedInstanceState);
   setCOntentView(R.layout.activity_download)
   
   //Register receiver
   IntentFilter filter = new IntentFilter();
   filter.addAction("downloadcomplete");
   registerReceiver(new MyReceiver(),filter);
}

private class MyReceiver extends BroadcastReceiver{
   public void onReceive(Context context, Intent intent){
   // handle the received broadcast message
   }
}
```
Services and threading
- if the service is busy, the app UI will freeze up
- to make the service and app more independent and responsive, the service should handle tasks in threads (Concurrency)

```kotlin
// Service
public int onStartCommand(Intent intent , int flags, int startId){

   if(intent.getAction().equals("download")){
      Thread thread= new Thread(new Runnable(){
         public void run(){
            String url = intent.getStringExtra("url");
            String contents= Downloader.downLoadFake(url)

            // finished! Tell everyone
            Intent done = new Intent();
            done.setAction("downloadcomplete");
            done.putExtra("url",url)
            done.putExtra("data",contents);
            sendBroadcast(done);
         }
      });
      thread.start();
   }   
   return START_STICKY;
```
Android provides a class called IntentService(subclass of Service) that runs all of its tasks in a single extra thread.
- Great for a queue of long-running tasks to do one-at-a-time.
- Instead of overriding onStartCommand, use onHandleIntent

Notification 
- A message displayed to the user outside of any apps UI in a top notification drawer area
- used to indicate system events status of service tasks
- go along with services normally

- Create a notificaiton using a Notification.Builder
- Use NotificationManager to send out the notification.
```kotlin
Notification.BUilder builder=new Notificaiton.Builder(this)
               .setContentTitle("title")
               .setContentText("text")
               .setAutoCancel(true)
               .setSmallIcon(R.drawable.icon)
Notification notification = builder.build();

NotificationManager manager =(NotificationManager)
   getSystemService(Context.NOTIFICATION_SERVICE);
manager.notify(ID, notification);
```

Example (Notification when download is done)
```kotlin
// Service
public int onStartCommand(Intent intent , int flags, int startId){

   if(intent.getAction().equals("download")){
      Thread thread= new Thread(new Runnable(){
         public void run(){
            String url = intent.getStringExtra("url");
            String contents= Downloader.downLoadFake(url,5000);
            
            Notification.Builder builder = new Notification.Builder(this)
                     .setContentTitle("Download complete")
                     .setContentText("I received the file:"+url)
                     .setSmallIcon(R.drawable.icon_download);
            Notification notification = builder.build();

            NotificationManager manager =(NotificationManager)
               getSystemService(Context.NOTIFICATION_SERVICE);
            manager.notify(ID, notification);

            // finished! Tell everyone
            Intent done = new Intent();
            done.setAction("downloadcomplete");
            done.putExtra("url",url)
            done.putExtra("data",contents);
            sendBroadcast(done);
         }
      });
      thread.start();
   }   
   return START_STICKY;
```
Notification with intent ( Notification to do something when you tap on it )
```kotlin
Notification.BUilder builder=new Notificaiton.Builder(this)
               .setContentTitle("title")
               .setContentText("text")
               .setAutoCancel(true)
               .setSmallIcon(R.drawable.icon)
               
Intent intent = new Intent(this, ActivityClassName.class);
Intent.putExtra("key1","value1");
PendingIntent pending= PendingIntent.getActivity(this, 0, intent, 0);
builder.setContentIntent(pending);

Notification notification = builder.build();

NotificationManager manager =(NotificationManager)
   getSystemService(Context.NOTIFICATION_SERVICE);
manager.notify(ID, notification);
```
## Broadcast receiver
Listen to sendbroadcast either from own service or other apps/android services

## Lec 11: Databases and SQL
crud (create read update delete)

- A databse can be located in many places:
   - within ur android
   - on a remote webserver
   - spread throughout many remote servers"in the cloud")

DataBase Software
Oracle, Microsoft SQL Server Acess, PostgreSQL, MySQL, SQLite

SELECT name
FROM countries
WHERE population > 200000;

ERM diagram
- Entity
- Relationship

Schema, constraints 
