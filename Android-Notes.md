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

definitions_list.setOnItemClickListener{_,_,index,_ ->
   defns.remove(index)
   myAdapter.notifyDataSetChanged()
}
defns= ArrayList<String>()
myAdapter= ArrayAdapter<String>(this, android.R.layout.simple_list_item_1,defns)


