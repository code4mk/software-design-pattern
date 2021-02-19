* create a complex object step by step.

```php
// Builder design pattern                                                            
// code4mk

<?php

class SmartPhone
{
    public $camera;
    public $ram;
}

class SamsungPhone extends SmartPhone
{
    //
}

class RedmiPhone extends SmartPhone
{
    //
}

interface SmartPhoneBuilder
{
    public function addCamera();
    public function addRam();
    public function getProduct();
}

class SamsungPhoneBuilder implements SmartPhoneBuilder
{
    private $phone;
    private $optinos;
    public function __construct($options)
    {
        $this->phone = new SamsungPhone();
        $this->options = $options;

    }

    public function addCamera()
    {
        $this->phone->camera = $this->options['camera'];
    }

    public function addRam()
    {
        $this->phone->ram = $this->options['ram'];
    }

    public function getProduct()
    {
        return $this->phone;
    }
}

class RedmiPhoneBuilder implements SmartPhoneBuilder
{
    private $phone;
    private $optinos;
    public function __construct($options)
    {
        $this->phone = new RedmiPhone();
        $this->options = $options;

    }

    public function addCamera()
    {
        $this->phone->camera = $this->options['camera'];
    }

    public function addRam()
    {
        $this->phone->ram = $this->options['ram'];
    }

    public function getProduct()
    {
        return $this->phone;
    }
}

class SmartPhoneCreator
{
    public function build(SmartphoneBuilder $builder)
    {
        $builder->addCamera();
        $builder->addRam();
        return $builder->getProduct();
    }
}

$creator = new SmartPhoneCreator();
$samsungBuilder = new SamsungPhoneBuilder(['camera' => '64', 'ram' => '16']);
$redmiBuilder = new RedmiPhoneBuilder(['camera' => '12','ram' => '64']);

print_r ($creator->build($samsungBuilder));
print_r ($creator->build($redmiBuilder));
```
![](https://refactoring.guru/images/patterns/content/builder/builder-en.png)

# resources

* https://designpatternsphp.readthedocs.io/en/latest/Creational/Builder/README.html
*  https://refactoring.guru/design-patterns/builder
* https://gist.github.com/aliselcuk/59e702e55d26de15c7fa2ef7907373c2
* https://gist.github.com/firefoxrebo/f78ab3c352b77279c94e208570eaf187
