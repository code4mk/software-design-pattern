# Decorator design pattern

* extending funtionalities.

```php
interface FoodItem
{
    public function cost();
}
// all we need is a burger
class Burger implements FoodItem
{
    public function cost () {
        return 4;
    }
}
// Now decorate with cheese
class Cheese implements FoodItem
{
    private $item;
    public function __construct (FoodItem $item) {
        $this->item = $item;
    }
    public function cost () {
        return $this->item->cost() + 0.25;
    }
}
// now decorate with patty
class Patty implements FoodItem
{
    private $item;
    public function __construct (FoodItem $item) {
        $this->item = $item;
    }
    public function cost () {
        return $this->item->cost() + 1;
    }
}
$b = new Burger();
$c = new Cheese($b); // passing burger
$pb = new Patty($b); // passing burger
$pc = new Patty($c); // passing cheese burger
$b->cost(); // 4
$c->cost(); // 4.25
$pb->cost(); // 5
$pc->cost(); // 5.25
```

# resources

* https://sourcemaking.com/design_patterns/decorator/php
* https://medium.com/@sirajul.anik/understanding-decorator-pattern-with-php-implementation-7f536e742bb0
