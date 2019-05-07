# Android Notes
## Layout
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



