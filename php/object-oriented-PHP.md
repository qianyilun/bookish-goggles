# Object Oriented PHP

* Interface

  * extends 1 class

  * implements multiple interfaces

    ```php
    <?php
    interface Singable
    {
        public function sing();
    }
    ```

* Class 

  ```php
  <?php
  class Animal
  {
      protected $name;
      protected $favorite_food;
      protected $sound;
      protected $id;
  
      public static $number_of_animals = 0;
  
      const PI = "3.14159";
  
      // constructor
      function __construct()
      {
          // access field
          $this->id = 1;
  
          // access static variable
          DemoClass::$number_of_animals++;
      }
  
      function __get($name)
      {
          // be careful about the $name and name
          // $this->name is not correct
          return $this->$name;
      }
  
      function __set($name, $value)
      {
          $this->name = $value;
      }
  
      function __toString()
      {
          return $this->name;
      }
  
      function run() {
          echo $this->name . "runs like crazy <br />";
      }
  }
  ```

* Abstract Class

  ```php
  <?php
  abstract class AbstractClassExample
  {
      abstract function RandomFunction($attr1);
  }
  ```

* Class with **extends** and **implements**

  ```php
  <?php
  class Dog extends Animal implements Singable
  {
      function run()
      {
          // extended
          // parent::run();
  
          echo $this->name . " runs like Dog";
  
      }
  
      function sing()
      {
          echo $this->name . " sings Wang Wang";
      }
  }
  ```

* Access and Run

  ```php
  $dog = new Dog();
  $animal = new Animal();
  
  $dog->sing();
  $animal->run();
  ```


#### reference

* [Object Oriented PHP](https://youtu.be/5YaF8xTmxs4) 