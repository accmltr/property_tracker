# property_tracker
Made as a utility for game development in scala-games. Simple solution for the pattern of storing values that come with subscription-based events that broadcasts when the values are changed.

# Example
```
import lib.property.Property

class Character(val name: String, val maxHp: Int) {
  val hp = Property(
    maxHp,
    i =>
      require(
        i <= maxHp && i >= 0,
        "Cannot set hp to higher than max or lower than 0"
      )
      i
  )
}

val wolf = new Character("Wolf", 70)

wolf.hp.value // : Int = 70

wolf.hp.onChange += ((o, n) => println(s"hp changed from $o to $n"))

wolf.hp.value = 54 // hp changed from 70 to 54

wolf.hp.value // : Int = 54

wolf.hp.value = 71 // java.lang.IllegalArgumentException: requirement failed: Cannot set hp to higher than max or lower than 0
```
![image](https://github.com/accmltr/property_tracker/assets/19354678/cef93fcd-72a7-4fd6-9a8f-7168559a2832)
